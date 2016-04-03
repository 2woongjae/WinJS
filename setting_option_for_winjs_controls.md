## Setting Option for WinJS Controls

### 알아야 하는 이유

HTML 에서 콘트롤에 추가적인 프로퍼티를 줄 필요가 있다.

### 해결책

data-win-options 를 이용한다.

### 사용법

```
<div data-win-control="WinJS.UI.Rating" data-win-options="{maxRating: 4, enableClear: false}"></div>
```

**enableClear 이 true 이면, 어떻게 되는지 체크**