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
- MobX는 observable을 사용하면 properties, entire objects, arrays, Maps, Sets 등을 모두 자동으로 관찰 가능하게끔 만들 수 있다. 여기에 가장 중요한 어노테이션(annotation)으로는 3가지가 있다.
	- observable: 추적 가능한 state 정의
	- action: state를 변경하는 메소드
	- computed: state와 캐시로부터 새로운 결과를 반환한다.
	
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


