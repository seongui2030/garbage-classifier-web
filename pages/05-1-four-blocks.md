
```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Input(shape=(180, 180, 3)),
    data_augmentation,
    tf.keras.layers.Rescaling(1.0 / 255.0),

    tf.keras.layers.Conv2D(32, 3, padding="same", activation="relu"),
    tf.keras.layers.MaxPooling2D(),

    tf.keras.layers.Conv2D(64, 3, padding="same", activation="relu"),
    tf.keras.layers.MaxPooling2D(),

    tf.keras.layers.Conv2D(128, 3, padding="same", activation="relu"),
    tf.keras.layers.MaxPooling2D(),

    tf.keras.layers.Conv2D(256, 3, padding="same", activation="relu"),
    tf.keras.layers.MaxPooling2D(),

    tf.keras.layers.GlobalAveragePooling2D(),
    tf.keras.layers.Dropout(0.40),
    tf.keras.layers.Dense(128, activation="relu"),
    tf.keras.layers.Dropout(0.25),
    tf.keras.layers.Dense(10, activation="softmax")
])
```

채널 수를 늘리는 이유는 깊은 층이 더 다양한 특징 조합을 표현하게 하기 위해서입니다. Dropout은 학습 중 일부 연결을 임시로 꺼 특정 특징에 지나치게 의존하는 것을 줄입니다. 예측 때는 자동으로 꺼집니다.

```python
model.summary()
assert model.input_shape == (None, 180, 180, 3)
assert model.output_shape == (None, 10)
```

`None`은 배치 이미지 수가 고정되지 않았다는 뜻입니다.

