---
title: "React 48장 - useCallback과 useMemo"
excerpt: "useCallback과 useMemo 최적화"

categories: React
tags: [useCallback, useMemo]

toc: true
toc_sticky: true

date: 2023-06-27
last_modified_at: 2023-06-27
---

# React

## useMemo, useCallback

- 컴포넌트의 성능을 최적화하기 위해 사용되는 훅이다.
- 리액트에서 렌더링 => 함수 호출 => 변수 초기화의 과정에서 불필요한 리렌더링을 최소화시켜 원래 있던 값이나 함수를 재사용하여 성능을 높이기 위해 사용한다.

## useMemo

- `useMemo`는 동일한 계산을 반복해야 할 때, 계산한 값을 메모리에 저장하여 동일한 계산이 반복 수행하는 것을 방지한다.
- 동일한 값을 반환하는 계산을 반복적으로 수행해야 할 경우, 이미 저장돼있는 값을 활용하여 반복된 동작이 실행되지 않도록 한다.

```jsx
function RepeatCalc() {
  const value = calculate();
  return <div>{value}</div>;
}

function calculate() {
  return 10;
}
```

- 위 코드에서 함수의 렌더링,호출,초기화 과정이 반복되기 때문에, 컴포넌트가 렌더링 될 때마다 `value`라는 변수가 초기화되며 재호출된다.
- 만약 함수가 무겁고 복잡하다면 비효율적인 호출이 반복되는 것인데, 렌더링되더라도 `calculate`를 재호출하지 않고 저장되어있는 값을 재사용한다.
- `useMemo`는 값을 메모리에 저장시켜놓고 재사용하기 때문에 메모리에 값을 저장하는 것만으로도 메모리 사용이 발생하고, 중복되는 결과값으로 불필요한 렌더링이 일어나지 않는 경우, 사용하지 않는 것이 메모리 측면에서 효율적이다.

### useMemo 구조

- 첫 번째 인자로는 콜백함수를, 두 번째 인자로는 의존성 배열을 받는다.
- 의존성 배열 안에 있는 값이 업데이트 될 때만 콜백함수를 다시 호출하여 메모리에 저장된 값을 업데이트한다.

```jsx
const value = useMemo(() => {
  return calculate();
}, [item]);
```

### useMemo 사용 예시

```jsx
function App() {
  const [number, setNumber] = useState(0);
  const [txt, setTxt] = useState("");

  const increase = () => {
    console.log("숫자가 증가합니다.");
    setNumber(number + 1);
  };

  const decrease = () => {
    console.log("숫자가 감소합니다.");
    setNumber(number - 1);
  };

  const reset = () => {
    console.log("글자가 초기화됩니다.");
    setTxt("");
    return txt;
  };

  return (
    <div>
      <p>숫자 : {number}</p>
      <button onClick={increase}>increase</button>
      <button onClick={decrease}>decrease</button>

      <p>글자 : {txt}</p>
      <input type="text" onChage={(e) => setTxt(e.target)} />
      <button onClick={reset}>reset</button>
    </div>
  );
}
```

**삽질**

- 예시를 만들어보려고 위와 같은 코드를 짰지만, 내가 예상했던대로 상태값이 변경됨에 따라 컴포넌트가 리렌더링 되면서 실행됐어야 하지만 아무런 변화가 없었다.
- 나는 지금껏 상태를 변경하는 함수만을 작성했을 뿐이며, 컴포넌트가 리렌더링된다 해도 `button`을 통해 발생하는 실행함수이기 때문에 콘솔에 현재 실행한 함수밖에 찍히지 않았다.

### 새로운 예시

- 이와 같이 작성하면 컴포넌트가 리렌더링됨에 따라 `p`태그의 `plus10()`함수가 실행되기 때문에 상태값이 변경될 때마다 콘솔에 **그냥 값**이 찍히게 된다.
- `useMemo`를 활용해보자.

```jsx
export default function App() {
  const [number, setNumber] = useState(0);
  const [txt, setTxt] = useState("");

  const increase = () => {
    console.log("숫자가 증가합니다.");
    setNumber(number + 1);
  };

  const decrease = () => {
    console.log("숫자가 감소합니다.");
    setNumber(number - 1);
  };

  const plus10 = () => {
    console.log("그냥 값");
    const result = 10 + 10;
  };

  return (
    <div>
      <p>숫자 : {number}</p>
      <button onClick={increase}>increase</button>
      <button onClick={decrease}>decrease</button>

      <p>숫자에 10을 더한 값 : {plus10()}</p>
    </div>
  );
}
```

### useMemo 사용하기

- 생각보다 간단하게 바꿀 수 있다.
- 기존의 코드에서 `initialNum`은 바뀌지 않기 때문에 콘솔이 찍히지 않는다.
- `plus10`함수에 대한 리렌더링이 일어나지 않는다는 것을 의미한다.
- 삽질을 하느라 오래 걸렸지만 어떤 느낌으로 사용되지는 알 수 있었으며, 더 복잡한 예시를 작성해볼 필요성을 느꼈다.

```jsx
function App() {
  const [number, setNumber] = useState(0);
  const [initialNum, setinitialNum] = useState(0);

  const increase = () => {
    console.log("숫자가 증가합니다.");
    setNumber(number + 1);
  };

  const decrease = () => {
    console.log("숫자가 감소합니다.");
    setNumber(number - 1);
  };

  const plus10 = useMemo(() => {
    console.log("그냥 값");
    const result = initialNum + 10;
    return result;
  }, [initialNum]);

  //   const plus10 = () => {
  //     console.log("그냥 값")
  //     return initialNum + 10;
  //   }

  return (
    <div>
      <p>숫자 : {number}</p>
      <button onClick={increase}>increase</button>
      <button onClick={decrease}>decrease</button>

      <p>숫자에 10을 더한 값 : {plus10}</p>
    </div>
  );
}
```

## useCallback
