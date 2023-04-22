---
title: "React 47장 - React-Query (2)"
excerpt: "React Query 배워보기 - "

categories: React
tags: [proxy, api, cors, useQuery, pagenation]

toc: true
toc_sticky: true

date: 2023-04-22
last_modified_at: 2023-04-22
---

# React

## React Query

#### 1. Pagenation

- 이전 글에서 작동했던 것처럼 의존성 배열을 추가하여, 데이터를 가진 페이지의 번호가 바뀔 때마다 새로운 데이터들을 불러오도록 지정하여 button에 대한 이벤트를 처리할 수 있다.

```jsx
async function fetchPosts() {
  const response = await fetch("http://example.com/posts?limit=10&page=1");
  return response.json();
}

function Post() {
  const [pageNum, setPageNum] = useState(0);

  const { data, isLoading, isError, error } = useQuery("post", fetchPosts);

  return (
    <>
      ...중략
      <button>Previous Page</button>
      <button>Next Page</button>
    </>
  );
}
```

- 기존에 작성된 코드에서 의존성 배열을 추가해주고, `fetchPosts`에 pageNum에 관한 정보를 넘겨주어 pageNum에 해당하는 페이지에 들어있는 데이터들을 받아오도록 한다.
- post에 관한 각 댓글의 목록을 받아오는 방식과 똑같다.

```jsx
function Post() {
  const [pageNum, setPageNum] = useState(1);
  const maxPage = 10;

  const { data, isLoading, isError, error } = useQuery(["post", pageNum], () =>
    fetchPosts(pageNum)
  );

  return (
    <>
      ...중략
      <button disable={pageNum <= 0} onClick={() => setPageNum(pageNum - 1)}>
        Previous Page
      </button>
      <button disable={pageNum >= 10} onClick={() => setPageNum(pageNum + 1)}>
        Next Page
      </button>
    </>
  );
}

async function fetchPosts(pageNum) {
  const response = await fetch(
    `http://example.com/posts?limit=10&page=${pageNum}`
  );
  return response.json();
}
```

#### 2.Prefetching

- App 컴포넌트에서 선언한 queryClient의 메서드인 prfetch 쿼리를 가져온다.
- 가져온 훅을 기능 컴포넌트에서 선언 후 사용한다.
- isLoading 을 사용하여 page가 바뀔 때마다 매번 새로운 데이터를 요청하고 이를 기다리는 과정을 반복하면 사용자 경험에 좋지 않은 영향을 끼친다.
- 따라서 page가 바뀔 때마다 다음 페이지에 대한 데이터를 미리 받아오는 작업을 거치고, 이 데이터를 캐시해놓아 사용자가 다음 page를 눌렀을 떄 캐시된 데이터를 미리 보여주는 방식을 사용한다.

```jsx
import { useQuery, useQueryClient } from "react-query";

function Posts() {
  const queryClient = useQueryClient();
  useEffect(() => {
    if(pageNUm < maxPage>){
      const nextPage = pageNum + 1;
      queryClient.prefetchQuery(["posts", nextPage], () => fetch(nextPage));
    }
  }, [pageNum, queryClient]);
}
```

- pageNum이 바뀔 때마다 nexPage에 대한 데이터를 미리 가져온다.
- `prefetch`로 사용할 key 값은 우리가 이전에 사용한 fetch의 키와 동일하다.
- 우리가 이전 페이지로 돌아갔을 때도 데이터를 유지하도록 설정을 추가한다.

```jsx
const { data, isLoading, isError, error } = useQuery(
  ["posts", pageNum],
  () => fetchPosts(pageNum),
  {
    staleTime: 2000,
    keepPreviousData: true,
  }
);
```
