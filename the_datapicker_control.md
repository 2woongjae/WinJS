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

**다음과 같이 data-win-options 에서 monthPattern, datePattern, yearPattern 을 설정하여, UI 의 종류를 고를 수 있다.**

```
<div
  id="Birthday"
  data-win-control="WinJS.UI.DatePicker"
  data-win-options="{
    monthPattern: '{month.abbreviated}',
    datePattern: '{day.integer(2)}',
    yearPattern: '{year.abbreviated}'
  }">
</div>
```

**monthPattern**
* month.full
* month.abbreviated(Number)
* month.solo.full
* month.integer(Number)

**datePattern**
* month.integer(Number)
* dayofweek.abbreviated

**yearPattern**
* year.full
* year.abbreviated(Number)