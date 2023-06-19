---
title: "TypeScript 10장 - 적용타입 (1)"
excerpt: "타입스크립트"

categories: TypeScript
tags: [타입스크립트, TypeScript, 이벤트타입]

toc: true
toc_sticky: true

date: 2023-06-20
last_modified_at: 2022-06-20
---

# TypeScript

## Input 이벤트

- `useState`를 이용해 우리가 입력한 값을 기억하고 바꿔주고 싶을 때, 입력이 발생하는 `onChange`의 `event.target.value`에 대한 값에 대한 타입 지정이다.

```jsx
const [example, setExample] = useState<string>("");
const handleChange = (e) => {
    setExample(e.target.value);
}

return (
    <input type="text" onChange=((e) => hanldeChange(e))/>
)
```
