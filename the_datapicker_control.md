## The DataPicker Control

### 알아야 하는 이유

어플리케이션 페이지에서 유저에게 날짜를 선택하게 할 필요가 있다.

### 해결책

WinJS.UI.DataPicker 를 이용한다.

### 사용법

```
<div 
  id="Birthday" 
  data-win-control="WinJS.UI.DataPicker">
</div>
<div id="info"></div>
```

```
(function() {
  'use strict';
  
  function GetControl() {
  
    WinJS.UI.processAll().done(function() {
    
      var dataPicker = document.getElementById('Birthday').winControl;
      var InfoElement = document.getElementById('info');
      
      dataPicker.addEventListener('change', function(args) {
      
        InfoElement.innerHTML = dataPicker.current.toDateString();
      
      });
    
    });
  
  }

  document.addEventListener('DOMContentLoaded', GetControl);

})();
```