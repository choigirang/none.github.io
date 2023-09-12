---
title: "React 53장 - Eslint 설치 오류"
excerpt: "프로젝트 기본 세팅"

categories: React
tags: [React, 리액트, Eslint, Typescript, Prettier]

toc: true
toc_sticky: true

date: 2023-09-12
last_modified_at: 2023-09-12
---

# React

## Eslint

```js
PS C:\Users\choigirang\Desktop\code-container> npm install @typescript-eslint/eslint-plugin
npm WARN config global `--global`, `--local` are deprecated. Use `--location=global` instead.
npm ERR! code ERESOLVE
npm ERR! ERESOLVE could not resolve
npm ERR!
npm ERR! While resolving: code-container@0.1.0
npm ERR! Found: @typescript-eslint/eslint-plugin@5.62.0
npm ERR! node_modules/@typescript-eslint/eslint-plugin
npm ERR!   @typescript-eslint/eslint-plugin@"^5.5.0" from eslint-config-react-app@7.0.1
npm ERR!   node_modules/eslint-config-react-app
npm ERR!     eslint-config-react-app@"^7.0.0" from react-scripts@5.0.0
npm ERR!     node_modules/react-scripts
npm ERR!       react-scripts@"5.0.0" from the root project
npm ERR!   peerOptional @typescript-eslint/eslint-plugin@"^4.0.0 || ^5.0.0" from eslint-plugin-jest@25.7.0
npm ERR!   node_modules/eslint-plugin-jest
npm ERR!     eslint-plugin-jest@"^25.3.0" from eslint-config-react-app@7.0.1
npm ERR!     node_modules/eslint-config-react-app
npm ERR!       eslint-config-react-app@"^7.0.0" from react-scripts@5.0.0
npm ERR!       node_modules/react-scripts
npm ERR!         react-scripts@"5.0.0" from the root project
npm ERR!   1 more (the root project)
npm ERR!
npm ERR! Could not resolve dependency:
npm ERR! @typescript-eslint/eslint-plugin@"*" from the root project
npm ERR!
npm ERR! Conflicting peer dependency: @typescript-eslint/parser@6.6.0
npm ERR! node_modules/@typescript-eslint/parser
npm ERR!   peer @typescript-eslint/parser@"^6.0.0 || ^6.0.0-alpha" from @typescript-eslint/eslint-plugin@6.6.0
npm ERR!   node_modules/@typescript-eslint/eslint-plugin
npm ERR!     @typescript-eslint/eslint-plugin@"*" from the root project
npm ERR!
npm ERR! Fix the upstream dependency conflict, or retry
npm ERR! this command with --force, or --legacy-peer-deps
npm ERR! to accept an incorrect (and potentially broken) dependency resolution.
npm ERR!
npm ERR! See C:\Users\choigirang\AppData\Local\npm-cache\eresolve-report.txt for a full report.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\choigirang\AppData\Local\npm-cache\_logs\2023-09-11T15_00_31_723Z-debug-0.log
```

- Eslint 세팅 중 발생한 에러
- `npm install eslint`로 여러 가지 질문을 통해 설치가 진행되는데, 이와 관련된 패키지나 플러그인이 설치된다.
- 다른 블로그 글들을 찾아봐도 이상없이 잘 진행되던데 나는 계속 에러가 발생했다.
- 패키지 자체에 작성 후 `npm install`도 해보고 다 밀어버린 다음에 새로 깔아보는데도 같은 오류가 발생했다.
- 관련 에러에 대한 자료가 잘 안 나오던 중 드디어 찾을 수 있었다.
- [참조링크](https://stackoverflow.com/questions/76828444/failed-to-install-typescript-eslint-eslint-plugin)

- 글에서도 볼 수 있듯이 package-json 파일에서 eslint의 plugin을 찾아보면 필요한 버전을 볼 수 있다.
- 설치에 필요한 패키지 버전들을 먼저 설치 후 plugin을 설치
