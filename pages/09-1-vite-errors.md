# 10. Git과 GitHub Pages 배포

Git은 파일 변화의 기록이고 GitHub는 그 기록을 공유하는 원격 저장소입니다. GitHub Pages는 정적 파일을 HTTPS 웹사이트로 제공합니다. Vite 프로젝트는 소스 파일을 그대로 게시하지 않고 `npm run build`로 `dist`를 만든 뒤 배포합니다.

```text
VSCode 수정
→ git add
→ git commit
→ git push
→ GitHub Actions
→ npm ci
→ npm run build
→ dist 업로드
→ GitHub Pages
```

웹앱은 서버에 비밀 키가 필요하지 않고 브라우저에서 모델을 실행하므로 정적 Pages에 적합합니다. 모델 파일도 사용자 기기로 내려가므로 교육용 공개 모델이라는 점을 이해합니다.

