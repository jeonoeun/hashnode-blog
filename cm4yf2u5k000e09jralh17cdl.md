---
title: "[WEB] 🌎 주소창에 "www.naver.com"를 입력하면 어떤 일이 생길까?"
datePublished: Sat Dec 21 2024 16:51:56 GMT+0000 (Coordinated Universal Time)
cuid: cm4yf2u5k000e09jralh17cdl
slug: wwwnavercom
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734799013083/e1c711e5-2f5f-4d39-9041-e66e4aeb39a4.jpeg
tags: dom, 64sk7yq47jum7ygs, 67im65287jqw7kcaiougjounloungq

---

# 🌎 **브라우저 구조**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734800119706/c181ae09-8289-4647-9915-b05881885e5a.png align="center")

* **사용자 인터페이스**
    
    * 웹페이지 상단바에 위치한 뒤로가기, 앞으로가기, 새로고침 등등,말 그대로 사용자와 상호 작용하는 인터페이스를 뜻한다
        
* **브라우저 엔진**
    
    * 예를 들어, 사용자가 뒤로가기를 누르면 렌더링 엔진에게‘사용자가 뒤로가기를 눌렀으니 이전의 사이트를 가져와서 그려줘!’라고 알려주는 역할을 함
        
* **📌 렌더링 엔진**
    
    * 웹사이트를 그리는 엔진
        
* **통신**
    
    * 웹 브라우저의 네트워크를 담당
        
* **UI 백엔드**
    
    * 사용자 입력, 마우스 움직임, 클릭 등을 핸들링 하는 곳
        
* **자바스크립트 해석기**
    
    * JS코드를 해석할 때 사용하는 JS 엔진
        
* **자료 저장소**
    
    * 브라우저가 정보를 저장하는 곳으로 로컬스토리지, 세션스토리지 등이 여기 속한다
        

ㅤ

# 🌎 **주소창에 "**[**www.naver.com**](http://www.naver.com)**"를 입력하면 어떤 일이 생길까?**

## 1\. IP 주소 찾기

사실 `"www.naver.com"`라고 입력해도 브라우저는 읽지 못한다. 브라우저가 실제로 읽는 건 `IP` 주소이기 때문에 해당하는 `IP` 주소를 찾아야 한다.

그럼 `IP` 주소는 어떻게 찾을까?

> **DNS에게 찾아감(Domain Name System)www.naver.com에 해당하는 IP를 찾으면 DNS와 함께 IP에 맞는 IP 주소를 찾는다.**

이 과정이 복잡하기 때문에

> **DNS cache에 IP 주소를 저장해서 다음에는 거기에서 바로 가져온다.**

ㅤ

## 2\. 리소스 요청

### 1\. 캐릭터화

`IP` 주소를 찾고 나면 웹사이트를 그려야 한다. 이때, "서버야 나 웹사이트 그리고 싶은데 `HTML` 좀 보내줘"하고 서버에 요청하면 우리가 아는 `HTML` 형태의 파일을 주는 것이 아니라 바이트 스트림 형태로 주기 때문에 인코딩을 해야 한다.

* 보통 `UTF-8 Encoding` 같은 방식으로 인코딩을 한다.
    
* 우리가 보는 `HTML` 파일에 우리가 이 방식으로 인코딩 했다고 알려주는 것.
    

인코딩을 하고 나면 이렇게 **D**ocument 문서가 생긴다.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734800164853/6f8ae337-d967-4434-93c8-fca0bae4c7e3.png align="center")

### 2\. 토큰화

생성된 태그를 한글자 한글자 컴퓨터가 읽으면서 토큰을 만든다.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734800200615/71241ce2-905f-4e43-8101-256701e2c500.png align="center")

### 3\. 노드

토큰을 **O**bject의 객체 형태로 재해석한다.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734800212951/dbc7648f-f24f-4567-ba71-d7af43956b92.png align="center")

### **4\. DOM Tree**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734800231552/586ac090-766c-428b-b647-4e5d7706385a.png align="center")

최종적으로는 만들어진 객체들에 관계를 부여해야 한다. (HTML 태그의 부모 - 자식 관계)

Tree 형태로 관계를 주는 것을 **M**odel이라고 한다.

* **D**ocument 문서를
    
* **O**bject 객체 형태로 만들어서
    
* **M**odel 관계를 만든다
    

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><code>HTML</code>의 최종 목표는 이렇게 문서를 해석해서&nbsp;<strong>DOM Tree</strong>를 만드는 것!</div>
</div>

ㅤ

## **3\. Render Tree**

위 과정을 거쳐 불러온 `HTML`, `CSS`, `JS` 파일들을 **합체**해야 한다. 이 과정에서 쓸데없는 노드들을 제외한다.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><strong>이렇게 진짜로 웹사이트를 그리기 위한 최종 설계도를 그리는 것.</strong></div>
</div>

ㅤ

## 4\. 최종 그리기 단계

이제 진짜 웹사이트를 그리기만 하면 되는데 정확히 어디에다 그릴건지 정해야 한다. (반응형)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734800424107/df486021-0b6a-4bac-b502-f126620b7d89.png align="center")

* **Layout:** 정확한 `px`값을 계산하는 단계이다
    
* **Paint:** 여러개의 레이어로 나눠서 그림
    
