
저장소에서 `Settings → Pages → Source → GitHub Actions`를 선택합니다. `Deploy from a branch`나 제안된 Jekyll/Static HTML 워크플로를 선택하지 않습니다. 이미 Vite용 `deploy.yml`이 있기 때문입니다.

활성화 전 첫 Actions는 다음 오류로 실패했습니다.

```text
Get Pages site failed
Please verify that the repository has Pages enabled
```

Source를 GitHub Actions로 바꾼 뒤 `Actions → 실패 작업 → Re-run jobs`로 다시 실행합니다. 모든 단계가 초록색이면 성공입니다.

```text
https://seongui2030.github.io/garbage-classifier-web/
```

배포 후 휴대폰에서 모델 준비, 사진 촬영, 열 개 확률을 검사합니다. GitHub Pages는 HTTPS이므로 카메라 입력 테스트에 적합합니다. 배포 직후 몇 분 동안 이전 캐시가 보이면 강력 새로고침합니다.

