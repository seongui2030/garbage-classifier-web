
```text
tensorflowjs_model/
├── model.json
├── group1-shard1of1.bin
├── labels.json
└── labels.txt
```

`model.json`에는 층 구조, 활성화 함수, 입력 형태, 가중치 파일 이름이 있습니다. `.bin`에는 학습된 실수 가중치가 이진 형식으로 저장됩니다. 모델이 크면 여러 shard 파일로 나뉠 수 있으며 모두 함께 배포해야 합니다.

`labels.json`은 모델 자체가 만든 파일이 아니라 앱이 출력 번호와 이름을 연결하기 위한 파일입니다.

```json
[
  {"index": 0, "english": "battery", "korean": "배터리"},
  {"index": 1, "english": "cardboard", "korean": "카드보드"}
]
```

파일을 수정할 때 `.bin` 이름을 바꾸면 `model.json`의 `weightsManifest`와 불일치합니다. 네 파일을 같은 `public/model` 폴더에 둡니다.

