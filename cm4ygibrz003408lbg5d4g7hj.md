---
title: "TIL 241221 | Firebase Authentication 에러"
datePublished: Sat Dec 21 2024 17:31:58 GMT+0000 (Coordinated Universal Time)
cuid: cm4ygibrz003408lbg5d4g7hj
slug: til-241221-firebase-authentication
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734801429689/f031bb3d-b2e8-4737-94c9-6f2e40010114.jpeg
tags: firebase, til

---

그날 그날 공부하거나 정리한 것을 노션에 기록하고 2차로 정리해서 블로그에 옮기는 식으로 하고 있었는데, 블로그에는 대단하고 영양가있는 글을 써야한다는 부담 때문에 계속해서 미루게 된다… 그래서 이제는 짧은 글이라도 배우고 느낀 것들을 블로그에 정리해보려고 한다!

### **문제상황**

이메일로 인증된 사용자의 기존 이메일을 바꾸는 작업을 하는데, `updateEmail`로 이메일을 변경할 때 다음과 같은 에러가 발생했다.

<div data-node-type="callout">
<div data-node-type="callout-emoji">🚨</div>
<div data-node-type="callout-text"><strong>FirebaseError: Firebase: Please verify the new email before changing email. (auth/operation-not-allowed).</strong></div>
</div>

### **해결**

* \*\*email enumeration protection(이메일 열거 보호)\*\*를 체크 해제 해주면 굉장히 쉽게 해결되는 문제였다.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734802195920/756cf237-043d-428c-a5d6-1db28993647a.png align="center")

### **느낀점**

* 스택오버플로어에 그대로 나와있는 에러였는데 검색도 안 해보고 계속 내 코드가 뭐가 잘못됐지… 고민하고 찾고 있었다. 검색을 생활화하자!
    

ㅤ