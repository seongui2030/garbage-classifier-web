
학습 모델은 Google Drive의 Keras 형식으로 저장합니다.

```python
MODEL_PATH = (
    "/content/drive/MyDrive/CNN_Garbage_Project/"
    "garbage_10class_cnn.keras"
)

model.save(MODEL_PATH)
```

다시 불러올 때 학습을 이어 가지 않고 예측·변환만 한다면 `compile=False`를 사용합니다.

```python
loaded_model = tf.keras.models.load_model(
    MODEL_PATH,
    compile=False
)

print(loaded_model.input_shape)
print(loaded_model.output_shape)
```

정상 형태는 `(None,180,180,3)`과 `(None,10)`입니다. 파일 존재와 크기도 확인합니다.

```python
from pathlib import Path

path = Path(MODEL_PATH)
assert path.exists()
print(path.stat().st_size / 1024**2, "MB")
```

이 프로젝트는 H5 중간 저장에서 직렬화 오류가 발생했으므로, 성공 경로에서는 H5를 사용하지 않았습니다. 원본 `.keras`를 불러와 표준 층으로 깨끗한 추론 모델을 다시 만들고 가중치를 복사한 뒤 TensorFlow.js로 직접 저장했습니다.

