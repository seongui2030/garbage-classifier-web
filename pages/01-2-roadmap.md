# 03-4. 손상·중복·오분류 이미지 점검

확장자가 `.jpg`라도 실제 이미지가 아닐 수 있습니다. Pillow로 파일을 열어 검증합니다.

```python
from PIL import Image

def is_valid_image(path):
    try:
        with Image.open(path) as image:
            image.verify()
        return True
    except Exception:
        return False
```

손상 파일은 즉시 영구 삭제하기보다 검토 폴더로 이동하여 기록을 남깁니다.

```python
REVIEW_DIR = Path("/content/to_review")
REVIEW_DIR.mkdir(parents=True, exist_ok=True)

for class_name in CLASS_NAMES:
    for path in (MERGED_DIR / class_name).iterdir():
        if not is_valid_image(path):
            target = REVIEW_DIR / f"{class_name}_{path.name}"
            shutil.move(path, target)
```

`NameError: REVIEW_DIR is not defined`는 변수를 만들기 전에 사용했기 때문입니다. 코드 셀을 일부만 실행하면 이런 문제가 생깁니다. 경로 설정 → 폴더 생성 → 함수 정의 → 함수 호출 순서를 지킵니다.

중복 검사는 파일 내용의 해시값을 이용할 수 있습니다. 같은 사진이 학습과 테스트에 동시에 존재하면 모델이 암기한 사진을 맞혀 성능이 실제보다 높아집니다. 또한 클래스마다 무작위 표본을 30장 이상 눈으로 확인하여 잘못 분류된 사진, 여러 물체가 함께 있는 사진, 워터마크가 큰 사진을 검토합니다.

