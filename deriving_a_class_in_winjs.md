## Deriving a Class in WinJS

### 알아야 하는 이유

당신의 어플리케이션에 상속 컨셉을 적용할 필요가 있다.

### 해결책

WinJS.Class.derive 메서드를 이용하면, 다른 클래스로부터 상속을 받는 클래스를 만들수 있다.

### 사용법

* Base class : 첫번째 인자, 상속을 헤줄 부모 클래스
* Constructor : 두번째 인자, 클래스의 멤버를 초기화해주는 생성자 함수
* Instance members : 세번째 인자, 인스턴스 변수
* Static members : 네번째 인자, 스태틱 변수
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

var ContractEmployee = WinJS.Class.derive(Employee, function(name) {
  this.name = name;
  this.type = 'Contract Employee';
});

var ContractEmployee1 = new ContractEmployee('Senthil');

console.log(ContractEmployee1.name);
console.log(ContractEmployee1.type);
```

The WinJS.Class.derive function behaves like the WinJS.Class.define function, except that it uses the prototype of the base class using the Object.create function to construct the derived class. The Object.create method deruves one type from another by prototyping the parent object; it also adds the properties that are part of the child object.