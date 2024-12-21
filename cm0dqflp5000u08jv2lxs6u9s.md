---
title: "[프로그래머스] Lv.0 저주의 숫자 3"
datePublished: Wed Aug 28 2024 10:47:48 GMT+0000 (Coordinated Universal Time)
cuid: cm0dqflp5000u08jv2lxs6u9s
slug: lv0-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724841466974/21057b22-d393-4e83-b6f5-5a7bf7da0bee.png
tags: 7zse66gc6re4656y66i47iqk

---

# 문제

3x 마을 사람들은 3을 저주의 숫자라고 생각하기 때문에 3의 배수와 숫자 3을 사용하지 않습니다. 3x 마을 사람들의 숫자는 다음과 같습니다.

| 10진법 | 3x 마을에서 쓰는 숫자 | 10진법 | 3x 마을에서 쓰는 숫자 |
| --- | --- | --- | --- |
| 1 | 1 | 6 | 8 |
| 2 | 2 | 7 | 10 |
| 3 | 4 | 8 | 11 |
| 4 | 5 | 9 | 14 |
| 5 | 7 | 10 | 16 |

정수 `n`이 매개변수로 주어질 때, `n`을 3x 마을에서 사용하는 숫자로 바꿔 return하도록 solution 함수를 완성해주세요.

---

(출처) [https://school.programmers.co.kr/learn/courses/30/lessons/120871](https://school.programmers.co.kr/learn/courses/30/lessons/120871)

ㅤ

ㅤ

# 전체 코드

```jsx
function solution(n) {
    let i = 0;
    let res = 0;

    while (i < n) {
        res++;
        if (res % 3 === 0 || String(res).includes("3")) continue;
        i++;
    }

    return res;
}
```

* `while` 루프가 한 번 실행될 때마다 `res`는 무조건 1씩 증가한다.
    
* 그리고 나서 OR 연산자를 이용해 `res`가 3의 배수이거나 숫자 3을 포함하는지를 검사한다.
    
    * 만약 `res`가 3의 배수이거나 숫자 3을 포함하면, `continue` 문을 사용하여 `i++`를 건너뛰고 다음 루프로 넘어간다.
        
    * 그렇지 않으면, `i++`를 실행.
        
* 결과적으로, `res`는 루프가 한 번 실행될 때마다 항상 1씩 증가하지만, `i`는 조건을 만족할 때만 증가한다.
    

ㅤ

ㅤ