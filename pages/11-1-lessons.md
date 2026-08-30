# 08-3. 휴대폰 사진 전처리

휴대폰 후면 카메라를 요청합니다.

```jsx
<input
  type="file"
  accept="image/*"
  capture="environment"
  onChange={handleImageChange}
/>
```

브라우저와 기기에 따라 카메라 또는 갤러리 선택 화면이 나옵니다. 사진은 중앙 정사각형으로 자르고 `180×180`으로 바꿉니다.

```jsx
function makeInputTensor(imageElement) {
  return tf.tidy(() => {
    const original = tf.browser.fromPixels(imageElement, 3);
    const [height, width] = original.shape;
    const size = Math.min(height, width);
    const top = Math.floor((height - size) / 2);
    const left = Math.floor((width - size) / 2);

    return tf.image
      .resizeBilinear(
        original.slice([top, left, 0], [size, size, 3]),
        [180, 180],
        true
      )
      .toFloat()
      .expandDims(0);
  });
}
```

최종 형태는 `[1,180,180,3]`입니다. 모델 내부에 `Rescaling(1/255)`가 있으므로 `.div(255)`를 추가하지 않습니다.

