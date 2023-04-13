---
title: "React 46장 - React-Query (1)"
excerpt: "React Query 배워보기"

categories: React
tags: [proxy, api, cors]

toc: true
toc_sticky: true

date: 2023-04-13
last_modified_at: 2023-04-13
---

# React

## React Query

### 설치하기

- 서버에서 받아온 데이터의 캐시와 업데이트를 쉽게 관리할 수 있다.
- 리액트 쿼리를 설치한다.

```node
npm i react-query
npm i @types/react-query
// 타입스크립트 리액트 쿼리
```

### 사용법

- 리액트 쿼리를 설치했으면 쿼리를 사용할 최상위 컴포넌트를 감싸줘야한다.

```jsx
//App.jsx

import { QueryClient, QueryClientProvider } from "react-query";

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <div className="App"></div>
    </QueryClientProvider>
  );
}
```

- 이제 자식 컴포넌트에서 리액트 쿼리를 사용할 수 있다.
- 쿼리는 구조분해할당으로 받아올 데이터를 선언해주고, 몇 가지 인자가 온다.
  - 첫 번째는 쿼리를 사용할 `key`
  - 두 번째는 쿼리 함수를 사용한다. (데이터를 가져올 비동기 함수)

```jsx
import { useQuery } from "react-query";

async function fetchPosts() {
  const res = await fetch("http://example.com/posts");

  return res.json();
}

function Ex() {
  const { data } = useQuery("post", fetchPosts);

  return <div></div>;
}
```
