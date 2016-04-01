## Namespaces in Javascript

### 왜 사용해야 하나?

* 공통 기능들을 묶어주고,
* WinJS 라이브러리 사용하여 개발시, 개발자의 자바스크립트 코드에 네이밍 충돌 오류를 막기위해서

### 해결책

네임스페이스는 개발자가 공통의 기능들을 더 나은 묶음과 조직하게 해준다.
다른 언어들 - C#, VB.NET, Java, etc - 이런 특성을 제공한다.
많은 자바스크립트 프레임워크들은 네임스페이스를 제공하지 않지만,
WinJS 는 개발자가 자신의 프로젝트에 네임스페이스 기능을 이용할 수 있도록 제공한다.
네임스페이스는 유용하게 사용할수 있다. 특히나 당신의 앱이 여러 개발자의 여러 라이브러리를 이용할 경우에 그렇다.

### 사용법

WinJS.Namespace.define 함수를 이용하여 사용 가능하다.

```
var object = WinJS.Namespace.define(name, members);
```

두개의 인자를 사용한다.

* name : 첫번째 인자, 새로운 네임스페이스의 이름을 나타낸다.
* Members : 두번째 인자, 이것은 선택적인 인자이다. 이미 정의된 네임스페이스에 새로운 오브젝트를 추가할때 사용된다. 
* return : 새로 정의된 네임스페이스 객체를 반환한다.

** 인자 하나 짜리 define **
```
// DeveloperPublish 라는 새로운 네임스페이스를 만든다.
WinJS.Namespace.define('DeveloperPublish');

// DeveloperPublish 네임스페이스 안에 Utilities 라는 객체를 만든다.
DeveloperPublish.Utilities = {
  DisplayMessage: function() {
    return "Message from DeveloperPublish Namespace";
  }
}
```

** 인자 두개 짜리 define *** 

```
// Apress 라는 새로운 네임스페이스를 만들면서, 그안에 Utilities 라는 객체를 만든다.
WinJs.Namespace.define('Apress', {
  Utilities: {
    DisplayMessage: function() {
      return "Message from Apress Namespace";
    }
  }
});
```

** define 으로 선언된 네임스페이스 사용하기 **
```
console.log(DeveloperPublish.Utilities.DisplayMessage());
console.log(Apress.Utilities.DisplayMessage());
```

### WinJS.Namespace = default Namespace

디폴트 네임스페이스는 다음과 같은 객체와 함수를 가지고 있다.

* 프로미스 객체
* namespace, log, xhr 을 정의하는 함수

그래서 아래와 같은것이 있다.


* promise (객체)
* vailidation (프로퍼티)
* define (함수)
* defineWithParent (함수)
* log (함수)
* xhr (함수)

정의되기 전에 참조할수 없다는 점을 기억하라.
만약에 시도하면, 'Namespace is undefined' 라는 에러가 나온다.

스코프에 대한 문제를 잘 다룰수 있게 도와주는 WinJS 라이브러리의 feature 이다.
WinJS/js 폴더에 base.js 파일에 네임스페이스 구현체가 있다.
