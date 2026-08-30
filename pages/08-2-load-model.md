
```jsx
import * as tf from "@tensorflow/tfjs";

async function loadModel() {
  await tf.ready();

  const modelUrl =
    `${import.meta.env.BASE_URL}model/model.json`;
  const labelsUrl =
    `${import.meta.env.BASE_URL}model/labels.json`;

  const [model, response] = await Promise.all([
    tf.loadLayersModel(modelUrl),
    fetch(labelsUrl),
  ]);

  if (!response.ok) {
    throw new Error("labels.json 불러오기 실패");
  }

  const labels = await response.json();
  return { model, labels };
}
```

`await`는 비동기 작업이 끝날 때까지 함수의 다음 줄을 기다립니다. 모델과 라벨을 동시에 요청하여 시간을 줄입니다. `BASE_URL`은 로컬의 `/`와 GitHub Pages의 `/garbage-classifier-web/`을 자동으로 맞춥니다.

빈 입력으로 한 번 예열하면 첫 실제 예측 지연을 줄일 수 있습니다. 사용이 끝난 텐서는 `dispose()`하여 휴대폰 메모리를 정리합니다.

