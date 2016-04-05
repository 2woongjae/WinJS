## The TimePicker Control

### 알아야 하는 이유

어플리케이션 페이지에서 유저에게 시간을 선택하게 할 필요가 있다.

### 해결책

WinJS.UI.TimePicker 를 이용한다.

### 사용법

```
<div 
  id="TimeSelector" 
  data-win-control="WinJS.UI.TimePicker">
</div>
<div id="info"></div>
```

```
(function() {
  'use strict';
  
  function GetControl() {
  
    WinJS.UI.processAll().done(function() {
    
      var timePicker = document.getElementById('TimeSelector').winControl;
      var InfoElement = document.getElementById('info');
      
      timePicker.addEventListener('change', function(args) {
      
        InfoElement.innerHTML = timePicker.current.toTimeString();
      
      });
    
    });
  
  }

  document.addEventListener('DOMContentLoaded', GetControl);

})();
```

**다음과 같이 data-win-options 에서 clock, minuteIncrement, hourPattern, minutePattern, periodPattern 를 설정하여, UI 의 종류를 고를 수 있다.**

```
<div
  id="TimeSelector"
  data-win-control="WinJS.UI.TimePicker"
  data-win-options="{
    clock: '24HourClock',
    minuteIncrement: 15,
  }">
</div>
```

**hourPattern**
* hour.integer(Number)

**minutePattern**
* {minute.integer(Number)}

**periodPattern**
* period.abbreviated(Number)