## Creating a Class in WinJS

### 알아야하는 이유

당신의 윈도우 런타임 앱에서 자바스크립트 코드 안에서 클래스를 만들 필요가 있다.

### 해결책

WinJS.Class.define 을 이용하면 클래스를 만들수 있다.

### 사용법

클래스는 객체 지향 컨셉을 잘 지원하는 피쳐이다. 반면에 자바스크립트는 클래스를 빌트인으로 지원하지 않는다. 자바스크립트에서는 모든것이 객체이다.
WinJS 는 개발자에게 자신의 어플리케이션에서 클래스를 생성하고 이용할수 있도록 해준다.

* Constructor : 첫번째 인자, 생성자이다.
* Instance members : 두번째 인자, 인스턴스 변수
* Static members : 세번째 인자, 스태틱 변수
* return : 새로 정의된 네임스페이스 객체를 반환한다.

프로젝트에서 WinJSFundamentals.js

```
var Author = WinJS.Class.define(function(name, title) {

  this.name = name;
  this.title = title;

}, {

  _name: undefined,
  _title: undefined,
  name: {
    set: function(value) {
      this._name = value;
    },
    get: function() {
      return this._name;
    }
  },
  title: {
    set: function(value) {
      this._title = value;
    },
    get: function() {
      return this._title;
    }
  }
});

var author1 = new Author('Senthil', 'WinJS recipes');

console.log(author1.name);
console.log(author1.title);
```