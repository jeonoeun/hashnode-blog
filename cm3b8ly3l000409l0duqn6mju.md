---
title: "[Typescript] 유니온 타입으로 인덱스 오류 방지하기"
datePublished: Sun Nov 10 2024 06:52:25 GMT+0000 (Coordinated Universal Time)
cuid: cm3b8ly3l000409l0duqn6mju
slug: typescript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731307105689/523ede28-194f-4a44-93d4-2854604b9a94.png
tags: typescript

---

# 문제

```javascript
// socialLoginButton.tsx

interface Props {
  label: string;
}

const links = {
  kakao: "카카오",
  naver: "네이버",
  google: "구글",
};

export default function SocialoginButton({ label }: Props) {
  return (
    <button>
      <span>{links[label]}로 로그인</span>
    </button>
  );
}
```

`socialLoginButton` 컴포넌트를 만들던 중에 문자열로 받아온 `label`의 타입을 `string`으로 명시해주니까 다음과 같은 타입 에러가 발생했다.

<div data-node-type="callout">
<div data-node-type="callout-emoji">🚨</div>
<div data-node-type="callout-text">'string' 형식의 식을 '{ kakao: string; naver: string; google: string; }' 인덱스 형식에 사용할 수 없으므로 요소에 암시적으로 'any' 형식이 있습니다.</div>
</div>

ㅤ

**왜 이런 에러가 발생할까?**

* `label`로 `links` 객체에 접근할 때 `label`은 `"kakao"`, `"naver"`, `"google"` 중 하나여야 하지만, 현재 코드에서는 단순히 `string` 타입으로 명시하고 있기 때문에 생기는 에러이다.
    

ㅤ

# 해결

TypeScript에게 `label`이 **특정한 값만 가질 수 있다**는 것을 명확히 알려주면 된다. 유니온 타입, `keyof` 연산자 등을 활용해서 안전한 타입을 명시할 수 있다.

#### 1\. **유니온 타입 사용하기**

`label`을 **유니온 타입**으로 정의하면 TypeScript가 해당 값들이 반드시 `"kakao"`, `"naver"`, `"google"` 중 하나라고 정확하게 알 수 있게 된다.

```javascript
interface Props {
  label: "kakao" | "naver" | "google";
}
```

#### 2\. `keyof` 연산자 사용하기

TypeScript에서 `keyof` 연산자를 사용해서 `label`이 `links` 객체의 키 중 하나라는 것을 명시할 수도 있다.

```javascript
interface Props {
  label: keyof typeof links;
}
```

ㅤ