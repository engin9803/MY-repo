- 기본형 데이터와 참조형 데이터  
자바스크립트 데이터 타입은 크게 두가지인 `원시형(Primitive Type)`과 `참조형(Reference Type)`으로 분리  
기본(원시)형 - `Number`, `String`, `Boolean`, `null`, `undefined` 가 있으며 ES6 에서는 `Symbol` 도 추가되었다  
참조형 - `객체(Object)`가 있고 그 하위에 `배열(Array)`, `함수(Function)`, `정규표현식(RegExp)` 등이 있으며, ES6에서는 `Map`, `Set`, `WeakMap`, `WeakSet` 등도 추가되었다. 
    - 두 타입의 차이는  
        - 기본형 - 바로 값을 그대로 할당 
        - 참조형 - 값이 저장된 주소값을 할당(참조)

- 불변 객체를 만드는 방법  
bject.assign(빈 객체, 복사하려는 객체)
```js
var obj1 = { name: 'Serzhul' }

var obj2 = Object.assign({}, obj1)

obj2.name = 'Daewon'
// obj1 => {name: 'Serzhul'}
// obj2 => {name: 'Daewon'}

// obj1의 불변성이 유지된다.
```
```js
Object.freeze(불변하게 만드려는 객체)
var obj1 = { name: 'Serzhul' }
Object.freeze(obj1)
obj1.name = 'Daewon'
console.log(obj1)
// {name: 'Serzhul'} => 속성 값이 변하지 않음
```
- 얕은 복사와 깊은 복사
    - 얕은 복사는 객체의 참조값(주소 값)을 복사하고
    - 깊은 복사는 객체의 실제 값을 복사합니다.

얕은 복사(shallow copy)
얖은 복사는 참조(주소)값의 복사를 나타낸다.
```js
const obj = { vaule: 1 }
const newObj = obj;

newObj.vaule = 2;

console.log(obj.vaule); // 2
console.log(obj === newObj); // true
```
자바스크립트의 참조 타입은 얕은 복사가 된다고 볼 수 있으며, 이는 데이터가 그대로 생성되는 것이 아닌 해당 데이터의 `참조 값(메모리 주소)`를 전달하여 결국 한 데이터를 공유함

깊은 복사(deep copy)
깊은 복사는 값 자체의 복사를 나타낸다.
```js
let a = 1;
let b = a;

b = 2;

console.log(a); // 1
console.log(b); // 2
console.log(a === b); // false
```
자바스크립트의 원시 타입은 깊은 복사가 되며, 이는 `독립적인 메모리에 값 자체를 할당하여 생성하는 것`이다.