
프로젝트 루트에서 빌드 후 Git에 기록합니다.

```powershell
npm run build
git status
git add .
git commit -m "쓰레기 CNN 분류 React 웹앱 구현"
git branch -M main
git remote add origin https://github.com/사용자이름/garbage-classifier-web.git
git push -u origin main
```

`node_modules`와 `dist`는 `.gitignore`로 제외합니다. `package.json`과 `package-lock.json`을 올리면 Actions가 동일 패키지를 설치할 수 있습니다.

원격에 README 같은 커밋이 이미 있어 Push가 거부되면 강제 Push부터 하지 않습니다. 원격 내용을 `fetch`하고 병합하거나, 프로젝트 루트가 맞는지 먼저 확인합니다.

```powershell
git rev-parse --show-toplevel
git remote -v
```

앞으로 수정 후에는 `add → commit → push` 세 단계로 자동 재배포됩니다.

