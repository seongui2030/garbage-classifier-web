# 06-3. 휴대폰 사진 한 장 분류

Colab에서 휴대폰 사진을 업로드하고 동일한 전처리로 예측합니다.

```python
from google.colab import files
from tensorflow.keras.utils import load_img, img_to_array
import numpy as np

uploaded = files.upload()
image_path = next(iter(uploaded))

image = load_img(image_path, target_size=(180, 180))
array = img_to_array(image)
batch = np.expand_dims(array, axis=0)

probabilities = model.predict(batch, verbose=0)[0]
order = np.argsort(probabilities)[::-1]

for rank, index in enumerate(order, start=1):
    print(rank, CLASS_NAMES[index], f"{probabilities[index]*100:.2f}%")
```

실제 사례에서 의류 39.77%, 금속 34.63%, 종이 20.02%가 나왔습니다. 1위만 보면 의류지만 2위와 차이가 작고 최고 확률도 낮습니다. 이것은 모델이 사진을 잘 이해했다고 보기 어렵습니다.

```python
best = probabilities[order[0]] * 100
if best < 60:
    print("신뢰도가 낮습니다. 밝은 곳에서 물체 하나만 다시 촬영하세요.")
```

실제 사진은 모델을 칭찬하기 위한 시험이 아니라 학습 데이터의 빈틈을 찾는 자료입니다.

