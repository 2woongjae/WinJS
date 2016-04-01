# Add Namespace to an Existing Namespace

### 왜 사용해야 하나?

이미 있는 네임스페이스에 네임스페이스를 추가하고, 당신의 기능들을 정의할 필요가 있다.

### 해결책

WinJS.Namespace.defineWithParent 함수를 사용하여, 이미 존재하는 네임스페이스에 네임스페이스를 추가한다.

### 사용법

define 메서드와 비슷하게 사용하여, 이미 존재하는 네임스페이스에 새 네임스페이스를 추가할 수 있다.

* Parent namespace : 첫번째 인자, 존재하는 네임스페이스의 이름을 나타낸다.
* name : 두번째 인자, 새로운 네임스페이스의 이름을 나타낸다.
* Members : 세번째 인자, 이것은 선택적인 인자이다. 이미 정의된 네임스페이스에 새로운 오브젝트를 추가할때 사용된다. 
* return : 새로 정의된 네임스페이스 객체를 반환한다.

```
WinJS.Namesapce.define('Apress');
WinJS.Namespace.defineWithParent('Apress', 'Books', {
  Utilities: {
    DisplayMessage: function() {
      return "Message from Apress.Books Namespace";
    }
  }
});
```

```
console.log(Apress.Books.Utilities.DisplayMessage());
```

**네임스페이스는 오직 다른 네임스페이스, 클래스, 함수, 상수만 포함 가능하다.**