# 04-4. 클래스 불균형과 가중치

클래스별 이미지 수가 달라도 학습은 가능하지만, 차이가 크면 많은 클래스 쪽으로 예측이 치우칠 수 있습니다. 이 데이터는 최대와 최소 클래스 수 차이가 약 3.93배였습니다.

클래스 가중치는 적은 클래스의 오답에 더 큰 손실을 부여합니다.

```python
from sklearn.utils.class_weight import compute_class_weight
import numpy as np

weights = compute_class_weight(
    class_weight="balanced",
    classes=np.unique(train_labels),
    y=train_labels
)

class_weight = {
    int(index): float(weight)
    for index, weight in enumerate(weights)
}
```

학습에 전달합니다.

```python
model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=30,
    class_weight=class_weight
)
```

가중치가 모든 문제를 해결하지는 않습니다. 적은 클래스의 이미지 다양성이 부족하면 같은 사진을 단순 복제하는 것보다 다양한 배경, 각도, 조명으로 새 사진을 추가하는 편이 좋습니다. 평가도 전체 정확도 하나가 아니라 클래스별 정밀도와 재현율을 확인합니다.

