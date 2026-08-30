
혼동행렬은 실제 클래스와 예측 클래스의 조합을 표로 나타냅니다.

```python
import numpy as np
from sklearn.metrics import confusion_matrix, classification_report

y_true = []
y_pred = []

for images, labels in test_ds:
    probs = model.predict(images, verbose=0)
    y_true.extend(labels.numpy())
    y_pred.extend(np.argmax(probs, axis=1))

cm = confusion_matrix(y_true, y_pred)
print(classification_report(y_true, y_pred, target_names=CLASS_NAMES))
```

대각선은 정답, 대각선 밖은 혼동입니다. 종이를 카드보드로 자주 예측한다면 두 클래스의 두께, 접힘, 표면 질감을 더 다양하게 학습해야 합니다. 의류와 금속 혼동이 발생했다면 실제 사진을 보고 반사광, 배경, 물체 형태 등 가능한 원인을 기록합니다.

혼동행렬을 단순히 ‘틀린 개수’로 끝내지 말고 데이터 개선 질문으로 바꿉니다.

- 어느 두 클래스가 가장 많이 혼동되는가?
- 그 클래스의 학습 표본 수와 다양성은 충분한가?
- 라벨 자체가 모호한 이미지는 없는가?

