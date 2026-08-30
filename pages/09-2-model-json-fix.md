
Keras 3.15.1이 만든 입력 속성을 TensorFlow.js 4.22가 이해하지 못하여 다음 오류가 발생했습니다.

```text
An InputLayer should be passed either a batchInputShape or an inputShape
```

`model.json`의 속성 이름을 변경했습니다.

```text
batch_shape → batch_input_shape
```

다음 오류는 가중치 이름 앞의 모델 접두사가 원인이었습니다.

```text
Provided weight data has no target variable:
garbage_10class_web_model/conv2d/kernel
```

`model.json`의 가중치 이름에서 다음 접두사를 일괄 제거했습니다.

```text
garbage_10class_web_model/
```

변경 전 `garbage_10class_web_model/conv2d/kernel`, 변경 후 `conv2d/kernel`입니다. `.bin` 숫자는 변경하지 않았습니다. 수정 후 Network의 캐시를 끄고 강력 새로고침하여 모델 준비 완료를 확인했습니다.

