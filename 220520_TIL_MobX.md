# MobX에 대하여

## MobX란?

### 정의
- 전역 상태 라이브러리이다. 모든 상태변화가 일어나는 부분을 자동으로 추적해주는 역할을 한다.
- Redux와 또 다른 State관리 라이브러리
- 기본적으로 객체지향 느낌이 강하고, 번잡한 보일러플레이트 코드들을 데코레이터 제공으로 깔끔하게 해결한다.
- 보일러플레이트 코드란? 최소한의 변경으로 여러 곳에서 재사용되며, 반복적으로 비슷한 형태를 띄는 코드를 말한다. 이렇게 보면 마냥 좋다고 생각할 수 있다. 하지만 쉽게 말해서 반복적인 코드를 필요로 하고, 이것이 중복되어 많은 양의 코드를 양산하는 것, 즉 찍어내는 코드라고 이야기한다.
- MobX는 간단하고 확장 가능한 상태 관리 라이브러리를 모토로 삼고 있다. 즉, 유지보수가 쉬워지도록, 상태 관리의 단계를 간결하게 해 주도록 한다.

### MobX의 특징
- React의 종속적인 라이브러리가 아니다.
- 아키텍처나 상태 컨테이너가 아닌 라이브러리이다.
- redux와 다르게 store의 제한이 없다.
	- store란 프로젝트에redux를 적용하기 위해 필요한 것으로, 프로젝트에는 단 한 개의 store만 가질 수 있으며 상태(state)의 중앙 저장소라고 할 수 있다.
- observable을 기본적으로 사용하고, 절대적으로 필요한 경우에만 state를 변경한다.
	- observable이란 사전적으로는 '관찰할 수 있는'이라는 뜻을 가지고 있다. 즉, observable객체는 어떤 '객체'를 관찰할 수 있는 형태로 만드는 것을 말하며, 이 객체에 따라 실제 관찰하는 값(=스트림에 흘려 보내는 값) 혹은 관찰 대상인 사건(=이벤트)이 결정된다.
- MobX는 observable을 사용하면 properties, entire objects, arrays, Maps, Sets 등을 모두 자동으로 관찰 가능하게끔 만들 수 있다. 여기에 가장 중요한 어노테이션(annotation)으로는 몇가지가 있다.
	- observable: 추적 가능한 state 정의
	- action: state를 변경하는 메소드 표시
	- computed: state로부터 새로운 사실을 도출하고 그 결과값을 캐시하는 getter를 나타낸다.
- Typescript를 기반으로 만들어짐

### MobX 주요 요소
- state - 관찰 받고 있는 상태
	- 모델을 채우는 객체. 비객체, 원시, 참조의 그래프
	- 특정 부분이 바뀌면 MobX에서는 정확히 어떤 부분이 바뀌었는지 알 수 있다.
	- 이 state의 변화는 reaction과 computation을 일으킨다.
- Derivation(Computed values) - 파생 값(연산된 값)
	- Observable State의 변화에 따른 값
	- 기존의 상태값과 다른 연산된 값에 기반하여 만들어질 수 있는 값
	- 특정값을 연살할 떄에만 처리된다.
	- 어플리케이션으로부터 자동으로 계산될 수 있는 모든 값
	- observable로부터 도출할 수 있는 값이 변경되면 자동으로 업데이트
	- 성능 최적화를 위해 사용
- Reactions - 반응
	- Observable State의 변화에 따른 부가적인 변화
	- 값이 바뀜에 따라 해야 할 일을 정하는 것을 의미한다.
	- 파생 값과 비슷하지만  값을 생성하지 않는 함수
	- 적당할 때 자동으로 DOM이 업데이트 되거나 네트워크 요청을 하도록 만듦.
	- when, autorun, reaction
- Action: 액션 
	- Observable State, 사용자가 지정한 것을 포함한 모든 변경사항
	- 상태를 변경시키는 모든 것
	- MobX는 모든 사용자의 액션으로 발생하는 상태 변화들이 전부 자동으로 파생값(Derivation)과 리액션(Reactions)으로 처리되도록 함



	
## 예제

