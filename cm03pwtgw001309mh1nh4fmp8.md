---
title: "[프로그래머스] Lv.0 유한소수 판별하기"
datePublished: Wed Aug 21 2024 10:35:30 GMT+0000 (Coordinated Universal Time)
cuid: cm03pwtgw001309mh1nh4fmp8
slug: lv0-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724236399012/d1febd43-3392-4764-8296-83735c375883.png
tags: 7zse66gc6re4656y66i47iqk

---

# 문제

소수점 아래 숫자가 계속되지 않고 유한개인 소수를 유한소수라고 합니다. 분수를 소수로 고칠 때 유한소수로 나타낼 수 있는 분수인지 판별하려고 합니다. 유한소수가 되기 위한 분수의 조건은 다음과 같습니다.

* 기약분수로 나타내었을 때, 분모의 소인수가 2와 5만 존재해야 합니다.
    

두 정수 `a`와 `b`가 매개변수로 주어질 때, a/b가 유한소수이면 1을, 무한소수라면 2를 return하도록 solution 함수를 완성해주세요.

(출처) [https://school.programmers.co.kr/learn/courses/30/lessons/120878](https://school.programmers.co.kr/learn/courses/30/lessons/120878)

---

# 전체 코드

```javascript
// 최대공약수
function getGCD (num1, num2) {
    let gcd = 1;

    for(let i = 2; i <= Math.min(num1, num2); i++){
        if(num1 % i === 0 && num2 % i === 0){
            gcd = i;
        }
    }

    return gcd;
}

// 소인수분해
function getPrimeFactors(n) {
    let arr = [];

    for (let i = 2; i <= n; i++) {
        while (n % i === 0) {
            arr.push(i);
            n /= i;
        }
    }

    return arr;
}

function solution(a, b) {
    let gcd = getGCD(a, b)
    b = b / gcd

    let arr = getPrimeFactors(b)

    // 2와 5만 포함하고 있는지 확인
    if(arr.every(factor => factor === 2 || factor === 5)) return 1;
    else return 2;
}
```

`a`와 `b`의 **최대공약수(GCD)를 계산하고,** `b`를 그 GCD로 나눈다. 나눈 결과의 소인수들이 `2`와 `5`로만 구성되어 있는지를 확인해서\*\*(= 유한소수인지 확인)\*\* 조건이 맞으면 `1`을, 그렇지 않으면 `2`를 반환한다.

ㅤ

1. **최대공약수(GCD) 구하기(**`getGCD` **함수):**
    

```javascript
function getGCD(num1, num2) {
    let gcd = 1;

    for (let i = 2; i <= Math.min(num1, num2); i++) {
        if (num1 % i === 0 && num2 % i === 0) {
            gcd = i;
        }
    }

    return gcd;
}
```

* `2`부터 `num1`과 `num2` 중 더 작은 수까지 반복하며, 두 수 모두를 나눌 수 있는 가장 큰 숫자를 찾는다.
    
* `gcd` 변수의 초기값은 `1`이고, `for`문을 통해 공약수를 찾을 때마다 `gcd`의 값을 업데이트한다.
    

ㅤ

* **(참고) 유클리드 호제법**
    
    최대공약수를 구하는 알고리즘으로 유클리드 호제법을 사용하는 방법도 있다.
    
    ```javascript
    function getGCD(num1, num2) {
        while (num2 !== 0) { 
            let temp = num2;  
            num2 = num1 % num2;  
            num1 = temp;  
        }
        return num1;
    }
    ```
    
    ㅤ
    

2. **소인수분해 (**`getPrimeFactors` **함수):**
    

```javascript
function getPrimeFactors(n) {
    let arr = [];

    for (let i = 2; i <= n; i++) {
        while (n % i === 0) {
            arr.push(i);
            n /= i;
        }
    }

    return arr;
}
```

* `2`부터 시작하여 `n`을 나눌 수 있는 소수들을 찾고, 나눌 때마다 해당 소수를 `arr` 배열에 추가한다.
    
* 나눈 후 `n`의 값을 업데이트하고, `n`이 더 이상 `i`로 나누어지지 않을 때까지 반복한다.
    
* 최종적으로 `arr`에는 `n`의 소인수들이 포함된다.
    

ㅤ

3. `solution` **함수:**
    

```javascript
function solution(a, b) {
    let gcd = getGCD(a, b);
    b = b / gcd;

    let arr = getPrimeFactors(b);

    // 2와 5만 포함하고 있는지 확인
    if (arr.every(factor => factor === 2 || factor === 5)) return 1;
    else return 2;
}
```

* `getGCD` 함수를 사용해 두 수의 최대공약수를 구하고, `b`를 그 최대공약수로 나눈다.
    
* `getPrimeFactors` 함수를 사용하여 소인수분해 한다.
    
* `b`의 소인수들이 `2`와 `5`로만 구성되어 있는지 확인하기 위해 `every` 메서드를 사용한다.
    
* 소인수들이 모두 `2` 또는 `5`라면 `1`을 반환하고, 그렇지 않으면 `2`를 반환한다.
    

ㅤ

### References

* [JavaScript 최소공배수 & 최대공약수 구하기 by zwundzwzig님](https://velog.io/@amoeba25/JavaScript-%EC%B5%9C%EC%86%8C%EA%B3%B5%EB%B0%B0%EC%88%98-%EC%B5%9C%EB%8C%80%EA%B3%B5%EC%95%BD%EC%88%98-%EA%B5%AC%ED%95%98%EA%B8%B0)