---
title: "[Vite] Vite + React + TS 기반 프로젝트 시작하기"
datePublished: Sat Nov 23 2024 14:45:48 GMT+0000 (Coordinated Universal Time)
cuid: cm3ua8sg6000408mn99vj4gfe
slug: vite-react-ts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1732372714528/013c03ec-1648-4d2b-95d1-e46d8edc0e89.png
tags: reactjs, typescript, vite

---

# 들어가며

유데미 강의를 들으면서 했던 프로젝트를 통해서 `Vite`의 여러가지 장점이 있다는 걸 느꼈고, 그래서 이번 프로젝트에서는 가볍고 빠른 개발 환경을 구축하기 위해서 `Vite + React + TypeScript`을 사용해보려고 한다.

ㅤ

# Vite를 사용해야 하는 이유

> [Vite를 사용해야 하는 이유](https://ko.vitejs.dev/guide/why.html)

공식페이지에서 설명하는 ‘Vite를 사용해야 하는 주요 이유’를 요약하자면 다음과 같다.

1. **빠른 서버 구동**: Esbuild로 의존성을 사전 번들링해 기존 번들러보다 10~100배 빠릅니다.
    
2. **효율적인 코드 제공**: 브라우저의 \*\*ESM(ES Modules)\*\*을 활용해 필요한 코드만 동적으로 처리합니다.
    
3. **빠른 갱신 속도**: 수정된 파일만 교체해 HMR 및 로딩 성능이 뛰어납니다.
    
4. **생산성과 사용자 경험 향상:** 개발 중 더 빠른 피드백 루프를 제공해 생산성을 높이고, 대규모 프로젝트에서도 쾌적한 작업 환경을 제공합니다.
    
5. **최적화된 빌드**: Rollup으로 트리 셰이킹, 청크 분할 등 최적화를 제공합니다.
    

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><strong>즉, Vite는 번들러 중심의 기존 개발 도구가 겪던 성능 문제를 해결하며, 빠르고 개발 환경을 제공하는 빌드 도구로, Vite를 사용하면 프로젝트에서 빠른 개발과 빌드 속도를 경험할 수 있다.</strong></div>
</div>

ㅤ

# 시작하기

### 설치

```powershell
$ npm create vite@latest [프로젝트 이름] --template react-ts
```

이렇게 작성하면 프로젝트의 이름과 사용하려는 템플릿을 직접 지정할 수도 있다.

### 실행

```powershell
$ npm run dev
```

ㅤ

# 절대 경로 설정하기

`TypeScript`를 사용할 경우, `vite.config.js`와 `tsconfig.json` 파일에 절대 경로 속성을 추가해줘야 한다.

#### vite.config.js

```javascript
// vite.config.js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: [
      { find: "@", replacement: path.resolve(__dirname, "src") },
      { find: "@pages", replacement: path.resolve(__dirname, "src/pages") },
    ],
  },
});
```

#### tsconfig.json

`baseUrl`: 기본 경로 설정 `paths`: 지정하고 싶은 절대 경로를 **"별칭: 경로"** 순으로 지정

```json
{
  "compilerOptions": {
    ...
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
      "@pages/*": ["src/pages/*"],
    }
    ...
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

`baseUrl` 설정에 따라서 `paths`의 속성도 수정해야 한다.

```json
"baseUrl": "src",
"paths": {
  "@/*": ["*"],
  "@pages/*": ["pages/*"],
  "@components/*":["components/*"]
}
```

이렇게 지정하고 나면 절대경로를 사용할 수 있다.

```javascript
// 상대경로
import reactLogo from "./assets/react.svg"

// 절대경로
import reactLogo from "@/assets/react.svg";
```

그런데 이렇게 설정하면 다음과 같은 오류가 발생한다.

> **'path' 모듈 또는 해당 형식 선언을 찾을 수 없습니다.**

`TypeScript`가 `@types/node`를 찾지 못해서 발생하는 오류라고 한다. 이런 경우에는 `@types/node` 패키지를 추가하면 해결된다.

```powershell
$ npm install -D @types/node
```

ㅤ

# 참고

* [\[Vite, TypeScript\] Vite + 타입스크립트 환경에서 절대 경로 설정하기!](https://shape-coding.tistory.com/entry/Vite-TypeScript-Vite-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-%EC%A0%88%EB%8C%80-%EA%B2%BD%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)
    
* [Vite 시작하기](https://ko.vitejs.dev/guide/)
    

ㅤ