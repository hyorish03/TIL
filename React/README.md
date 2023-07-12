## JSX란?

JSX는 자바스크립트의 확장 문법이다. 리액트는 이 JSX를 이용해서 화면에서 UI가 보이는 모습을 나타낸다.

```jsx
/* JavaScript */ /*       HTML      */ //js
const simple = <h1>Hello world!</h1>;
```

- JSX를 이용하면 UI를 나타낼 때 자바스크립트(login)과 HTML구조 (Markup)을 같이 사용할 수 있기 때문에 기본 UI에 데이터가 변하는 것들이나 이벤트들이 처리되는 부분을 더욱 쉽게 구현가능하다.

## 원래 리액트에서 화면을 그리는 방식

- React.createElement API를 사용해서 엘리먼트를 생성한 후 (객체가 된다) 이 엘리먼트를 In-Memory에 저장한다.
- 그리고 ReactDOM.render 함수를 사용해서 실제 웹 브라우저에 그려준다.

```jsx
//React.createElement를 이용해 엘리먼트 생성
const myelement = React.createElement('h1', {}, 'I do not use JSX');

//ReactDOM.render 함수를 사용해 실제 웹 브라우저에 그려준다.
ReactDOM.render(myelement, document.getElementById('root');
```

## JSX는 createElement를 쉽게 사용하기 위해 사용한다

- 모든 UI를 만들때마다 createElement를 사용해서 컴포넌트를 만들 수는 없다.
- 그렇기 때문에 JSX를 사용한 후 그걸 바벨이 다시 createElement로 바꿔서 사용한다

## JSX를 사용하면서 주의해야 할 문법들 (문법 규칙)

1. 만일 JSX 컴포넌트에 여러 엘리먼트 요소가 있다면 반드시 부모요소 하나로 감싸주어야 한다.

## JSX Key 속성이란?

- 리액트에서 요소의 리스트를 나열할 때는 Key를 넣어주여야 한다.
- 키는 React가 변경, 추가 또는 제거된 항목을 식별하는데에 도움이 된다.
- 요소에 안정적인 ID를 부여하려면 배열 내부의 요소에 키를 제공해야 한다.

예를들어 왼쪽의 list에서 오른쪽의 list로 변경된다면, 즉 3이 기존의 1, 2 뒤에 추가 된다면

React는 기존 list에서 3번만 추가하면 된다고 안다.

```jsx
<ul>
  <li>1</li>
  <li>2</li>
</ul>
```

```jsx
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ul>
```

그러나 왼쪽의 list에서 오른쪽의 list로 변경된다면, 즉 3이 기존의 1, 2 앞에 추가 된다면

React는 모든 요소가 새롭게 된거라 인식하고 모든 자식 엘리먼트를 새롭게 그려버린다.

```jsx
<ul>
  <li>1</li>
  <li>2</li>
</ul>
```

```jsx
<ul>
  <li>3</li>
  <li>1</li>
  <li>2</li>
</ul>
```

<aside>
💡 이런 경우 key를 추가해서 1, 2번을 새롭게 그리는 것이 아닌, 3번을 추가 후 1, 2번은 자리 이동을 해주면 된다.

</aside>

## State vs Props

### State

- 부모 컴포넌트에서 자녀 컴포넌트로 데이터를 보내는 것이 아닌 해당 컴포넌트 내부에서 데이터를 전달할 때 State를 이용한다.
  - 예를들어 검색 창에 글을 입력할 때 글이 변하는 것은 State을 바꾼다.
- State는 변경 가능하다
- State가 변하면 re-render 된다

```jsx
State = {
  message: " ",
  attachFile: undefined,
  openMenu: false,
};
```

### Props

- Properties의 줄임말이다.
- Props는 상속하는 부모 컴포넌트로부터 자녀 컴포넌트에 데이터등을 전달하는 방법이다.
- Props는 읽기 전용으로 자녀 컴포넌트 입장에서는 변하지 않는다. 변하게하고자 하면 부모 컴포넌트에서 state를 변경시켜주어야 한다.

```jsx
const [todoData, setTodoData] = useState([]);
<Lists todoData={todoData}/> // 이런식으로 props를 넘겨준다

//List.js
function List (todoData) {
	...
}
```

## 구조분해 할당

### 구조분해할당이란 ?

배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JS 표현식이다.

### 왜 사용 ?

Clean Code를 위해서 !!!

```jsx
let animalData = {
	accessory : 'horn',
	name : 'cuty',
	color : 'purple;
};

//구조분해할당 미사용시
function buildAnimal(animalData){
	let accessory = animalData.accessory
	let name = animalData.name
	let color = animalData.color
	...
}

//구조분해할당 사용시
function buildAnimal(animalData){
	let {accessory, name, color} = animalData;
}
```

리액트18 버전에서 라이브러리들을 설치할 때

종속성에 관한 에러가 날 때가 많이 있다.

_`npm ERR! **code ERESOLVE**`_

_`npm ERR! **ERESOLVE unable to resolve dependency tree**`_

_`npm ERR! **Found: react@18.1.0**`_

_`npm ERR! node_modules/react`_

_`npm ERR!  **react@"^18.1.0"** from the root project`_

_`npm ERR! **Could not resolve dependency:**`_

_`npm ERR! **peer react@"^17.0.1"** from react-dnd...`_

`[원인]`

unable to resolve dependency tree리액트 18 버전 라이브러리와 설치하려는 해당 라이브러리의 종속성이 안 맞기 때문이다.

`[해결 방법]`

이럴 때는 여러 가지 해결방법이 있는 데 첫 번째는 리액트 버전을 17로 낮추는 것인데 별로 좋은 방법은 아니다. 다른 방법은 npm 대신에 yarn을 이용해서 yarn install로 종속성을 설치해주는 방법이다. 만약 yarn으로 설치해도 안된다면 npm의 강제 설치 옵션으로 설치해주시면 된다.

- -legacy-peer-deps : 기존 버전 다 무시하고 일단 설치.
- -force : package-lock.json에 몇가지의 다른 의존 버전들을 추가하면서 설치.
