
상위 `C:\CNN-WebApp`에서 Git을 시작하면 GitHub 첫 화면에 `garbage-classifier-web` 폴더가 한 번 더 나타납니다. Actions는 저장소 최상위의 `.github/workflows`만 인식하므로 루트가 중요합니다.

정상 확인:

```powershell
cd C:\CNN-WebApp\garbage-classifier-web
git rev-parse --show-toplevel
```

결과가 프로젝트 폴더여야 합니다. 원격 상태를 백업한 뒤 내부 프로젝트를 독립 저장소로 만들고 `--force-with-lease`로 올바른 구조를 반영했습니다. `--force-with-lease`는 확인한 원격 이후 다른 변경이 있으면 중단하므로 무조건 `--force`보다 안전합니다.

GitHub 첫 화면에 `.github`, `public`, `src`, `package.json`이 바로 보이면 성공입니다. VSCode도 `File → Open Folder`에서 프로젝트 폴더 자체를 엽니다.

