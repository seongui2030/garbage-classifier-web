
프로젝트 Pages 주소에는 저장소 이름이 포함됩니다. `vite.config.js`를 설정합니다.

```javascript
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [react()],
  base: "/garbage-classifier-web/",
});
```

`.github/workflows/deploy.yml`의 핵심 단계입니다.

```yaml
name: Deploy garbage classifier to GitHub Pages
on:
  push:
    branches: [main]
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
      - uses: actions/setup-node@v7
        with:
          node-version: "lts/*"
          cache: npm
      - run: npm ci
      - run: npm run build
      - uses: actions/configure-pages@v6
      - uses: actions/upload-pages-artifact@v5
        with:
          path: "./dist"
      - id: deployment
        uses: actions/deploy-pages@v5
```

YAML은 탭이 아니라 공백 들여쓰기를 사용합니다.

