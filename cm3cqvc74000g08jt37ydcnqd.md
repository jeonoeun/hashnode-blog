---
title: "[React] TanStack Query 시작하기"
datePublished: Mon Nov 11 2024 08:11:23 GMT+0000 (Coordinated Universal Time)
cuid: cm3cqvc74000g08jt37ydcnqd
slug: react-query-tanstack-query
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731312500756/0bdfa7be-094a-48e2-9751-173a3508a84d.webp
tags: reactjs, react-query, tanstack-query

---

# TanStack Query(React Query)란?

`HTTP` 요청을 전송하고 프론트엔드 사용자 인터페이스를  
백엔드 데이터와 동기화된 상태로 유지하는데 이용하는 라이브러리이다.  
ㅤ

# TanStack Query를 사용하는 이유

* **refetch**
    
* **캐시 처리**
    
    * 가져온 데이터를 캐시 처리하고 메모리에 저장해 필요할 때 다시 사용한다.
        
    * 예를 들어, 다른 페이지로 이동한 후 다시 홈으로 갈 때 홈에서 필요한 모든 데이터를 다시 다 가져오는 게 아니라 메모리에 이미 저장된 데이터를 재사용해서 업데이트된 데이터만 자체적으로 가져온다.
        
* `TanStack Query`를 사용하는 가장 큰 이유는 **코드가 간소화되고 재사용하기 쉬워지기 때문이다.**
    

> 👀 이러한 섬세한 기능들이 사이트를 좀 더 효과적이고 사용자 친화적으로 만들어주기 때문에 사용하는 것!

ㅤ

# useQuery

* 서버로부터 데이터 가져올 때 사용한다.
    
* 이때 두 가지 `params`가 필수적으로 포함되어야 한다.
    

### 1\. queryFn

```jsx
useQuery({
		queryKey: ["events"],
    	queryFn: fetchEvents,
  })
```

* 실제 요청을 전송할 때 실행할 함수를 전달한다.
    
* `React Query`는 `HTTP` 요청을 하는 로직이 있는 것이 아니라 요청을 관리하는 로직을 제공한다.
    
* 그 로직은 요청과 관련한 데이터와 발생 가능한 오류를 추적하는 역할 등을 하기 때문에 `fetch`, `axios` 등의 방법으로 요청을 전송하는 코드는 직접 작성해야 한다.
    
* 반드시 요청을 전송해야하는 것은 아니고 프로미스를 반환하는 함수를 전송하면 된다.
    

### 2\. queryKey

```jsx
useQuery({
        queryKey: ["events", { max: 3 }],
  })
```

* 데이터 재사용에 필요한 식별자이다.
    
* 배열 형태로 저장하는데 여러 키값을 정할 수 있고 문자열 형태로만 특정되지 않고 객체, 이중 배열 등으로 설정할 수 있다.
    

ㅤ

# useQuery 실행

```jsx
const { data, isPending, isError, error } = useQuery({
    queryKey: ["events"],
    queryFn: fetchEvents,
  });
```

* `useQuery`를 요청하고 실행되면 객체를 얻는다. 객체 분해 구조 할당으로 제일 중요한 것을 받아올 수 있다.
    

> * `data` - fetch 함수를 통해 반환 받은 값
>     
> * `isPending` - 요청이 실행중인지 아닌지 확인
>     
> * `isError` - fetch 함수에서 throw error를 반환하면 isError가 true가 됨
>     
> * `error` - fetch 함수에서 호출된 error
>     

ㅤ

이렇게 설정을 하고 실행해보면 사이트를 벗어낫다가 다시 돌아올 때마다 `HTTP` 요청이 되는 것을 볼 수 있다 !

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731312606945/f493d783-f823-4e99-9183-9257d38731c6.png align="center")

ㅤ