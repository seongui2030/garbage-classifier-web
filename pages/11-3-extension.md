# 07-3. 깨끗한 추론 모델과 가중치 복사

원본의 데이터 증강 층을 제외하고 같은 표준 CNN을 다시 만듭니다. 새 모델의 합성곱과 Dense 구조는 원본과 정확히 같아야 합니다.

```python
original = tf.keras.models.load_model(MODEL_PATH, compile=False)
clean = tf.keras.Sequential([
    tf.keras.layers.Input(shape=(180,180,3), name="input_image"),
    tf.keras.layers.Rescaling(1/255, name="rescaling"),
    tf.keras.layers.Conv2D(32,3,padding="same",activation="relu",name="conv2d"),
    tf.keras.layers.MaxPooling2D(),
    tf.keras.layers.Conv2D(64,3,padding="same",activation="relu",name="conv2d_1"),
    tf.keras.layers.MaxPooling2D(),
    tf.keras.layers.Conv2D(128,3,padding="same",activation="relu",name="conv2d_2"),
    tf.keras.layers.MaxPooling2D(),
    tf.keras.layers.Conv2D(256,3,padding="same",activation="relu",name="conv2d_3"),
    tf.keras.layers.MaxPooling2D(),
    tf.keras.layers.GlobalAveragePooling2D(),
    tf.keras.layers.Dropout(0.40),
    tf.keras.layers.Dense(128,activation="relu"),
    tf.keras.layers.Dropout(0.25),
    tf.keras.layers.Dense(10,activation="softmax")
])
```

가중치 개수와 모양을 검사하고 복사합니다.

```python
old_w, new_w = original.get_weights(), clean.get_weights()
assert len(old_w) == len(new_w)
assert all(a.shape == b.shape for a, b in zip(old_w, new_w))
clean.set_weights(old_w)
```

무작위 입력으로 두 예측을 비교하여 최대 차이가 `1e-5` 이하인지 확인합니다. 실제 결과는 0이었습니다.

