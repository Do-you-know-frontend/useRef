# useRef

`useRef`는 **저장공간 또는 DOM요소에 접근하기 위해 사용되는 React Hook**이다

우리가 자바스크립트를 사용 할 때에는, 우리가 특정 `DOM` 을 선택하기 위해서 `querySelector` 등의 함수를 사용한다.
React를 사용하는 프로젝트에서도 가끔씩 `DOM` 을 직접 선택해야 하는 상황이 필요하다. 그럴때 우리는 `useRef`라는 React Hook을 사용한다.

 

## 언제 사용할까?

### 저장공간 (변수 관리)

`ref`안에 있는 값을 아무리 변경해도 컴포넌트는 다시 렌더링 되지 않는다.

`state` 대신 `ref`를 사용한다면 **불필요한 렌더링**을 막을 수 있다. 

컴포넌트가 아무리 렌더링이 되어도 `ref` 안에 저장되어 있는 값은 변화되지 않고 유지가 된다.

변경시 렌더링을 발생시키지 말아야 하는 값을 다룰 때 정말 편리하다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b6886783-b2f2-40ca-93eb-0163ebeb2cf3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230117%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230117T105049Z&X-Amz-Expires=86400&X-Amz-Signature=8b222329c8ea84d20df420c0d8766ce8deb7c2db88fe7a931b3cb184b0d2add7&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

**useRef로 관리하는 값은 값이 변해도 화면이 렌더링되지 않는다.**

- `setTimeout`, `setInterval`을 통해 만들어진 id
- `scroll` 위치 기억하고 싶을때
- 배열에 새 항목을 추가할 때 필요한 고유값 `key`

**우리가 컴포넌트 별로 특정 데이터를 가지게 하고, 이러한 데이터들을 리렌더링 없이 관리하고 싶다면 `useRef`를 사용한다면 가능하다.**

### Dom 요소에 접근할 때

대표적으로 input 요소를 클릭하지 않고 **포커스**를 주고 싶을 때 많이 사용한다.

```jsx
const App = () => {
  const inputRef = React.useRef();
  React.useEffect(()=>{
    inputRef.current.focus();
  })
  return (
    <>
      <div className="App">
        <input type="text" ref={inputRef} />
      </div>
    </>
  );
};
```

> 💡 주의
> 
> 
> `useRef`를 사용할 때 주의해야 할 점이 있는데, 바로 **`current**` 속성을 사용해야 한다. 이는 우리가 선택하고자 하는 `DOM`을 가리킨다고 보면 된다.
> 

> 🤔 의문
> 
> 
> `document` 객체로 접근하면 간단하게 접근할 수 있는데 리액트에서는 굳이 `useRef`를 제공하는 이유는 무엇일까?
> 

그 이유는 **효율성** 때문이다.

`document` 객체를 사용해서 `DOM`에 직접적으로 도달하게 되면 비효율적인 상황이 발생할 수 있다.

리액트에서는 컴포넌트의 상태 안에서 특정 변수로 라이프 사이클과는 **독립적이고 최적화된 상태**로 사용하고 싶은 저장 공간을 제공한다.

# References
[useState/useRef 와 setTimeout/setInterval](https://microcephalus7.github.io/react/js/377/)

[useRef와 폼 그리고 에러 경계](https://velog.io/@dev0408/get-to-know-react-5)
