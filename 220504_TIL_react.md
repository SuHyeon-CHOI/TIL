# 리액트를 다루는 기술 1

## JSX
- JSX는 자바스크립트의 확장 문법이며 XML와 매우 비슷하게 생겼다.
- 브라우저에서 실행되기 전에 코드가 번들링되는 과정에서 바벨을 사용하여 자바스크립트 형태릐 코드로 변환된다.
- 예제코드
```javascript
function App() {
	return (
		<div>
			hello <b>react</b>
		</div>
	);
}
변환되는 코드
function App(){
	return.React.createElement("div", null, "Hello", React.createElement("b", null, "react"));
}
```
- 매번 React.createElement 함수 사용한다면 불편하니 JSX를 사용하여 매우 편하게 UI를 렌더링할 수 있다.

## JSX의 장점
- 보기 쉽고 익숙하다.
- 활용도가 높다.
```javascript
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(
	<React.StrictMode>
		<App />
	</React.StrictMode>,
	document.getElementById('root')
);
```

## JSX 문법
- 감싸인 요소
	- 컴포넌트에 여러 요소가 있다면 반드시 부모 요소 하나로 감싸야 한다.
```javascript
function App() {
	return(
		<div>
			<h1>리액트 안녕!</h1>
			<h2>잘 작동하니?</h2>
		</div>
	);
}

export default App;
```
- 자바스크립틑 표현
	- JSX 안에서는 자바스크립트 표현식 작성 가능. 작셩하려면 JSX 내부에서 코드를 {}로 감싸면 된다.
```javascript
function App() {
	const name = '리액트';
	return (
		<>
			<h1{name} 안녕!</h1>
			<h2>잘 작동하니?</h2>
		</>
	);
}

export default App;
```
- If문 대신 조건부 연산자
	- JSX 내무의 자바스크립트 표현식에서 if 문을 사용할 수는 없다. 
	- 하지만 조건에 따라 다른 내용을 렌더링해야 할 때에는 JSX 밖에서 if문을 사용하여 사전에 값을 설정하거나, {}안에 조건부 연산자(=삼항 연산자)를 사용하면 된다.
```javascript
function App() {
	const name = '리액트';
	return (
		<div>
			{name === '리액트' ? (
				<h1>리액트입니다.</h1>
			) : (
				<h2>리액트가 아닙니다.</h2>
			)}
		</div>
	);
}

export default App;
```

## AND 연산자(&&)를 이용한 조건부 렌더링
- 개발 도중 특정 조건 만족하면 내용을 보여주고, 만족하지 않으면 아예 아무것도 렌더링하지 않아야 하는 상황이 올 수 있다.
- 조건부 연산자를 사용하면 구현 가능하다.
```javascript
function App() {
	const name = '뤼왝트';
	return <div>{name === '리액트' ? <h1>리액트입니다.</h1> : null}</div>;
}

export default App;
```
- 위 코드와 같이 null을 렌더링하면 아무것도 보여주지 않는다
- && 연산자를 사용하여 조건부 렌더링을 짧은 코드로 구현 가능하다.
```javascript
function App() {
	const name = '뤼왝트';
	return <div>{name === '리액트' && <h1>리액트입니다.</h1>}</div>;
}

export default App;
```

## undefined를 렌더링하지 않기
- 리액트 컴포넌트에서는 함수에서 undefined만 반환하여 렌더링하는 상황을 만들면 안 된다.
- 반면 JSX 내부에서 undefined를 렌더링 하는 것은 괜찮다.

## 인라인 스타일링
- 리액트에서 DOM 요소에 스타일을 적용할 때는 문자열 형태로 넣는 것이 아니라 객체 형태로 넣어주어야 한다.
- 스타일 이름 중에서 background-color처럼 -이 포함되어 있는 이름은 카멜표기법으로 작성해야 한다.
```javascript
function App() {
	const name = '리액트';
	const style = {
		backgroundColor: 'black',
		color: 'aqua',
		fontSize: '48px',
		fontWeight: 'bold',
		padding: 16px
	};
	return <div style={style}>{name} </div>
}

export default App;
```

