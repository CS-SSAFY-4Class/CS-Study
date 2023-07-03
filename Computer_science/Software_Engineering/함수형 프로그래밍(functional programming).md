# 함수형 프로그래밍
Functional Programming
<br><br>

## 개요
<br><br>

- 자료(data) 처리를 함수의 계산으로 취급하고,<br>
  "상태"(state)와 "가변 데이터"(variable)를 멀리하는 프로그래밍 패러다임.

- 명령형 프로그래밍 : "상태"를 바꾸는 것을 강조
  - Statement(문-文)와 Expression(식-式)으로 수행
  - 무엇을 <b>어떻게</b>
- 함수형 프로그래밍 : 함수의 응용을 강조
  - Expression으로 수행
  - <b>무엇을</b>
<br><br>

#### Statement

- 명령형 프로그래밍 언어의 가장 작은 독립 요소.
- 프로그램은 하나 이상의 문이 연결되어 형성된다.
- 문은 "식(expression)"과 같은 내부 요소를 포함할 수 있다.
<br><br>

- 단순문
    1. 대입문: `a = a + 1;`
    2. 함수: `function();`
    3. 리턴문: `return thing;`
    4. GOTO 문: `GOTO 1;`
    5. 선언문: `int i;`

- 복합문
    1. 구문 블록
    2. IF 문
    3. switch 문
    4. while 문
    5. do-while 문
    6. For-loop
<br><br>

#### Expression

- 프로그래밍 언어에서 값, 변수, 연산자, 함수의 모임.
- 값을 결정하기 위해 평가 될 수 있는 프로그래밍 언어 "구문(syntax)" 엔티티이다.

#### Syntax

- 구문(syntax)란 프로그래밍 언어에서 프로그램의 모습, 형태, 구조가 어떻게 보이는지에 대해 정의하는 것이며, <br>
  구문은 정해진 문법을 이용한다.


## 특징

### 1. 순수함수

- 동일한 입력에는 항상 같은 값을 반환해야 하는 함수
- 함수의 실행이 프로그램의 실행에 영향을 미치지 않아야 하는 함수
- 함수 내부의 인자의 값을 변경하거나, 프로그램의 상태를 변경하는 Side Effect가 없는 것

1. 순수함수 X
```JavaScript
// 전역 변수 num을 참조하기 때문
let num = 1;

function add(a) {
    return a + num;
}
```

2. 순수함수 O
```JavaScript
// 프로그램의 상태와 함수의 동작이 아무런 연관이 없다.
function add(a, b) {
    return a + b;
}

const result = add(2, 3);
```

<br><br>

### 2. 비상태, 불변성 (_Stateless, _Immutability)

- 함수형 프로그래밍에서의 data는 변하지 않는 불변성을 유지해야 한다.
- 데이터의 변경이 필요한 경우, 원본 데이터 구조를 변경하지 않고 그 데이터의 복사본을 만들어서 그 일부를 변경하고, 변경한 복사본을 사용해 작업을 진행한다.

  - 아래의 경우는 전역에 정의된 person의 age 상태를 변경하므로 불변성 유지를 만족하지 못한다.
```javascript
let person = { name: "jongmin", age: "26" };

function increaseAge(person) {
    person.age = person.age + 1;
    return person;
}
```
  - 만일 전역 data를 이용해야 한다면, 데이터의 복사본을 만들고, 함수의 동작을 한 후, 반환한다.

<br><br>

### 3. 선언형 함수

1. 명령형 프로그래밍
```javascript
let numbers = [1, 2, 3];

function multiply(numbers, multiplier) {
    for (let i = 0; i < numbers.length; i++) {
        numbers[i] = numbes[i] * multiplier;
    }
}
```
- `numbers`의 상태를 변화시키는 함수이다.
<br>

2. 선언형 프로그래밍
```javascript
function multiply(number, multiplier) {
    return number.map((num) => num * multiplier);
}
```
- `number`는 함수의 인자로서 전역변수일 필요가 없다.
- `number`의 각 인자들에 `multiplier`을 곱한 "iterable something"을 반환한다.
<br>

- `if`, `switch`, `for` 등 명령문을 사용하지 않고, <br>
  `filter`, `map`, `take`, `reduce` 등 최대한 함수형 코드를 사용한다.

<br><br>

### 1급 객체와 고차함수

#### 1급 객체

- 변수나 데이터 구조 안에 담을 수 있다.
- 파라미터로 전달할 수 있다.
- 반환값(return value)으로 사용할 수 있다.
- 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다.
- 동적으로 프로퍼티 할당이 가능하다.

```javascript
const addTwo = (num) => num + 2;
const multiplyTwo = (num) => num * 2;
const transform = (numbers) => numbers.map(addTwo).map(multiplyTwo);

console.log(transform([1, 2, 3, 4])); // [6, 8, 10, 12]
```
- JavaScript: 함수를 변수에 할당하거나 반환함
<br>

#### 고차함수

- 함수를 인자로서 전달할 수 있어야 한다.
- 함수의 반환 값으로 또 다른 함수를 사용할 수 있다.

```javascript
// 고차 함수
const addInform = (name) => (age) => age + name;
const ssafy = addInform("싸피");

console.log(ssafy("9")); // 9싸피
```
- 함수의 반환 값으로 다른 함수 사용


### 정리
<br>

- 함수형 프로그래밍은...
  - 높은 수준의 추상화를 제공한다.
  - 함수 단위의 코드로 재사용이 용이하다.
  - 불변성 지향으로 프로그램 동작 예측이 쉽다.
<br>

- 하지만...
  - 순수함수를 구현함에 있어 코드의 가독성을 해칠 수 있다.
  - 반복을 구현하기 위해 재귀를 이용하는데, 자칫하면 무한루프에 빠질 수 있다.
  - 함수간 조합은 어려운 과정이다.
<br>

- 그래서...
  - 함수형 프로그래밍은 객체 지향 프로그래밍과 같이 하나의 패러다임이다.
  - 무조건 함수형, 객체지향 따로 보는 것이 아닌, 같이 쓰이기도 한다.
  - 우리도 JavaScript 언어에서 객체지향 프로그래밍의 특성과 함수형 프로그래밍의 특성을 모두 이용했다.
    - `Vue.js - vuex`에서 `state`의 data는 직접 건들지 않던 `actions`
    - `Vue.js`의 한 컴포넌트 에서만 사용하는 data는 함수형으로 return 하여 DOM에 SideEffect를 내지 않던 것.


<br><br>

> 출처

- [JS부분](https://velog.io/@teo/functional-programming)
- [개념부분](https://jongminfire.dev/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%B4%EB%9E%80)
- 각 기초 문법(Statement, Syntax) : 나무위키
<br>

- [추가:명령형->함수형 변환하기](https://opentogether.tistory.com/76)