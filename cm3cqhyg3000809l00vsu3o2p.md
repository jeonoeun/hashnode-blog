---
title: "【프로그래머스】 Lv.0 qr code"
datePublished: Mon Nov 11 2024 08:00:59 GMT+0000 (Coordinated Universal Time)
cuid: cm3cqhyg3000809l00vsu3o2p
slug: lv0-qr-code
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731312239076/223ce918-4ee2-4aee-8d4f-00a1a8074799.png

---

# 문제

두 정수 `q`, `r`과 문자열 `code`가 주어질 때, `code`의 각 인덱스를 `q`로 나누었을 때 나머지가 `r`인 위치의 문자를 앞에서부터 순서대로 이어 붙인 문자열을 return 하는 solution 함수를 작성해 주세요.

---

### 제한사항

* 0 ≤ `r` &lt; `q` ≤ 20
    
* `r` &lt; `code`의 길이 ≤ 1,000
    
* `code`는 영소문자로만 이루어져 있습니다.
    

ㅤ

# 풀이

```jsx
function solution(q, r, code) {
    return code.split("").map((el, index) => index % q === r ? el : null).join("")
}
```

`map()` 함수에서 조건이 참이면(= 현재 인덱스를 `q`로 나눈 나머지가 `r`과 같다면)  
현재 요소인 `el`을 반환하고, 조건이 거짓이면 `null`을 반환한다.  
그리고 나서 `join()`을 사용해 문자열로 합친다.

ㅤ

* **다른 풀이**
    

```jsx
function solution(q, r, code) {
  return [...code].filter((_, i) => i % q === r).join('');
}
```

`filter`를 쓰면 되는데 왜 생각을 못했지...😳  
내가 푼 풀이는 `null`을 반환하게 될 경우 불필요한 요소가 남게 되기 때문에 `filter`를 사용해서 푸는 게 더 좋았을 것 같다.

ㅤ