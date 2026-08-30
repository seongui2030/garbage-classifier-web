# 03-3. 10개 클래스 폴더 만들기

Keras의 폴더 기반 로더는 하위 폴더 이름을 알파벳순으로 클래스 번호에 연결합니다. 이 프로젝트의 순서는 다음과 같습니다.

```python
CLASS_NAMES = [
    "battery", "cardboard", "clothes", "food", "glass",
    "metal", "paper", "plastic", "shoes", "trash"
]
```

폴더를 만들고 누락을 검사합니다.

```python
from pathlib import Path

MERGED_DIR = Path("/content/garbage_10class")

for class_name in CLASS_NAMES:
    (MERGED_DIR / class_name).mkdir(parents=True, exist_ok=True)

missing = [name for name in CLASS_NAMES if not (MERGED_DIR / name).exists()]
assert not missing, f"누락된 폴더: {missing}"
```

클래스별 수를 출력합니다.

```python
IMAGE_EXTENSIONS = {".jpg", ".jpeg", ".png", ".webp"}

for name in CLASS_NAMES:
    count = sum(
        1 for p in (MERGED_DIR / name).iterdir()
        if p.suffix.lower() in IMAGE_EXTENSIONS
    )
    print(f"{name:10s}: {count:5d}")
```

라벨 순서는 학습, Colab 예측, `labels.json`, React 화면에서 끝까지 동일해야 합니다. 순서가 바뀌면 모델이 배터리라고 계산해도 앱이 카드보드라고 표시할 수 있습니다.

