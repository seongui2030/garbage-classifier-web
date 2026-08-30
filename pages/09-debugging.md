# 08-1. 프로젝트 생성과 모델 배치

```powershell
npm create vite@latest garbage-classifier-web -- --template react
cd garbage-classifier-web
npm install
npm install @tensorflow/tfjs
npm run dev
```

모델 파일을 다음과 같이 배치합니다.

```text
public/model/
├── model.json
├── group1-shard1of1.bin
├── labels.json
└── labels.txt
```

개발 서버의 포트가 5173 사용 중이면 Vite가 5174를 선택합니다. 오류가 아니므로 터미널의 `Local` 주소를 사용합니다.

```text
http://localhost:5174/model/model.json
http://localhost:5174/model/labels.json
```

JSON이 보이면 정적 파일 경로가 성공한 것입니다. 기본 Vite 화면이 보이면 주소 끝의 `/model/...`이 빠졌거나 다른 포트에 접속한 것입니다.

