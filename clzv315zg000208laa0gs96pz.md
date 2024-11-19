---
title: "【프로그래머스】 Lv.0 최빈값 구하기"
datePublished: Thu Aug 15 2024 09:32:52 GMT+0000 (Coordinated Universal Time)
cuid: clzv315zg000208laa0gs96pz
slug: lv0
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723714196238/13760cfa-3447-43f4-9141-9f45399f574a.png

---

## 문제

최빈값은 주어진 값 중에서 가장 자주 나오는 값을 의미합니다. 정수 배열 `array`가 매개변수로 주어질 때, 최빈값을 return 하도록 solution 함수를 완성해보세요. 최빈값이 여러 개면 -1을 return 합니다.

(출처) [https://school.programmers.co.kr/learn/courses/30/lessons/120812](https://school.programmers.co.kr/learn/courses/30/lessons/120812)

---

#### **제한사항**

* 0 &lt; `array`의 길이 &lt; 100
    
* 0 ≤ `array`의 원소 &lt; 1000
    

---

#### **입출력 예**

| array | result |
| --- | --- |
| \[1, 2, 3, 3, 3, 4\] | 3 |
| \[1, 1, 2, 2\] | \-1 |
| \[1\] | 1 |

ㅤ

## 풀이

* 처음 제출 코드
    

```jsx
function solution(array) {
    let obj = {}

    array.forEach(num => {
        obj[String(num)] ? obj[String(num)] += 1 : obj[String(num)] = 1;
    })

    const arr = Object.values(obj);
    const max = Math.max(...arr);
    const count = arr.filter(x => x === max).length;
    const result = Object.keys(obj).find(key => obj[key] === max);

    return count > 1 ? -1 : Number(result);
}
```

주어진 배열에서 가장 빈도가 높은 숫자를 찾고, 그 숫자가 여러 개 존재하면 `-1`을 반환하는 로직을 구현하는 문제이다.

처음에는 객체의 키를 숫자 대신 문자열로 변환하여 저장하였는데 답을 제출하고 검색해보니 키 값을 숫자 그대로 사용해도 자바스크립트가 문자열로 자동 변환하기 때문에 굳이 문자열로 변환하는 것은 불필요한 부분이라고 생각해서 `obj[String(num)]`의 값을 업데이트 해주는 부분을 아래와 같이 고쳤다.

ㅤ

* 리팩토링 🛠️
    

```jsx
function solution(array) {
    let obj = {};

    array.forEach(num => {
        obj[num] = (obj[num] || 0) + 1;
    });

    const max = Math.max(...Object.values(obj));
    const count = Object.values(obj).filter(x => x === max).length;
    const result = Object.keys(obj).find(key => obj[key] === max);

    return count > 1 ? -1 : +result;
}
```

* `obj[num] = (obj[num] || 0) + 1;`
    
    * `obj[num]`이 이미 존재하면 그 값을 가져와서 `1`을 더한다.
        
    * `obj[num]`이 존재하지 않으면(`undefined`이면) 기본값인 `0`을 사용해서 `1`을 더한다.