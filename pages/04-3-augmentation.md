
데이터 증강은 학습할 때 사진을 조금씩 바꾸어 새로운 상황을 경험하게 합니다. 원본 파일을 늘리지 않고 매 배치에서 변형합니다.

```python
data_augmentation = tf.keras.Sequential([
    tf.keras.layers.RandomFlip("horizontal"),
    tf.keras.layers.RandomRotation(0.08),
    tf.keras.layers.RandomZoom(0.10),
    tf.keras.layers.RandomContrast(0.10),
], name="data_augmentation")
```

증강은 현실적으로 가능한 범위여야 합니다. 쓰레기를 180도 뒤집어도 의미가 같을 수 있지만 글자가 중요한 배터리나 포장지는 과도한 회전이 불리할 수 있습니다. 밝기 변화를 너무 크게 주면 색과 투명도 특징이 사라집니다.

데이터 증강 층은 학습 때만 활성화되고 예측 때는 꺼집니다. TensorFlow.js 변환에서는 불필요한 랜덤 층을 제거하고 가중치가 있는 CNN 층만 복사했습니다.

### 비교 실험

같은 학습 횟수로 증강 없음/약한 증강/강한 증강을 비교합니다. 학습 정확도만이 아니라 검증 정확도와 휴대폰 사진 결과를 함께 기록합니다.

