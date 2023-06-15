---
title: "JavaScript 8장 - 개념짚기 (2)"
excerpt: "자바스크립트"

categories: JavaScript
tags: [자바스크립트, JavaScript, 객체, 메서드, 프로퍼티]

toc: true
toc_sticky: true

date: 2023-06-14
last_modified_at: 2022-06-14
---

# JavaScript

## Object 객체

- `key`와 `value`로 구성되어 여러 개의 속성을 가질 수 있는 것을 말한다.
- `key`가 갖고 있는 값에 접근하려면 두 가지 방법으로 접근할 수 있다.

```js
const data = {
  sample: "this is a sample",
};

data.sample; // this is a sample
data["sample"]; // this is a sample
```

- 또한 객체에 속성을 추가하거나 삭제할 수도 있다.

```js
const data = {
  sample: "A",
};

data.sample2 = "B";
data["sample3"] = "C";
delete data.sample3;

// data = {sample: "A", sample2: "B"}
```

- `in`연산자를 사용해서 객체 안에 존재하는 속성을 확인할 수 있다.
- 어떤 값이 넘어올지 확신할 수 없을 때 사용한다.

```js
const data = {
  name,
  age
}

"name" in data; // true
"no-data" in data; // false

function user(data){
  if("age" in data || "name" in data){
    return true;
  }else if(!("example" in data)){
    return false;
  }
}

const Mike = {
  age: 30,
  location: seoul
}

const Jane = {
  gender: "girl";
}

user(Mike); // true
user(Jane); // false

for(x in Mike){
  console.log(x)
}
// 30
// seoul
```

## method

- 객체의 속성에 할당 된 함수를 의미한다.

```js
const act = {
  fly: function () {
    console.log("날아요");
  },
  ride: function (data) {
    console.log(data + "를 타고 갑니다.");
  },
};

console.log(act.ride("자전거")); // 자전거를 타고 갑니다.

const example = {
  name: "Jane",
  user: function () {
    console.log(`$(this.name) 안녕하세요.`);
  },
};
```
