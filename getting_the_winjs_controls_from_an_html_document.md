## Getting the WinJS Controls from an HTML Document

### 알아야 하는 이유

HTML 페이지에 삽입한 컨트롤을 자바스크립트에서 얻어와서 프로퍼티를 셋업할 필요가 있다.

### 해결책

DOM 엘리먼트로부터 컨트롤을 얻어와서, winControl 프로퍼티를 사용한다.

### 사용법

```
<div id="rating" data-win-control="WinJS.UI.Rating"></div>
```

```
(function() {
  'use strict';
  
  function GetControl() {
  
    WinJS.UI.processAll().done(function() {
    
      var ratingControl = document.getElementById('rating').winControl;
      ratingControl.userRating = 2;
    
    });
  
  }

  document.addEventListener('DOMContentLoaded', GetControl);

})();
```