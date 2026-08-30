# 07-2. Python 3.11 변환 환경

최신 Colab Python과 TensorFlow.js 의존성 사이에 `np.object`, `distutils`, Protobuf 충돌이 발생했습니다. 성공한 방법은 독립 환경입니다.

```python
import subprocess

subprocess.run(["python", "-m", "pip", "install", "uv"], check=True)
subprocess.run(["uv", "python", "install", "3.11"], check=True)
subprocess.run([
    "uv", "venv", "/content/tfjs-env", "--python", "3.11"
], check=True)
subprocess.run([
    "uv", "pip", "install",
    "--python", "/content/tfjs-env/bin/python",
    "numpy==1.26.4", "tensorflow==2.19.0",
    "tensorflowjs==4.22.0", "setuptools==75.8.2"
], check=True)
```

CNN에 필요 없는 Decision Forests의 Protobuf 충돌은 변환 스크립트에서 빈 모듈로 차단했습니다.

```python
import sys, types
sys.modules["tensorflow_decision_forests"] = types.ModuleType(
    "tensorflow_decision_forests"
)
import tensorflowjs as tfjs
```

이는 CNN 기능을 제거하지 않습니다. 의사결정숲 변환 모듈만 불러오지 않게 합니다.

