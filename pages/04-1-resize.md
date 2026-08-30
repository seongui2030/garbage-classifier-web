
여러 장을 한꺼번에 변환하여 별도 폴더에 저장할 수 있습니다. 원본을 보존하고 출력 폴더를 따로 사용합니다.

```python
from PIL import Image, ImageOps
from pathlib import Path

def convert_to_180(source, target):
    target.mkdir(parents=True, exist_ok=True)

    for path in source.iterdir():
        if path.suffix.lower() not in {".jpg", ".jpeg", ".png"}:
            continue

        with Image.open(path) as image:
            image = image.convert("RGB")
            image = ImageOps.fit(
                image,
                (180, 180),
                method=Image.Resampling.LANCZOS
            )
            image.save(target / f"{path.stem}.jpg", quality=92)
```

`ImageOps.fit`은 비율을 찌그러뜨리지 않고 중앙을 잘라 정사각형으로 만듭니다. 단순 `resize((180,180))`는 긴 사진을 눌러 물체 모양을 왜곡할 수 있습니다.

학습 로더가 자동 리사이즈한다면 모든 원본을 미리 저장 변환할 필요는 없습니다. 다만 휴대폰 앱과 같은 전처리를 확인하기 위한 별도 실습으로 유용합니다.

### 검사

```python
with Image.open(sample_path) as image:
    print(image.size, image.mode)
```

정상 출력은 `(180, 180) RGB`입니다.

