# 12. 부록

부록은 수업 중 빠르게 찾아보는 자료입니다. 클래스 순서, 주요 용어, 성공 체크리스트, 확인문제를 제공합니다. 오류가 발생하면 코드를 무작정 바꾸기 전에 체크리스트에서 이전 성공 지점을 찾습니다.

프로젝트의 핵심 약속을 다시 정리합니다.

```text
입력: RGB, 180×180, 배치 차원 포함
정규화: 모델 내부 Rescaling(1/255)
출력: 알파벳순 10개 클래스 Softmax
웹 모델: model.json + 모든 bin
웹 경로: import.meta.env.BASE_URL
배포: main Push → GitHub Actions → dist → Pages
```

