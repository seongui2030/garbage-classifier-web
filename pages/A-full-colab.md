# 부록 A. 전체 Colab 코드

아래 코드는 각 장의 핵심을 한 노트북에서 실행하기 위한 기준 코드다. 데이터 경로는 실제 압축 해제 결과에 맞게 바꾼다.

```python
import os, random, json, numpy as np, tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers
SEED=42
random.seed(SEED); np.random.seed(SEED); tf.random.set_seed(SEED)
DATA='/content/waste6'; IMG=(160,160); BATCH=32

train_ds=keras.utils.image_dataset_from_directory(DATA,validation_split=.2,
    subset='training',seed=SEED,image_size=IMG,batch_size=BATCH)
val_ds=keras.utils.image_dataset_from_directory(DATA,validation_split=.2,
    subset='validation',seed=SEED,image_size=IMG,batch_size=BATCH,shuffle=False)
names=train_ds.class_names
AUTOTUNE=tf.data.AUTOTUNE
train_ds=train_ds.shuffle(1000,seed=SEED).prefetch(AUTOTUNE)
val_ds=val_ds.prefetch(AUTOTUNE)

augment=keras.Sequential([layers.RandomFlip('horizontal'),
    layers.RandomRotation(.08),layers.RandomZoom(.1)])
model=keras.Sequential([
    layers.Input((160,160,3)), augment, layers.Rescaling(1./255),
    layers.Conv2D(32,3,padding='same',activation='relu'), layers.MaxPooling2D(),
    layers.Conv2D(64,3,padding='same',activation='relu'), layers.MaxPooling2D(),
    layers.GlobalAveragePooling2D(), layers.Dropout(.2),
    layers.Dense(6,activation='softmax')])
model.compile(keras.optimizers.Adam(1e-3),'sparse_categorical_crossentropy',['accuracy'])
cb=[keras.callbacks.EarlyStopping(patience=4,restore_best_weights=True),
    keras.callbacks.ModelCheckpoint('/content/best.keras',save_best_only=True)]
history=model.fit(train_ds,validation_data=val_ds,epochs=20,callbacks=cb)
model.save('/content/waste_cnn.keras')
with open('/content/class_names.json','w') as f: json.dump(names,f)
```

## 실행 점검표

- 클래스 순서가 예상과 같은가?
- 훈련·검증 데이터가 겹치지 않는가?
- 마지막 Dense의 출력 수가 6인가?
- 손실 함수가 정수 라벨 형식과 맞는가?
- 가장 좋은 epoch의 가중치를 복원했는가?
