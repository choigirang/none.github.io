---
title: "React 49장 - rendering, re-render"
excerpt: "rendering, re-render"

categories: React
tags: [렌더링, 리렌더링, 리액트, 기초]

toc: true
toc_sticky: true

date: 2023-06-27
last_modified_at: 2023-06-27
---

# React

- `useMemo`의 리렌더링에 대한 정보들을 들여다보다가, 아직 리액트의 기본적인 특성들을 깊이 이해하지 못 했다는 생각이 들어 작성해보는 글이다.

## rendering

- 리액트에서 렌더링이란, 리액트를 설치하면 볼 수 있는 `ReactDOM.render()` 함수가 그것이다.
- 또한, 초기에 컴포넌트의 정보를 토대로 화면이 어떻게 구성될지를 결정하고, 보여질 수 있도록 화면을 구성하는 것이 **렌더링**이다.

## re-render

- 리렌더링은 초기에 구성된 화면에 대한 내용에서, 상태값이 업데이트 되거나 어떠한 컴포넌트에 대해 연결되어 있는 컴포넌트들에 대해 새롭게 구성하는 것이다.
- 리렌더링 과정을 거치면 컴포넌트가 새롭게 갈아끼워지는 것인데,이러한 과정에서 초기에 구성했던(렌더링된) 화면과 변경을 감지하고 새롭게 구성될(리렌더링) 화면과의 비교를 통해, 변화가 있는 요소들을 DOM에 반영하는 것이다.
- 리렌더링은 어떠한 값을 사용하고 있는 여러 개의 컴포넌트가 존재할 때, 그 값이 변경된다면 그 값을 반영한 모든 컴포넌트들이 전부 재구성된다.
- 이렇게 잦은 렌더링 과정이 일어날 경우, 메모리 측면에서 애플리케이션 성능에 문제가 일어날 수밖에 없기 떄문에 최적화가 필요하다.

### re-render의 조건

- 리렌더링이 일어나기에는 몇 가지 조건이 있다.
- 자식 컴포넌트의 state나 props에 변경사항이 있는 것과는 무관하게, 부모 컴포넌트가 리렌더링되면 자식 컴포넌트도 리렌더링 된다.
- 부모/자식, 형제 관계를 주의해야 하는데 관련 자료를 읽다가 매우 복잡하고도 의아한 자료를 발견했다.
- [참고자료](https://velog.io/@mogulist/understanding-react-rerender-easily)
- 짧게 요약을 하자면, 부모/자식 관계로 보여지는 컴포넌트가 리렌더링의 관점에서는 아닐 수도 있기 때문에 컴포넌트의 구조만으로 부모/자식 관계를 생각하여 `"A 컴포넌트가 변하면 당연히 B 컴포넌트도 변하겠지?"`라고 생각했지만, 사실은 영향을 받지 않을 수도 있다.

```jsx
function App() {
  return (
    <Parent lastChild={<ChildC />}>
      <ChildB />
    </Parent>
  );
}

function Parent({ children, lastChild }) {
  return (
    <div className="parent">
      <ChildA />
      {children}
      {lastChild}
    </div>
  );
}
```

- `ChildB` 컴포넌트가 `Parent` 컴포넌트에 감싸져 있으므로, `Parent` 컴포넌트가 리렌더링되면 리렌더링되는 컴포넌트는 `ChildA`컴포넌트밖에 없다.
- **자식 컴포넌트란, 부모 컴포넌트의 JSX안에 사용된 모든 컴포넌트**, 로 정의되기 때문에 `ChildB`와 `ChildC`는 정확히 `App`컴포넌트의 자식들이다.
- `React DevTools`에서도 트리 구조를 확인할 수 있는데, 얼핏 보기엔 `Parent` 컴포넌트의 자식 컴포넌트라고 볼 수 있지만 `rendered by`를 확인하면 관계된 컴포넌트가 무엇인지 확인할 수 있다.
  [](https://velog.velcdn.com/images/mogulist/post/7f982312-305a-4670-aa17-ef0f6da37c37/image.png)
  [](https://velog.velcdn.com/images/mogulist/post/888d004a-f0c3-438c-b5c2-2547bfbded0c/image.png)

## 화면을 구성할 Virtual DOM과 DOM
