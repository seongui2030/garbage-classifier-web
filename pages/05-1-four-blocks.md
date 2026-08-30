# 01-3. 개발 환경과 준비물

## 학습과 서비스 환경

| 구분 | 도구 | 역할 |
|---|---|---|
| 데이터·학습 | Kaggle, Google Colab | GPU 학습과 데이터 처리 |
| 파일 보관 | Google Drive | `.keras`, ZIP 보관 |
| 웹 개발 | VSCode, Node.js, React, Vite | 브라우저 앱 제작 |
| 모델 실행 | TensorFlow.js | 브라우저 CNN 추론 |
| 버전 관리 | Git, GitHub | 코드 기록과 공유 |
| 운영 | GitHub Pages | HTTPS 정적 웹 배포 |

## 준비물 확인

- Kaggle 계정과 API 인증 수단
- Google 계정과 Colab·Drive
- Node.js LTS와 npm
- VSCode와 Git
- 테스트용 JPG 또는 PNG
- 휴대폰 Chrome 또는 Safari

## 버전 확인 명령

VSCode 터미널에서 실행합니다.

```powershell
node -v
npm -v
git --version
```

Vite 8은 지원되는 최신 Node.js가 필요합니다. 명령을 찾지 못하면 Node.js 설치 후 VSCode를 완전히 종료했다가 다시 엽니다.

## 폴더 원칙

프로젝트 루트는 `package.json`이 있는 폴더입니다.

```text
C:\CNN-WebApp\garbage-classifier-web
```

Git 명령도 이 폴더에서 실행합니다. 상위 폴더에서 `git init`을 하면 GitHub에 프로젝트 폴더가 한 단계 중첩될 수 있습니다.

## 보안 원칙

Kaggle 토큰, 비밀번호, API Key는 GitHub에 올리지 않습니다. `.env.local`은 프런트엔드에서 비밀을 완전히 보호하지 못합니다. 브라우저로 전달되는 값은 사용자가 볼 수 있으므로, 비밀 키가 필요한 기능은 별도의 서버에서 처리해야 합니다.

