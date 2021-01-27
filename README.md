# :melon: 함수형 프로그래밍이란..

## 1. 함수형 ?

자바스크립트에서는 함수가 1급 시민으로 함수형 프로그래밍을 할 수 있다. 1급 시민은 함수를 정수나 문자열 처럼 일반 값처럼 취급된다는 뜻이다. 그래서 함수를 **_변수_** 에 넣을 수도 있고, **_배열_** 에 넣을 수도 있으며, **_다른 함수의 인자_** 로 넘길 수도 있다. **_함수의 반환 값_** 으로 사용 될 수 있다.
<br /><br />

## 2. 함수형 프로그래밍

함수형 프로그래밍에선 중요한 개념이 몇 가지 있다. 그 중 공부한 두 가지를 다뤄보자!

- 불변성

- 순수함수
  <br />
  <br />

### 2. 1. 불변성

함수형 프로그래밍에서는 데이터가 변할 수 없다. 그저 원본의 데이터를 복제하여, 복제한 데이터를 변경하여 작업을 실행한다.

```javascript
    let me = {
        name: '김덕기'
        weight: "66kg"
        military: true;
    }

    function changeName(me, newName) {
        me.name = newName;
        return me
    }

    console.log(changeName(me, 'ben').name) // ben
    console.log(me.name)                    // ben
```

위의 코드에서 볼 수 있듯 me 원본에서 name 속성은 변하였다. 불변성은 어떻게 작동할까? 답은 Object.assign, 스프레드 연산자(...)가 있다.

```javascript
// * Object.assign 메소드 사용
function changeName(me, newName) {
  const newMe = Object.assign({}, me);
  newMe.name = newName;
  return newMe;
}

console.log(changeName(me, "ben").name); // ben
console.log(me.name); // 김덕기
```

```javascript
// * 스프레드 연산자 사용
function changeName(me, newName) {
  const newMe = { ...me };
  newMe.name = newName;
  return newMe;
}

console.log(changeName(me, "ben").name); // ben
console.log(me.name); // 김덕기
```

<br />

### 2. 2. 순수 함수

순수 함수는 파라미터에 의해서만 반환값이 결정되는 함수를 뜻한다. 순수 함수는 최소 하나 이상의 인자를 받고, 인자가 같으면 항상 같은 값이나 함수를 반환한다. 순수 함수에는 부수 효과가 없다. 부수 효과란 전역 변수를 설정하거나, 함수 내부에 애플리케이션에 있는 다른 상태를 변경하는 것을 말한다. 순수 함수는 인자를 변경 불가능한 데이터로 취급한다.

_출처: 알렉스 뱅크스, 이브 포셀로 - 러닝 리액트 (한빛미디어) 66p._

순수 함수를 이해하기 위해 순수하지 않은 함수를 하나 보면,

```javascript
let dog = {
  name: "멍멍이",
  canBark: true,
  canPlaySoccer: false,
};

// 순수 하지 않은 함수
function specialCourse() {
  dog.canPlaySoccer = true;
  return dog;
}

specialCourse();

console.log(dog);
// { name: "멍멍이", canBark: true, canPlaySoccer: true}
```

specialCourse 함수를 호출하면 dog 객체의 속성이 바뀐다 = 함수 호출에 따른 부수 효과가 발생한다. 즉, 순수 함수가 아니다. 또한 원본 또한 변경한다.

```javascript
let dog = {
  name: "멍멍이",
  canBark: true,
  canPlaySoccer: false,
};

// 순수 함수
function specialCourse(anyDog) {
  return {
    ...anyDog,
    canPlaySoccer: true,
  };
}

console.log(specialCourse(dog));
// { name: "멍멍이", canBark: true, canPlaySoccer: true}
console.log(dog);
// { name: "멍멍이", canBark: true, canPlaySoccer: false}
```

위의 코드는 순수 함수다. 파라미터를 받았고, 복제된 새로운 객체를 반환하며, 밖에 있는 다른 변수를 변경하지 않기 때문이다.

리액트는 함수형 기법을 기반으로 만들어진 라이브러리다. 독립된 컴포넌트들이 프로퍼티로 데이터를 받아 UI를 렌더링한다. 컴포넌트들은 렌더링을 하는 역할만 담당하며 애플리케이션의 상태를 변화시키는 역할을 담당하지 않는다.

리액트의 어찌보면 가장 중요한 개념 **불변성**에 대해 알아 보았고 그 보다 더 넓은 개념인 함수형 프로그래밍에 대해서도 알아 보았다.
