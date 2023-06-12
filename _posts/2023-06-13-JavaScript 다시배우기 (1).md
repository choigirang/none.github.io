---
title: "JavaScript 7장 - 개념짚기 (1)"
excerpt: "자바스크립트"

categories: JavaScript
tags: [자바스크립트, JavaScript]

toc: true
toc_sticky: true

date: 2023-06-13
last_modified_at: 2022-06-13
---

# JavaScript

## 자료형

- `typeof null`은 `Object` 객체형으로 표현된다. `null`은 객체가 아니지만 자바스크립트의 초기 버전의 오류로 하위 호환성을 위해 수정되고 있지 않다.

## alert, prompt, confirm

### alert

- 사용자에게 확인창을 보여준다.
- `alert("링크로 이동합니다")`
  <img width="445" alt="스크린샷 2023-06-13 오전 3 31 28" src="https://github.com/choigirang/choigirang.github.io/assets/118104644/7577b509-179a-4ff4-8363-57d791c71ebc">

- 추가적인 이벤트 설정도 가능하다.
- `if(alert("링크로 이동합니다")) document.location = "http://exampleLink.com"`

### prompt

- `alert, confirm`과 비슷하게 사용자가 입력할 수 있는 입력창이 생성된다.
- 두 개의 입력값을 받을 수 있는데 함수의 첫 번째 인수에는 타이틀을 나타내고, 두 번째 인수에는 사전에 들어갈 기본 입력값이 들어간다.
- 입력받은 값은 무조건 문자열로 표현되기 때문에 사용자가 입력한 값을 활용하고자 한다면 숫자형으로 변환하여 사용해야 한다. => `Number()`
- `prompt("예약일을 입력해주세요", "2020-10-")`

![예시](https://github.com/choigirang/choigirang.github.io/assets/118104644/ce39a09e-ef9e-45fd-a47c-83ee29946705)

### confirm

- 사용자에게 선택창을 보여준다.
- 스크립트가 일시정지되고 스타일링이 불가능하다는 단점이 있다. => 대체 라이브러리 존재
- `confirm("링크로 이동s하시겠습니까?")`

<img width="435" alt="image" src="https://github.com/choigirang/choigirang.github.io/assets/118104644/476af1ea-8b0f-4cdf-90c4-854a89abc770">

- 마찬가지로 추가적인 이벤트 설정이 가능하다.

```js
if(confirm("링크로 이동하시겠습니까?")document.location = "https://github.com/choigirang")
```

## 형변환

- 문자 90과 문자 80을 더하면 `9080`이 되지만 곱하기,나누기 등의 수식은 **자동 형변환**에 의해 올바르게 계산된다. => `"100"/2 = 50`
- 이는 오류를 발생시킬 수 있어 의도를 갖고 원하는 타입으로 변환해주어야 하며 이를 **명시적 형변환** 이라고 한다.
- `Number(), String(), Boolean()`

```js
Number(0); // null
Number(undefined); // Nan

Boolean(1); // true
Boolean("1"); // true
Boolean(0); // false
Boolean(""); // false
Boolean(" "); // true
```
