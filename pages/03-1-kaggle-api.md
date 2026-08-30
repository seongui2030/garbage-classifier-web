
Kaggle API는 데이터셋을 코드로 내려받는 통로입니다. 토큰은 비밀번호처럼 관리합니다. 파일 이름만 `.env.local`로 바꾼다고 자동 인증되는 것은 아닙니다. Kaggle CLI가 요구하는 환경변수나 정해진 인증 위치에 설정해야 합니다.

Colab에서는 토큰을 출력하지 않고 환경변수로 전달합니다.

```python
import os

# 실제 값은 코드에 직접 적지 않고 Colab 보안 저장소를 권장합니다.
os.environ["KAGGLE_API_TOKEN"] = "발급받은_토큰"
```

데이터셋 자체의 소유자/이름을 확인한 뒤 다운로드합니다.

```bash
kaggle datasets download -d asdasdasasdas/garbage-classification
kaggle datasets download -d sumn2u/garbage-classification-v2
```

노트북 주소와 데이터셋 주소는 다를 수 있습니다. Kaggle의 다른 사람이 작성한 Notebook이 사용한 데이터는 화면 오른쪽 Input/Data 영역에서 실제 데이터셋 식별자를 확인해야 합니다.

### 보안 점검

- 토큰을 Markdown, 출력창, GitHub에 올리지 않습니다.
- 노출되면 Kaggle 설정에서 즉시 폐기하고 새 토큰을 만듭니다.
- `.env.local`은 `.gitignore`에 포함합니다.

