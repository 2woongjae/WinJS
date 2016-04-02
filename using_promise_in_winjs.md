## Using Promise in WinJS

### 알아야 하는 이유

당신은 코드를 비동기적으로 실행하여, UI 가 좀더 반응성이 좋도록 할 필요가 있다.

### 해결책

이 방법을 통하여, UI 쓰레드가 자유롭고 당신의 입력에 반응성이 더 좋아지도록 할 수 있다.

### 사용법

WinJS 와 UWp 에서 비동기 API 는 promise 로 대표된다. 그 중 대표적인 promise 구현체는 xhr 함수입니다. xhr 함수는 XMLHttpRequest 를 프로미스로 래핑한 것이다. 당신이 URL 과 response 타입을 지정하면, xhr 함수는 프로미스를 반환하고, 성공시 데이타를 반환하고, 실패시 error 를 반환한다.

```
WinJS.Utilities.ready(function() {
  var input = document.getElementById('inputurl');
  input.addEventListener('change', changeEvent);
}, false);

function changeEvent(e) {
  var resultDiv = documentById('output');
  
  WinJS.xhr({url: e.target.value}).then(function completed(result) {
    if (result.status === 200) {
      resultDiv.style.background = 'Green';
      resultDiv.innerText = 'Success';
    }
  }, function error(e) {
    resultDiv.style.background = 'red';
    resultDiv.innerText = e.statusText;
  });
}
```

```
xhrPromise.cancel();
```