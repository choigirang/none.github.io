---
title: "JavaScript 9장 - 개념짚기 (6)"
excerpt: "자바스크립트"

categories: JavaScript
tags: [자바스크립트, JavaScript]

toc: true
toc_sticky: true

date: 2023-07-02
last_modified_at: 2022-07-05
---

# JavaScript

## String

- 백틱은 여러 줄을 표현하는 것이 가능하다.
  - 따옴표로 줄바꿈을 표현하기 위해서는 역슬래시 n을 써야한다. `\n`

```js
let str = `예시를 보여주기
위한 백틱입니다.`;

let str2 = "예시를 보여주기 \n위한 백틱입니다.";
```

### indexOf(text)

- 특정 문자를 찾을 때 사용되며, 찾는 문자가 없을 시 -1을 반환한다.
- `if`문을 쓸 때, 찾는 문자의 위치가 0일 시, `0 = false`이기 때문에 주의해야 한다.
  - 그렇기에 `-1`보다 큰가로 비교해야 한다.

```js
let str = "Hi guys. Nice to meet you.";

str.indexOf("to"); // 14
str.indexOf("man"); // -1

if (str.indexOf("Hi")) console.log("Hi가 포함된 문장입니다."); // false
if (str.indexOf("Hi") > -1) console.log("Hi가 포함된 문장입니다."); // Hi가 포함된 문장입니다.
```

### slice(n,m)

- `n`을 시작점으로 `m`이전의 문자열까지를 반환하고, `m`이 음수면 끝에서부터 반환한다.

```js
let str = "abcdefg";

str.slice(2); // cdefg
str.slice(0, 5); // abcde
str.slice(2, -2); // cde
```

### substring(n,m)

- `n`과 `m` 사이의 문자열을 반환한다.
- `n`과 `m`을 바꿔도 동작한다.
- 음수는 0으로 인식한다.

```js
let str = "abcdefg";

str.substring(2, 5); // cde
str.substring(5, 2); // cde
```

### substr(n,m)

- `substring`과 비슷하게 생겼지만, `n`부터 시작하여 `m`개를 가져온다.
