# 07-4. model.json과 bin 생성·검사

```python
from pathlib import Path
import tensorflowjs as tfjs

OUTPUT = Path("/content/tfjs_model")
tfjs.converters.save_keras_model(clean, str(OUTPUT))

assert (OUTPUT / "model.json").exists()
bin_files = list(OUTPUT.glob("*.bin"))
assert bin_files
```

JSON을 열어 `weightsManifest`를 확인합니다.

```python
import json

data = json.loads((OUTPUT / "model.json").read_text(encoding="utf-8"))
assert "weightsManifest" in data
```

결과는 `model.json` 약 0.008MB, `.bin` 약 1.61MB였습니다. 라벨 파일을 UTF-8로 저장하고 ZIP으로 묶어 Drive에 보관했습니다.

```python
import shutil
shutil.make_archive("/content/tensorflowjs_model", "zip", OUTPUT)
```

변환 성공 기준은 파일 생성만이 아닙니다. 원본과 추론 모델 예측 일치, JSON 문법, manifest, 모든 bin 존재, 라벨 열 개 순서를 함께 확인합니다.

