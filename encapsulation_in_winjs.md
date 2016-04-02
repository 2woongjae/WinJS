## Encapsulation in WinJS

### 알아야 하는 이유

당신이 라이브러리를 만들때, 당신은 몇개의 메서드만을 노출하기를 원한다. 당신은 캡슈화를 제공할 필요가 있다.

### 해결책

함수를 구현하고, 네임스페이스로 그것을 아카이브 한다. 변수는 글로벌 또는 함수 스코프를 가지고 있다. 이 특징은 자바스크립트에서 기능적으로 캡슐화로 사용될 수 있다.

### 사용법

```
(function(global) {

  function GetPageViews() {
    return 1000;
  }
  
  function GetCPMRate() {
    return 1;
  }
  
  WinJS.Namespace.define('DeveloperPublish', {
    GetPageViews: GetPageViews
  });

})(this);

console.log(DeveloperPublish.GetPageViews());
```

자동 실행 익명함수가 두개의 함수를 가지고 있다.
DeveloperPublish 네임스페이스를 이용하여, 퍼블릭하게 사용할 함수를 외부로 노출할 수 있다.

```
(function(global) {

  function GetPageViews() {
    return 1000;
  }
  
  function GetCPMRate() {
    return 1;
  }
  
  function GetTotalRate() {
    return GetPageViews() * GetCPMRate();
  }
  
  WinJS.Namespace.define('DeveloperPublish', {
    GetPageViews: GetPageViews,
    GetTotalRate: GetTotalRate
  });

})(this);

console.log(DeveloperPublish.GetPageViews());
console.log(DeveloperPublish.GetCPMRate()); // X
console.log(DeveloperPublish.GetTotalRate());
```