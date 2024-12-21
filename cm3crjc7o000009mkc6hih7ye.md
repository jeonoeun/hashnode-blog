---
title: "[프로그래머스] Lv.1 크기가 작은 부분 문자열"
datePublished: Mon Nov 11 2024 08:30:03 GMT+0000 (Coordinated Universal Time)
cuid: cm3crjc7o000009mkc6hih7ye
slug: lv1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731313612280/b865f950-4333-47d1-94ac-f3676cbd0300.png
tags: 7zse66gc6re4656y66i47iqk

---

# 문제

숫자로 이루어진 문자열 `t`와 `p`가 주어질 때, `t`에서 `p`와 길이가 같은 부분문자열 중에서, 이 부분문자열이 나타내는 수가 `p`가 나타내는 수보다 작거나 같은 것이 나오는 횟수를 return하는 함수 solution을 완성하세요.

예를 들어, `t`\="3141592"이고 `p`\="271" 인 경우, `t`의 길이가 3인 부분 문자열은 314, 141, 415, 159, 592입니다. 이 문자열이 나타내는 수 중 271보다 작거나 같은 수는 141, 159 2개 입니다.

---

### 제한사항

* 1 ≤ `p`의 길이 ≤ 18
    
* `p`의 길이 ≤ `t`의 길이 ≤ 10,000
    
* `t`와 `p`는 숫자로만 이루어진 문자열이며, 0으로 시작하지 않습니다.
    

---

### 입출력 예

| t | p | result |
| --- | --- | --- |
| "3141592" | "271" | 2 |
| "500220839878" | "7" | 8 |
| "10203" | "15" | 3 |

ㅤ

# 풀이

```jsx
function solution(t, p) {
    const arr = [];

    t.split("").map((str, index) => {
        let num = t.slice(index, index + p.length)
        if(num.length === p.length) {
            arr.push(Number(num))
        }
    })
    return arr.filter(num => num <= Number(p)).length;
}
```

* 문자열을 `map`을 사용하기 위해서 `split`으로 나누고 배열을 순회함 순회하면서 `p`의 길이씩 잘라서 배열 `arr`에 넣어주는데 `p`와 길이가 같은 것들만 넣어준다. 그리고 `p`보다 작거나 같은 것들을 `filter`로 담아서 `length`를 반환해줬다.
    
* 이렇게 `map`과 `filter`를 사용해서 문제를 풀었는데 제출하고 다른 분들 풀이를 보니 거의 다 `for`문으로 푸셨다🥹
    

### for문을 이용한 풀이

```jsx
function solution(t, p) {
    let count = 0;
    for(let i=0; i<=t.length-p.length; i++) {
        let value = t.slice(i, i+p.length);
        if(+p >= +value) count++;
    }
    return count;
}
```

* `for`문을 사용한 풀이는 루프를 돌면서 조건을 확인하면서 직접적으로 필요한 부분만 처리한다.
    
* `map`과 `filter`를 사용하니 추가적으로 배열을 생성하고 순회하기 때문에 불필요하게 처리하는 부분이 생기기 때문에 성능과 효율성이 떨어진다.
    
* `for`문으로 푼 풀이보다 내 풀이가 간결함과 가독성이 떨어진다.
    
* 결국 나는 문자열의 모든 요소를 돌면서 다 담아서 거기서 `filter`를 사용해서 또 걸러내는 방식으로 문제를 푼 건데 애초에 직접적으로 범위를 정하고 조건을 정해서 걸러내는 게 더 좋은 방법으로 보인다.
    

ㅤ