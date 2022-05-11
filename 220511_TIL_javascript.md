# 초보자를 위한 자바스크립트 200제

## 16. 숫자형 이해하기
- 자바스크립트는 다른 프로그래밍 언어와 달리 숫자의 형태를 구체적으로 나눠 정의하지 않는다.
- 정수, 부동 소수점, 작은 수, 큰 수 등 여러 유형의 숫자를 숫자형(Number)하나로 정의한다.
- 이외에도 자바스크립트에는 Infinity, NaN 값이 있다. 숫자형으로 분류되지만, 일반적인 숫자와는 조금 다른 역할을 수행한다.
- Infinity는 다른 어떤 수보다 가장 큰 수를 뜻한다.
- NaN이란 'Not a number"라는 뜻으로, 산술 연산의 결과가 유효하지 않은 값 또는 숫자가 너무 커서 표현할 수 없는 값일 때 NaN으로 표현된다.

## 17. 문자형 이해하기
- 문자형(String)은 값이 텍스트 형태인 데이터를 의미한다.
- 문자열로 표현할 때에는 큰따옴표("), 작은따옴표('), 억음 부호(`)와 함께 사용한다.
- 처음과 끝의 기호는 동일해야 한다.
- 개행이 필요한 문장에는 \n을 추가하면 개행이 가능하다.

## 18. 불린형 이해하기
- 불린형(Boolean)은 참(true)와 거짓(false) 값으로 이루어진 자료형이다.

## 19. null과 undefined 기이해하기
- null은 비어 있는, 존재하지 않는 값을 의미한다. 즉, 값의 부재를 의미하며, 원시 자료형 null로 분류된다.
- 단, typeof로 자료형을 확인할 때 object(객체)를 반환하는데, 이는 자바스크립트 기존 이슈로 인한 결과이다. 이를 통해 null이 객체형이라 오해하지 않도록 주의할 필요가 있다.
- undefined는 변수가 정의되었지만, 아무 값도 할당받지 않은 상태를 의미한다.
- 예를 들어, 함수에서 명시적으로 값을 반환하지 않았을 때 또는 변수에 어떠한 값도 대입하지 않고 정의했을 때 undefined가 반환된다.
- 동등 연산자 ==인 경우에는 자료형 비교까지 이루어지지 않기 때문에 true를 반환한다. 
- 반면 자료형 변환이 없는 엄격한 일치 연산자 ===로 확인하면, null과 undefined의 자료형이 다르기 때문에 false가 반환되는 것을 볼 수 있다.

## 20. 템플릿 문자열 이해하기
```
var cart = [
	{name: '옷', price: 2000},
	{name: '가방', price: 1000}
];
var numOfItems = '카트에 ${cart.length}개의 아이템이 있습니다';
var cartTable = 
'<ul>
	<li>품목: ${cart[0].name}, 가격: ${cart[0].price}</li>
	<li>품목: ${cart[1].name}, 가격: ${cart[1].price}</li>
</ul>'
console.log(numOfItems); 
console.log(cartTable);

var personName = 'harin';
var helloString = 'hello' + personName;
var helloTemplateString = 'hello ${personName}';
console.log(helloString === helloTemplateString);
console.log(typeof helloTemplateString);

result:
	카트에 2개의 아이템이 있습니다
	<ul>
		<li>품목: 옷, 가격:2000</li>
		<li>품목: 가방, 가격:1000</li>
	</ul>
	true
	string
```

## 21. 산술 연산자
- 자바스크립트의 산술 연산자에는 표준 산술 연산자(덧셈, 뺄셈, 곱셈, 나눗셈)가 있다. 
- 덧셈(+) 연산자인 경우 문자형에 사용 가능하며, 이때는 두 개 이상의 문자열을 이어 붙일 수 있다.
- 산술 연산자에 = 연산자를 함께 사용하는 산술 등호 연산도 가능하다.
- 이 외에도 나머지 연산자(%), 거듭제곱 연산자(**), 단항음수/양수(+/-), 증감 연산자(++/--)가 있다.

## 22. 비교 연산자
- 비교 연산자는 두 개의 값을 비교하여 true와 false 결과값을 반환한다.
- 비교 연산자의 종류에는 값이 동등한지 비교하는 일치 연산자와 값의 관계를 비교하는 관계 연산자가 있다.
- 일치 연산자는 값의 일치 여부를 확인하며, 종류에는 동등 연산자, 부등 연산자, 일치 연산자, 불일치 연산자가 있다.
- 동등 연산자 ==는 비교 대상값의 자료형이 서로 다르면 강제로 형을 바꾼 뒤에 비교한다. 이때는 값의 자료형과 상관없이, 내용이 같은 경우 참(true)을 반환한다.
- 부등 연산자 !=는 값이 다른 경우 참(true)을 반환한다. 자료형이 다른 경우 동등 연산자와 동일하게 형을 변환하고 비교하게 된다.
- 일치 연산자 ===는 엄격한 기준을 가지고 있다. 값의 내용을 비교하는 것뿐만 아니라, 자료형까지 일치하는지 비교한다.
- 불일치 연산자 !==는 엄격한 기준으로 값의 불일치 여부를 확인하는 연산자이다. 같은 자료형에서 값의 내용이 다르거나 다른 자료형인 경우 참(true)을 반환한다.
- 관계 연산자는 두 개의 값 간의 크기 비교를 통해 관계를 확인하는 연산자이다. 관계 연산자에는 >, <, >=, <=가 있다.
- 자바스크립트는 숫자형 비교외 문자형에서도 비교 연산이 가능하다. 

## 23. 논리 연산자
- 논리 연산자(Logical Operator)는 어떠한 명제에 대한 논리적인 판단을 내리는 연산자이다. 참 또는 거짓의 값을 받아 논리적 연산의 결과로 true, false를 반환한다.
- 연산자 종류로는 AND 연산자 &&, OR 연산자 ||, NOT 연산자 !가 있고, 결과값은 항상 불리언(Boolean) 자료형으로 반환한다.

## 24. 삼항 연산자
- 삼항 연산자는 if와 switch처럼 조건문을 처리하는 연산자이다. 일반적으로 if 조건문의 축약형으로 사용되며, 세 개의 문장으로 구성된다.
- 조건문 ? 표현문 1 : 표현문 2
- 조건문의 결과가 true이면 표현문 1을 실행하고, false이면 표현문 2를 실행한다.
- 삼항 연산의 결과로 반환된 값은 다시 변수로 할당할 수 있다.

## 25. 비트 연산자
- 비트(Bit)란 이진수의 줄임말로, 0과 1로 구성된 숫자 체계를 갖고 있는 이진수의 단일 값을 가진다.
- 비트는 바이트(Byte)와 같이 자주 언급되는 용어로, 바이트는 컴퓨터 용량의 기본 단위로, 비트는 데이터의 가장 작은 기억장치의 최소 단위이다.
- 자바스크립트의 비트 연산자는 크게 비트 논리 연산자와 비트 이동 연산자로 나뉜다.
- 비트 논리 연산자로는 AND 연산자&, NOT 연산자 ~, OR 연산자 |,  XOR 연산자 ^가 있다.
- 비트 이동 연산자에는 <<, >>, >>>가 있다.

## 26. 자료형 변환 이해하기
- 자바스크립트에서는 자료형 간 변환을 지원한다.
- 예를 들어, 숫자형 변수값을 문자형으로 변환하거나, 문자형 변수값을 숫자형으로 변환할 수 있는데, 자바스크립트에서는 이를 자료형 변환(type coercion) 또는 형변환이라고 한다.
- 자료형을 변환하기 위한 방법으로는 두 가지가 있다.
	- 개발자가 직접 명시적으로 자료형을 변환한다.
	- 자바스크립트 엔진에 의해 자동으로 자료형이 변환된다.
- 특히 엔진에 의해 자동으로 자료형이 변환되는 것은 자바스크립트가 동적 자료형 언어이기 때문에 적용되는 특징이다.

## 27. 배열 이해하기
- 배열 자료형의 형태는 대괄호[]와 괄호 사이의 요소(들)로 구성된다.
- 요소가 없는 대괄호 []는 빈 배열을 의미한다.
- 배열에 요소들을 나열하는 경우 콤마(,)를 통해 구분한다.
- 자바스크립트는 동적 자료형 성격을 갖고 있기 때문에, 배열의 길이와 자료형은 고정되지 않는다.
- 배열 내무의 특정 위치에 있는 요소로 바로 접근할 때에는 인덱스(Index)가 반드시 필요하다. 인덱스란, 배열 안에 위치한 요소의 좌표라고 할 수 있는데, 좌표의 원점이 되는 시작값은 숫자 0이다.

## 28. 객체 이해하기 (1)
- 객체(Object)는 값들을 그룹으로 묶은 데이터 모음이다. 객체를 만드는 방법은 표현식으로 중괄호{}를 사용하면 된다.
- 중괄호 안에 여러 값들을 넣을 수 있는데, 키(Key)와 값(Value)을 한 쌍으로 정의하며 이를 속성(Properties)이라 부른다.
- {Key : Value}
- 하나의 키에는 하나의 값이 매핑된다. 
- 객체 안에 중복된 키 이름은 허용하지 않으며, 두 줄 이상의 속성을 정의할 때는 콤마, 를 사용하여 구분한다. 이 경우 가독성을 위해 각 속성 앞에는 들여쓰기를 하고 끝나는 지점에는 콤마를 두는 것을 권장한다.
```
var family = {
	'address' : 'Seoul',
	members: {}, 
	addFamily: function(age, name, role) {
		this.members[role] = {
			age : age,
			name : name
		};
	},
	getHeadcount: function() {
		return Object.keys(this.members).length;
	}
};
family.addFamily(30, 'chloe', 'aunt');
family.addFamily(3, 'lyn', 'niece');
family.addFamily(10, 'dangdangi', 'dog');
console.log(family.getHeadcount());
```
- 객체는 다양한 원시 자료형의 값을 가질 수 있고, 객체 속성으로 또다른 객체와 함수 리터럴을 가질 수 있다.
- JSON(JavaScript Object Notation)은 자바스크립트의 객체와 매우 유사한 구조를 지닌 데이터 교환 형식(format)이다. JSON 형태는 객체와 비슷하게 키 : 값 쌍의 모음들로 이루어져 있다. 그러나 반드시 속성 키 이름은 큰 따옴표""로 표시된 문자열이어야 하고, 값은 오직 문자열, 숫자, 배열, true, false, null 또는 다른 JSON 객체만 가능하다.
- {"Key" : value}
- 이처럼 객체와 JSON의 형태는 비슷해 보여도 동일하지 않다.

## 29. 객체 이해하기 (2)
```
var family = {
	'address' : 'Seoul',
	members: {},
	addFamily: function(age, name, role) {
		this.members[role] = {
			age: age,
			name: name
		};
	},
	getHeadcount: function() {
		return Object.keys(this.members).length;
	}
};

family.addFamily(30, 'chloe', 'aunt');
family.addFamily(3, 'lyn', 'niece');
family.addFamily(10, 'dangdangi', 'dog');

var printMembers = function() {
	var members = family.members;
	for (role in members) {
		console.log('role => ' + role + ', name=> ' + members[role].name + ', age => ' + members[role].age);
	}
};
printMembers();

var members = family.members;
members['nephew'] = {age: 3, name: 'hyun'};
members.niece = {age: 5, name: 'lyn'};
delete members.aunt;
delete members['dog'];
printMembers();
```
- 객체의 속성에 접근하는 방법은 객체의 우측에 콤마, 를 두고 그 다음에 객체 속성으로 정의된 키 이름을 작성하면 된다. 또는 대괄호[]안에 키 값을 문자열로 작성하는 방법도 있으나, 콤마로 속성에 접근하는 것이 선호되는 방식이다.
- 그 외에 객체에 속성을 추가/수정/삭제하는 방법 또한, 결국에는 속성에 접근하기 때문에 콤마, 또는 대괄호[]를 사용하는 방식과 유사하다.

## 34. 함수 이해하기
- 함수 형태를 표현하면 크게 네 가지로 구분된다.
	- 키워드
	- 함수 이름
	- 매개변수 목록
	- 함수 실행부
- 자바스크립트에서는 함수를 만드는 데 두 가지 다른 방식으로 나타낼 수 있다. 이는 함수 표현식과 함수 선언문이다.
```
var greeting_expression = function(name) {
	console.log('Hi, ' + name);
}

function greeting_declaration(name) {
	console.log('Hi, ' + name);
}

greeting_expression('Chloe');
greeting_declaration('Chloe');
```
- 함수를 호출할 때는 함수 리터럴이 할당된 변수 이름 또는 함수 선언문의 함수 이름이 필요하다. 
- 주의할 점은 함수 표현식에서 정의한 함수 이름은 해당 함수 안에서만 호출 가능하다. 
- 많은 양의 코드를 연관 있는 것끼리 정리해서 함수로 만들면 코드를 보기 좋게 정리할 수 있다. 또는 반복 사용하는 코드를 함수로 만들어 필요할 때마다 호출할 수 있다. 이를 통해 함수는 중복코드를 줄이고, 코드의 재사용이라는 장점을 가지고 있다.

## 35. 예외 처리하기
- 자바스크립트 코드를 실행하다 에러가 발생하면 그 즉시 중단된다. 이를 대비해서 예외 처리는 반드시 필요하다.
- 자바스크립트에서 사용할 수 있는 예외 처리 방법에는 throw문과 try-catch-finally문이 있다.
- throw문은 예외 상황을 미리 파악하고 에러를 발생시켜 이후 코드가 실행되지 않도록 한다. 
- try-catch-finally문을 통해 예상치 못한 에러와 개발자가 의도한 에러 모두 대응 가능하다.
- try-catch-finally문은 try 블록 안에서 발생된 에러를 잡아내고, catch 블록으로 제어권을 넘긴다. try 블록에서 발생된 에러 정보는 catch 문의 변수로 전달되기 때문에, 개발자는 프로그램 종료 없이 어떤 에러가 발생했는지 확인할 수 있다. finally 블록은 에러 발생 여부와 상관없이 실행되는 블록이다. 

## 36. arguments 객체 이해하기
- 자바스크립트 함수는 매개변수를 가진다. 여기서 매개변수와 같이 사용되는 언어가 있는데 바로 전달 인자(argument)이다.
- 매개변수가 함수 선언 시 작성되는 변수라면, 전달 인자는 함수가 호출될 때 전달되는 값이다.
- 자바스크립트는 전달 인자의 개수와 매개변수의 개수가 달라도 에러를 발생시키지 않는다. 그래서 매개변수와 무관하게 함수 호출 시 더 많은 인자를 전달할 수 있다.
- 매개변수 외에 함수에서만 사용 가능한 특별한 객체를 제공하는데, 바로 arguments 객체이다.
