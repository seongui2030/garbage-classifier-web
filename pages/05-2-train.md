
정답이 클래스 번호 하나이므로 `SparseCategoricalCrossentropy`를 사용합니다.

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.001),
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    metrics=["accuracy"]
)
```

과적합을 줄이고 가장 좋은 시점을 저장합니다.

```python
callbacks = [
    tf.keras.callbacks.EarlyStopping(
        monitor="val_loss", patience=5,
        restore_best_weights=True
    ),
    tf.keras.callbacks.ReduceLROnPlateau(
        monitor="val_loss", factor=0.5,
        patience=2, min_lr=1e-6
    )
]

history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=30,
    callbacks=callbacks,
    class_weight=class_weight
)
```

`epoch`는 전체 학습 데이터를 한 번 본 횟수입니다. 학습 정확도는 계속 오르는데 검증 손실이 증가하면 과적합 가능성이 큽니다. 최고 학습 정확도만 보고 모델을 선택하지 않습니다.

### 기록표

| 실험 | 증강 | 가중치 | 최고 검증 정확도 | 휴대폰 결과 |
|---|---|---|---:|---|
| A | 없음 | 없음 |  |  |
| B | 약함 | 있음 |  |  |