### MobX 설정
- 패키지 설치
```
$ npm install mobx mobx-react
```
- observable 파일 생성(위치는 /src/modules에 numberStore.jsx로 생성함)
```
import { observable } from 'mobx'

const NumberStore = observable({
	// state
	num: 0,
	
	// action
	increaseAction(num) {
		this.num = this.num + num;
	},
	decreaseAction(num) {
		this.num = this.num - num;
	}
});

export default NumberStore;
```
- 사용되는 observable 파일들을 묶어주는 파일 생성 (위치는 scr/modules에 indexStore.jsx로 생성함)
```
import numberStore from './numberStore';

const indexStore = () => ({
	numberStore,
	// store1,
	// store2, 
	// ...
});

export default indexStore;
```
- App.jsx에서 Mobx 사용
```
import * as React from 'react';
import { useObserver } from 'mobx-react';
import indexStore from './modules/indexStore';

const App = () => {
	const { numberStore } = indexStore();

	const onClickIncrease = () => {
		numberStore.increaseAction(3);
	}

	const onClickDecrease = () => {
		numberStore.decreaseAction(2);
	}

	return useObserver(() => (
		<div>
			<p>현재값: {numberStore.num}</p>

			<button onClick={onClickIncrease}>증가</button>
			<button onClick={onClickDecrease}>감소</button>
		</div>
	))
}

export default App;
```
- 실행시켜보면 증가버튼은 3증가, 감소버튼은 2감소되는 것이 실시간으로 화면에 보여진다.

### 다른 예제 - MobX를 이용한 React Component 구현하기
- App.js
```
import React, { Component } from 'react';
import Counter from './Counter';

class App extends Component {
  render() {
    return (
      <div>
        <Counter />
      </div>
    );
  }
}

export default App;
```
- Counter.js
```
import React, { Component } from 'react';
import { decorate, observable, action } from 'mobx';
import { observer } from 'mobx-react';

class Counter extends Component {
  number = 0;

  increase = () => {
    this.number++;
  }

  decrease = () => {
    this.number--;
  }

  render() {
    return (
      <div>
        <h1>{this.number}</h1>
        <button onClick={this.increase}>+1</button>
        <button onClick={this.decrease}>-1</button>
      </div>
    );
  }
}

decorate(Counter, {
  number: observable,
  increase: action,
  decrease: action
})

export default observer(Counter);
```
- 상단에 MobX 관련 기능을 선언한 후, 코드 하단 쪽에 decorate 함수를 호출한 부분이 있다.
- 해당 decorate가 Counter 컴포넌트에게 상태 변환을 할 수 있도록 도와주는 함수이다.
- decorate 각 파라미터 설명
	- 첫 번째 인자 : 상태와 연결할 컴포넌트
	- 두 번째 인자 : Object타입, Key는 상태로 적용할 변수명 및 함수명, Value쪽은 각 Key에 맞는 요소에 적용할 액션(ex- observable:상태 관찰 대상, action: 상태 관찰 대상을 변화시킬 액션)
- 마지막 줄의 observer는 observable로 선언한 상태 값(위 코드에서는 number값)이 변할 때, 컴포넌트 API인 forceUpdate()를 자동 호출하여 변경된 값이 화면에 반영된다.
- 

## MobX의 단점
- 디버깅 툴이 딱히 정해진 것이 없어서 state 추적이라도 해야하면 하나하나 콘솔에 찍어봐야 한다고 함.
- 프로젝트의 규모가 어느 정도 있고, state가 많이 자주 변하는 경우에는 쓰기가 어렵다.
- MobX가 Redux보다 코드가 적어지는 것은 사실이나, 보기 간단해지는 만큼 코드들을 체계적으로 분리하기 어렵다고 한다.

## MobX6의 특징
- 장점 중 하나였던 데코레이터를 사용하지 않는다.
- 데코레이터를 사용하지 않는 대신에 makeObservable이라는 기능을 추가하였다. 이는 constructor의 각 변수에 대해 observable인지 action인지 먼저 정의하는 기능이라 할 수 있다.
- inject를 사용하지 않는다. 대신 MobXProviderContext를 사용하여 좀 더 react hooks에 친화적으로 수정되었다.
