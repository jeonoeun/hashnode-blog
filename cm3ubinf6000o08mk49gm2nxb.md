---
title: "[React] 개념 정리"
datePublished: Sat Nov 23 2024 15:21:28 GMT+0000 (Coordinated Universal Time)
cuid: cm3ubinf6000o08mk49gm2nxb
slug: react
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1732375222985/54f42520-1d2c-4f82-a059-d3c0c9f7281e.png
tags: reactjs

---

> Next.js 공식 문서를 보면 **리액트 프레임워크(React Framework)**인 것을 알 수 있다. 그래서 Next.js를 배우기 전에 헷갈리거나 몰랐던 리액트 기본 지식을 간단히 정리해보려고 한다!

ㅤ

# React란?

* 사용자 인터페이스를 만들기 위한 자바스크립트 라이브러리이다.
    
* 리액트는 컴포넌트 기반이기 때문에, 리액트 앱을 빌드하는 것은, 곧 컴포넌트(`jsx`코드를 반환하는 함수)를 빌드하는 것과 같다.
    
* 컴포넌트 이름은 반드시 대문자로 작성해야 한다. 아니면 그냥 `HTML` 태그로 간주해버린다.
    

ㅤ

# React Hooks

### useState

* `state` 상태 값이 바뀔 때마다 컴포넌트가 재실행된다.
    

```jsx
  const [enterdBody, setEnteredBody] = useState();
```

### useEffect

* 무한 루프 방지
    

```jsx
  useEffect(() => {
    async function fetchPosts() {
      const response = await fetch("http://localhost:8080/posts");
      const resData = await response.json();
      setPosts(resData.posts);
    }

    fetchPosts();
  }, ["의존성 배열"]);
```

ㅤ

# Routing

### RootLayout

* 자식 요소(`children`)가 렌더링 될 위치는 `Outlet`으로 지정한다.
    

```jsx
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      {
        path: "/",
        element: <Posts />,
        loader: postsLoader,
        children: [
          { path: "/create-post", element: <NewPost />, action: newPostAction },
          { path: "/:id", element: <PostDetails />, loader: postDetailsLoader },
        ],
      },
    ],
  },
]);
```

```jsx
export default function RootLayout() {
  return (
    <>
      <MainHeader />
      <Outlet />
    </>
  );
}
```

### Link

* `Link`를 쓰면 새로고침 없이 페이지를 이동할 수 있다. (반대로 `a` 태그는 페이지를 새로고침해서 가져온다.)
    

```jsx
  <Link to="..">
    Cancel
  </Link>
```

### useNavigate

* 페이지 이동의 기능을 하는 리액트 훅.
    
* `navigate("..")`는 현재 페이지의 한개 상위 페이지로 이동한다는 뜻이다. 터미널 명령어 `cd ..` 와 같다.
    

```jsx
  const navigate = useNavigate();

  function closeHandler() {
    navigate("..");
  }
```

* 이때까지 모달창을 함수를 사용해서 `state` 상태 변경으로 열고 닫았는데 `router`를 사용하는 방법이 재사용하기 좋고, 불필요한 변수나 함수 사용이 적어서 더 좋아보인다. 참고해야겠다.💭ㅤ
    

> React Router v6.4부터 **Client Side Browser**을 제공하고 있다. 서버에 요청하지 않고 클라이언트 측에서 처리하기 때문에 속도 등 엄청난 이점이 있다.

### loader

* 데이터 가져오기
    
* `loader`의 호출 시점은 컴포넌트가 렌더링 되기 전이다.
    
* 컴포넌트 바깥에서 실행되기 때문에 컴포넌트에는 영향을 주지 않는다.
    

```jsx
export async function loader() {
  const response = await fetch("http://localhost:8080/posts");
  const resData = await response.json();
  return resData.posts;
}
```

* `loader` 함수가 반환한 값을 `useLoaderData()`를 이용해서 반환된 데이터를 사용할 수 있다.
    

```jsx
function PostDetails() {
  const post = useLoaderData();

  if (!post) {
    return (
      <Modal>
	      
      </Modal>
    );
  }
}

export default PostDetails;
```

### action

* 데이터 전송하기
    

```jsx
import { Form, Link, redirect } from "react-router-dom";

function NewPost() {
  return (
      <Form method="post" className={classes.form}>
        <p>
          <label htmlFor="body">Text</label>
          <textarea id="body" name="body" required rows={3} />
        </p>
      </Form>
    </Modal>
  );
}

export default NewPost;

export async function action({ request }) {
  const formData = await request.formData();
  const postData = Object.fromEntries(formData);
  await fetch("http://localhost:8080/posts", {
    method: "POST",
    body: JSON.stringify(postData),
    headers: { "Content-Type": "application/json" },
  });

  return redirect("/");
}
```

#### Form

* `form` 태그와 같이 특정 `url`에 데이터를 전송해서 처리하는데 `HTML form`은 서버 측에, `Form`은 클라이언트 측에 요청을 보낸다는 차이가 있다.
    
* 클라이언트 측에서 요청을 받으면 `action` 함수에서 처리하는데 `POST` 요청 시 호출된다.
    

#### formData

* `action` 함수에서 전달된 데이터를 받을 수 있다.
    

#### redirect

* `action` 함수가 끝나면 `redirect`로 지정된 페이지로 이동한다.
    

ㅤ