* **Composite:** 여러개의 레이어를 마지막 단계에서 합쳐서 보여준다
    

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">이 구간은 우리가 웹사이트를 사용하면서 계속 반복되는(Reflow) 구간이기 때문에 <strong>최대한 덜 하는게 웹사이트 성능에 좋음.</strong></div>
</div>

* **Reflow 될 때**
    
    * 페이지 초기 렌더링 시(최초 `Layout` 과정)
        
    * 윈도우 리사이징 시(`Viewport` 크기 변경 시)
        
    * 노드 추가 또는 제거요소의 위치, 크기 변경(`left`, `top`, `margin`, `padding` 등등)
        
    * 폰트 변경(텍스트 내용)과 이미지 크기 변경(크기가 다른 이미지로 변경 시)
        

ㅤ

# \+ 더보기(리소스요청)

### **CSSOM Tree**

```xml
<link rel="stylesheet" type="text/css" href="/examples/media/expand_style.css">
```

`HTML` 파일을 읽다가 이렇게 `CSS` 명령어가 있으면 "서버야 아까 `HTML` 파일 보내준 거 보니까 `CSS` 파일도 필요하다 해서 그것도 보내줘~"라고 아까 주소에 다시 한번 요청한다.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">바이트 스트림 ⇒ 캐릭터화 ⇒ 토큰화 ⇒ 노드 ⇒&nbsp;<strong>CSSOM Tree</strong></div>
</div>

`CSS`도 `HTML`과 똑같이 위의 과정을 거치면 이런 형태의 **CSSOM Tree**가 생성된다.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1734800342928/ec01453f-ba46-4aab-9afd-84a30f8fdea9.png align="center")

ㅤ

### **JavaScript 파싱**

```xml
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="./style.css">
    <title></title>
</head>
<body>
    <script src="script.js"></script>
</body>
</html>
```

"서버야 읽다 보니까 `JS` 파일도 있네 이것도 보내줘!"하고 다시 요청을 한다. 이때 `HTML`은 자바스크립트 파일이 실행되는 동안에는 `DOM` 파싱을 멈춘다.

> * **왜 멈출까?**
>     
>     만약 DOM을 다 그렸는데 자바스크립트의 요청사항이 너무 많으면 그 요청사항에 따라 다시 또 그려야 한다. 그래서 일단 그리던 거 멈췄다가, JS파일을 다 읽고 요청사항에 맞게 다시 DOM 생성을 이어나간다.
>     

ㅤ

### **자바스크립트 태그가 항상 바닥에 있는 이유?**

```xml
<script src="main.js" defer></script>
<div id="test" class="test">hey</div>
```

예를 들어, JS 파일이 `<div id="test">`의 텍스트를 바꿔주세요라는 요청을 가진 파일인데 `<div id="test">`가 JS 파일보다 밑에 위치해 있으면 JS 파일이 요소를 알 수 없어서 에러가 발생한다. 따라서 `script` 태그가 `body` 태그 최하단에 위치해야 한다.

ㅤ

### **defer과 async**

```xml
<script src="main.js" defer></script>
<div id="test" class="test">hey</div>
```

근데 자바스크립트가 DOM 파일을 막는 건 말이 안되지 않니? 자바스크립트 읽는 동안 DOM 파싱 멈추는 거 싫다?

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><strong>그럴 경우,</strong>&nbsp;<code>defer</code><strong>이나</strong>&nbsp;<code>async</code><strong>를 사용하면</strong>&nbsp;<code>script</code>&nbsp;<strong>파일이</strong>&nbsp;<code>DOM</code><strong>의 생성을 막지 않는다.</strong></div>
</div>

ㅤ

### **근데 왜 CSS link 태그는 항상 위에 있는거야?**

`CSS`는 `DOM`의 생성을 막지 않음! `DOM`이 완성이 됐다고 바로 웹사이트에 보이는 것이 아니라 `CSSOM`을 기다렸다가 둘 다 완성이 되면 다음 스텝으로 진행한다.

그래서 `CSSOM`이 최대한 빨리 진행되는게 웹사이트 성능에 중요한 역할을 한다. 만약 `CSS` 파일이 너무 크면 `DOM`이 끝났어도 `CSSOM`이 끝나는 걸 계속 기다려야 하기 때문에 스타일 파일을 필요에 따라 나누는 게 웹성능을 높이는데 좋다.

ㅤ

# 🤔 그렇다면 웹사이트의 성능을 위해선 어떻게 해야할까?

* 소스(파일)의 사이즈 줄이기(바이트 수 줄이기)
    
* 외부에서 가져오는 리소스양 줄이기 - CSS 파일 같은 경우 Media Query 등을 써서 불필요한 파일은 나중에 가져오기
    
* 외부에서 가져오는 횟수 줄이기(인라인 스타일) - 장단점 있음
    
* Reflow, Repaint 줄이기(left, right 보다 transform 사용, 1px씩 보단 3px씩 등...)
    

ㅤ

# 🤨 강의 듣고 느낀 점

컴퓨터야.. 사이트 하나 읽기 위해서 생각보다 정말 많은 일을 하는구나. 그리고 지금까지 내가 짠 코드는 웹사이트 성능에 정말 안 좋았겠구나.. 앞으로 많이 고려하면서 코드를 짤 수 있도록 노력해야겠다.

ㅤ