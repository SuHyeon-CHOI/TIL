# 자바스크립트 프로그래밍 요약정리

## 순서도 그리기
- 프로그래밍에서 가장 중요한 것은 코드를 작성하기 전에 올바른 순서도를 만드는 것이다. 한 번만으로는 순서도를 완성할 수 없고 코딩하면서 계속 수정해야 한다. 
	- 프로그램 절차의 수는 정해져 있어야 한다.
	- 각 절차는 항상 같은 내용이어야 한다.
	- 모든 가능성을 고려해야 한다.
	- 예시는 절차를 검증하는데 사용한다.
- 순서도 그릴 때 반드시 사용자의 이벤트(버튼 클릭, 입력창 글자 입력 등)가 필요한 곳에서 순서도를 끊어야 함.

## 대화 상자 띄우기
- prompt 대화 상자에 사용자가 입력한 메시지가 문자열 형태로 전달되고, 입력하지 않고 취소를 누르면 null이 전달된다.
- alert 단순한 알림창으로, 호출하면 확인을 누르기 전까지 다음 스크립트 실행이 중단된다. 디버깅 용도로 사용할 때에는 console.log를 사용한다.
- confirm 사용자에게 확인을 받을 때 사용한다. 사용자가 확인을 누르면 true가 전달되고, 취소를 누르면 false가 전달된다.

