
## 포트 변경

```text
Port 5173 is in use, trying another one...
Local: http://localhost:5174/
```

오류가 아니라 다른 서버가 5173을 사용하여 5174로 바뀐 것입니다. 항상 터미널의 주소를 사용합니다.

## TensorFlow.js 미설치

```text
Failed to resolve import "@tensorflow/tfjs"
```

```powershell
npm install @tensorflow/tfjs
npm list @tensorflow/tfjs
```

설치 성공 결과는 `@tensorflow/tfjs@4.22.0`이었습니다.

## JSON 대신 기본 Vite 화면

`/model/model.json`을 입력했는데 기본 화면이 나오면 다른 포트의 Vite 서버에 접속했거나 `public/model` 구조가 틀렸을 수 있습니다. `dir public\model`과 브라우저 Network 탭으로 확인합니다.

