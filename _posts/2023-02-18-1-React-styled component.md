---
title:  "React 9장 - Styled-Component"
excerpt: "styled component를 이용한 UI"

categories: React
tags: [React, 리액트, map, key, 컴포넌트, JSX]

toc: true
toc_sticky: true
 
date: 2023-02-18
last_modified_at: 2023-02-18
---
# Styled Component
- 기존 DOM을 만드는 방식인, css나 scss 파일을 따로 생성하고 이를 불러와 사용하는 것이 아닌 컴포넌트 내부에 style을 작성하는 것을 말한다.
- style을 따로 불러와 사용하지 않기 때문에 css의 속성이 전역으로 중첩되어 적용되는 것을 방지한다는 장점이 있다.
```node
npm install styled-component
```

## styled component 만들기
- `const 컴포넌트명 = styled.태그명` 문법으로 만든다.
- 만들고자 하는 컴포넌트의 render 함수 밖에서 작성한다.

## 스타일에 props 적용하기
- styled-component는 변수에 의해 스타일을 바꿀 수 있다는 장점이 있다.
- 예를 들어, `email` 이라는 `state` 값에 따라 `ExampleWrap` 컴포넌트에 `prop` 으로 내려주는 `active` 값이 `true` 혹은 `false` 로 바뀐다.
- styled-component 는 내부적으로 `props`를 받을 수 있고, `props` 에 따라 스타일을 변경할 수 있다.

## 예시
```jsx
import React,{ useState } from "react";
import styled from "styled-component";

const ExampleWrap = () => {
    const [email, setEmail] = useState("");

    return(
        <ExampleWrap active={email.length}>
            <Button>Hello</Button>
            <NewButton color="blue">new Button</NewButton>
        </ExampleWrap>
    );
}

const ExampleWrap = styled.div`
  background: ${({ active }) => {
    if (active) {
      return "white";
    }
    return "#eee";
  }};
  color: black;
`;

const Button = styled.button`
    width: 200px;
    padding: 30px;
    `;

// Button 컴포넌트 상속
const NewButton = styled.Button`
    // NewButton 컴포넌트에 color가 있으면
    // 입력된 color 값을 사용,
    // 없으면 'red' 사용
    color: ${props => porps.color || "red"}
    `;

export default Example;
```

## Mixin css props
- `css props` 는 자주 쓰이는 css 속성을 담는 변수이다.
- `css 변수명 = css` 로 작성한다.


```jsx
const flexCenter = css`
    display: flex;
    justify-content: center;
    align-items: center;
    `;

const FlexBox = div`
    ${flexCenter}
    `;
```

## 다른 파일에서 컴포넌트 import 하기
- 해당 파일에서 정의한 css를 `export` 하여 다른 파일에서 `import` 할 수 있다.


```jsx
// Login.jsx
export const LoginContainer = styled.div`
    background: red;
    `;

// Other.jsx
import {LoginContainer} from "Login.jsx";

const Other = () => {
    return <LoginContainer></LoginContainer>;
};
```

## 반응형 디자인
- [styled-component 를 이용한 반응형 디자인 참조](https://velog.io/@syoung125/CSS-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9-%EB%94%94%EC%9E%90%EC%9D%B8-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)


```jsx
import React from "react"
import styled,{css} from "styled-component"

const sizes = {
    desktop: 1024,
    tablet: 768
};

// sizes 객체에 따라 자동으로 media 쿼리 함수를 만들어준다.
const media = Object.keys(sizes).reduce((acc,cur)=>{
    acc[label] = (...args) => css`@meadia (max-width: ${sizes[label] / 16}em) {
        ${css(...args)}
    }`;

    return acc;
}, {});

const Box = styled.div`
    // props로 넣어준 값을 직접 전달해줄 수 있다.
    background: ${props => props.color || "blue"};
    padding: 1rem;
    display: flex;
    width: 1024px;
    margin: 0 auto;
    ${media.desktop`width: 768px;`}
    ${media.tablet`width: 768px;`};
    `;

    
```