## HTML 태그 선택하기
- document.querySelector로는 하나의 태그만 선택할 수 있고, document.querySelectorAll로는 여러 개의 태그를 선택할 수 있다.
- 하나의 태그만 선택하고 싶을 때에는 id 속성(#아이디), 여러 개의 태그를 동시에 선택하고 싶을 때에는 class(.클래스)를 사용한다.
- 어떤 태그 안에 들어 있는 다른 태그 선택하려면 띄어쓰기를 하면 된다. 그러면 앞 선택자 안에 들어 있는 태그가 선택된다.

## 태그에 이벤트 달기
- 태그를 선택한 후에 addEventListener 메서드를 사용해 이벤트를 연결한다.
	- 태그.addEventListener('이벤트 이름', 리스너 함수);
- 리스너 함수의 매개변수로 event 객체를 제공하여 이벤트와 관련된 정보를 얻을 수 있다. 예를 들어 input 태그에 입력된 값을 가져오려면 event.target.value를 넣으면 된다.
	- const 리스너함수= (event) => {
		console.log(event.target.value);
	};
- 입력창에 입력된 값은 value 속성으로 가져온다. value에 값을 대입하면 대입한 값으로 변경된다.
	- 입력창.value // 입력창의 값을 가져옴
	- 입력창.value = 값 // 입력창에 값을 넣음
- 입력 태그(input, select, textarea 등)가 아닌 일반 태그들의 내부 값을 가져올 때에는 value가 아니라 textContent 속성을 사용한다.
- 입력창이나 버튼의 경우 focus 메서드를 호출하면 해단 태그가 하이라이트된다.

## 고차 함수 사용하기
- 함수를 호출할 때마다 반환 함수를 생성하는 함수를 고차 함수(high order function)라고 한다.
	- const func () => {
		return () => {
			console.log('hello');
		};
	};
- 반환된 함수는 다른 변수에 저장할 수 있고, 그 변수에 저장된 함수를 다시 호출할 수 있다.
	- const innerFunc = func();
	innerFunc(); // hello
- 반환하는 값을 바꾸고 싶을 때에는 매개변수를 사용한다.
	const func = (msg) => {
		return () => {
			console.log(msg);
		};
	};
- 화살표 함수 문법에 따라 함수의 본문에서 바로 반환되는 값이 있으면 {}와 return을 생략할 수 있다.
	const func = (msg) => {
		console.log(msg);
	};

## if문 중첩 제거하기
- if문이 중첩되면 코드파악이 힘들다. 
	- 공통된 절차를 각 분기점 내부에 넣는다.
	- 분기점에서 짧은 절차부터 실행하게 if문을 작성한다.
	- 짧은 절차가 끝나면 return(함수 내부의 경우)이나 break(for문 내부의 경우)로 중단한다.
	- else를 제거한다(이때 중첩 하나가 제거된다).
	- 다음 중첩된 분기점이 나올 때 위의 첫번째 항복부터 네번째 항목까지 반복한다.

## 무작위로 숫자 뽑기
- Math.random 메소드를 사용하면 무작위로 숫자가 뽑힌다. 단, 정수가 아니므로 Math.floor나 Math.ceil, Math.round 같은 메서드를 사용해 정수로 바꿔준다.

## 1부터 원하는 숫자까지 들어 있는 배열 만들기
- 반복문을 사용해 배열에 숫자를 push 하면 된다.
	const numbers = [];
	for (let n=1; n <= 숫자; n+=1) {
		numbers.push(n);
	}

## indexOf와 includes
- indexOf와 includes는 배열이나 문자열에 원하는 값이 들어 있는지 찾는 메서드.
- 원하는 값이 들어 있다면 해당 인덱스를 알려주고, 없다면 -1 반환

## forEach와 map
- forEach는 반복문 효과를 내는 배열의 매서드이다.
	const array = [1, 3, 5, 7];
	array,forEach((number, index) => {
		console.log(number, index);
	});
- map도 반복문 역할을 하지만 반환값이 있다는 점에서 forEach와 구분된다. map은 기존 배열의 요소를 일대일로 다른 값으로 바꾼다. 단, 기존 배열의 값이 바뀌는 것이 아닌 새로운 배열을 만든다.
	const array = [1, 3, 5, 7];
	const newArray = array.map((number, index) => {
		console.log(number, index);
		return number + 1;
	});
	console.log(array); // [1, 3, 5, 7]
	console.log(newArray); // [2, 4, 6, 8]

## document.createElement, document.createTextNode
- 각각 태그와 텍스트를 만드는 메서드이다. 단 다른 태그에 append나 appendChild하기 전까지는 화면에 보이지 않는다.

## appendChild와 append
- document.createElement, document.createTextNode로 만든 태그나 텍스트를 선택한 태그의 자식 태그로 넣는다.
- appendChild로는 하나만 넣을 수 있고, append를 사용하면 여러 개를 동시에 넣을 수 있다.
- append로 텍스트를 추가할 때는 document.createTextNode대신 문자열을 바로 넣어도 된다.

## 피셔-예이츠 셔플 알고리즘
- 숫자를 무작위로 섞는 방법이다. 먼저 무작위 인덱스를 하나 뽑은 후, 그에 해당되는 요소를 새로운 배열로 옮긴다. 이를 반복하다 보면 새 배열에 무작위로 섞인 숫자들이 들어간다.

## sort
- 비교 함수에 적힌 내용대로 배열을 정렬하는 메서드.
	배열.sort(비교함수);

## setTimeout
- 지정한 시간(밀리초) 뒤에 지정한 작업을 수행하는 타이머
	setTimeout(() =>
		// 내용
	}, 밀리초);

## 스코프
- var는 함수 스코프를, let은 블록 스코프를 가진다.
- 함수, if문, for문에서 접근 범위의 차이를 보인다.
- 또한 let을 사용할 때는 for문 안에서 let 변수의 값이 고정되므로 var와는 실행결과가 달라진다.

## setLinterval
- setTimeout과 비슷한 효과를 내나, 한 번만 실행되는 setTimeout과는 달리 지정한 시간마다 주기적으로 지정한 함수를 실행한다.
	setInterval (() => {
		// 내용
	}, 밀리초);

## clearInterval, clearTimeout
- setInterval과 setTimeout 함수는 각각 clearInterval과 clearTimeout 함수로 취소 가능. 
- 단 clearTimeout은 setTimeout에 지정한 함수가 아직 실행되지 않았을 때만 취소 가능

## 배열.includes
- ||을 사용한 코드는 배열의 includes 메서드로 반복을 줄일 수 있다.

## removeEventListener
- addEventListener로 연결한 함수를 지울 수 있다.
- 단, 연결할 때의 함수와 제거할 때의 함수가 같아야 한다.

오늘은 여기까지!
