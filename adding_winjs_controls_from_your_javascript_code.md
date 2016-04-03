## Adding WinJS Controls from Your Javascript Code

### 알아야 하는 이유

콘트롤을 HTML 에 추가하는 것이 아니라 자바스크립트를 통해 추가할 필요가 있다.

### 해결책

컨트롤을 명령적으로 만들수 있다. 자바스크립트에서 div 를 동적으로 생성하고 컨트롤을 만들 수 있다.

### 사용법

```
<div id="rating"></div>
```

```
(function() {
  'use strict';
  
  function AddControl() {
  
    var ratingDiv = document.getElementById('rating');
    var ratingCtrl = new WinJS.UI.Rating(ratingDiv);
    ratingCtrl.maxRating = 4;
  
  }

  document.addEventListener('DOMContentLoaded', AddControl);

})();
```

