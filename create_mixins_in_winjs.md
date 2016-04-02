## Create Mixins in WinJS

### 알아야 하는 이유

여러개의 자바스크립트 객체들의 메서드와 프로퍼티를 결합할 필요가 있다.

### 해결책

WinJS.Class.mix 메서드를 이용하여 결합한다.

### 사용법

derive 는 프로토타입 상속을 이용한다. 프로토타입 상속에는 좋은점과 나쁜점이 있다.
그것은 프로세스에 추가적인 시간이 필요하다. 그리고 성능에 영향을 미친다.
이것은 mix 를 통해서 극복될 수 있다.

* Constructor : 첫번째 인자, 클래스의 멤버를 초기화해주는 생성자 함수
* Mixin : 두번째 인자, mix 할 메서드를 가진 array
* return : 새로 정의된 네임스페이스 객체를 반환한다.

```
var Employee = WinJS.Class.define(function() {
  this.name = name;
  this.type = 'Employee';
}, {
  _name: undefined,
  _type: undefined,
  name: {
    set: function(value) {
      this._name = value;
    },
    get: function() {
      return this._name;
    }
  },
  type: {
    set: function(value) {
      this._type = value;
    },
    get: function() {
      return this._type;
    }
  }
});

var ContractEmployee = WinJS.Class.mix(function(name) {
  this.name = name;
  this.type = 'Contract Employee';
}, Employee);

var ContractEmployee1 = new ContractEmployee('Senthil');

console.log(ContractEmployee1.name);
console.log(ContractEmployee1.type);
```

**derive 와 다른 몇가지 특징이 더 있다**
* 다중 상속을 지원한다.
* 두번째 인자인 mixins 는 array 이기 때문에 다중 상속이 가능하다. (예제 필요)
