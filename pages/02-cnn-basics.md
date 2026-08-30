# 08-4. 최고 클래스와 10개 확률 표시

```jsx
const output = model.predict(inputTensor);
const values = await output.data();

const results = labels.map((label, index) => ({
  ...label,
  probability: Number(values[index]) * 100,
}));

results.sort((a, b) => b.probability - a.probability);
```

`map`은 라벨 열 개와 확률 열 개를 같은 번호로 묶습니다. `sort`는 확률이 큰 순서로 정렬합니다. 원래 `index`는 보존해야 모델 번호를 추적할 수 있습니다.

```jsx
const best = results[0];

{best.probability < 60 && (
  <p>신뢰도가 낮습니다. 밝은 곳에서 물체 하나만 다시 촬영하세요.</p>
)}
```

화면에는 1위 이름, 영문 이름, 신뢰도, 낮은 신뢰도 안내, 열 개 막대그래프를 표시합니다. 확률 막대 너비는 `${probability}%`로 설정할 수 있습니다.

접근성을 위해 사진에는 `alt`, 버튼에는 설명 가능한 글자를 넣고, 색만으로 성공·실패를 구분하지 않습니다.

