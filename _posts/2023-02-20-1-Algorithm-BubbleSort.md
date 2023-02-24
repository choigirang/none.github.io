---
title:  "Algorithm 256장 - BubbleSort"
excerpt: "버블정렬 알고리즘"

categories: Algorithm
tags: [Algorithm, 알고리즘, 문제풀이]

toc: true
toc_sticky: true
 
date: 2023-02-20
last_modified_at: 2023-02-20
---
# BubbleSort
## 문제
- 정수를 요소로 갖는 배열을 입력받아 오름차순으로 정렬하여 리턴한다.
  1. 첫 번째 요소가 두 번째 요소보다 크면, 두 요소의 위치를 바꾼다.
  2. 두 번째 요소가 세 번째 요소보다 크면, 두 요소의 위치를 바꾼다.
  3. 두 과정을 마지막까지 반복한다.(마지막에서 두 번째 요소와 마지막 요소를 비교)
  4. 위 과정을 한 번 거치게 되면, 가장 큰 요소가 배열의 마지막으로 밀려난다.
  5. 1 ~ 3의 과정을 첫 요소부터 다시 반복한다.
  6. 5를 통해 두 번째로 큰 요소가 배열의 마지막 바로 두 번째로 밀려난다.
  7. 1 ~ 3의 과정을 총 n번(배열의 크기) 반복한다.



```js
let bubbleSort = function(arr){
    
}
```

## 입력
- arr
  - `number` 타입을 요소로 갖는 배열
  - `arr[i]`는 정수
  - `arr[i]`의 길이는 1,000 이하


## 출력
- `number` 타입을 요소로 갖는 배열을 리턴해야 한다.
- 배열의 요소는 오름차순으로 정렬되어야 한다.
- `arr[i] <= arr[j]`(`i < j`)

## 주의사항
- `arr.sort`시용은 금지된다.

## 입출력 예시
```js
let output = bubbleSort([2,1,3]);
console.log(output)
// [1,2,3]
```

## 풀이
```js
const swap = function (indx1, indx2, arr){
    [arr[indx1], arr[indx2]] = [arr[indx2], arr[indx1]];
}

let bubbleSort = function(arr){
    let N = arr.length;

    for(let i=0; i < N; i++){
        let swaps = 0;

        for(let j=0; j < N-1-i; j++){
            if(arr[j] > arr[j+1]){
                swaps++;
                swap(j, j+1, arr);
            }
        }
    }

    if(swaps === 0){
        break;
    }

    return arr;
}
```