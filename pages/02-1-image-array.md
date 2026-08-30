# 03-2. 두 데이터셋 합치기

병합은 ‘폴더를 한곳에 복사’하는 것보다 신중해야 합니다. 같은 파일명이 존재하면 덮어쓸 수 있으므로 출처 접두사와 연속 번호를 붙입니다.

```python
from pathlib import Path
import shutil

def copy_images(source_dir, target_dir, prefix):
    target_dir.mkdir(parents=True, exist_ok=True)
    count = 0

    for path in sorted(source_dir.iterdir()):
        if path.suffix.lower() not in {".jpg", ".jpeg", ".png", ".webp"}:
            continue

        count += 1
        new_name = f"{prefix}_{count:06d}{path.suffix.lower()}"
        shutil.copy2(path, target_dir / new_name)

    return count
```

`prefix`가 `data1_metal`, `data2_metal`이라면 파일 이름만 보고 출처를 알 수 있습니다. `:06d`는 번호를 여섯 자리로 맞춥니다.

```python
metal_count1 = copy_images(src1 / "metal", merged / "metal", "data1_metal")
metal_count2 = copy_images(src2 / "metal", merged / "metal", "data2_metal")
print(metal_count1, metal_count2)
```

복사 후에는 원본 수와 대상 증가량이 맞는지 확인합니다. 성공 메시지를 무조건 출력하지 말고 실제 반환값과 파일 수를 비교합니다.

