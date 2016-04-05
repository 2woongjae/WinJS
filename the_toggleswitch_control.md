## The ToggleSwitch Control

### 알아야 하는 이유

유저가 화면에서 '바이너리 옵션'(true/false)을 조정할 필요가 있다.
예를 들면 서비스를 켰다 껐다 할 필요가 있다.

### 해결책

WinJS.UI.ToggleSwitch 컨트롤을 이용한다. 이것은 기본 체크박스와 비슷하다.
하지만 더 나은 터치 동작을 지원한다. => 스와이프가 가능하다는 점.

### 사용법

```
<div
  id="locationServices"
  data-win-control="WinJS.UI.ToggleSwitch"
  data-win-options="{
    title:'Location Services',
    labelOff: 'Disabled',
    labelOn: 'Enabled',
    checked: true
  }">
</div>
<div id="info"></div>
```

```
(function() {
  'use strict';
  
  function GetControl() {
  
    WinJS.UI.processAll().done(function() {
    
      var toggleButton = document.getElementById('locationServices').winControl;
      var InfoElement = document.getElementById('info');
      
      toggleButton.addEventListener('change', function(args) {
      
        if (toggleButton.clicked) {
        
          InfoElement.innerHTML = 'Location Services enabled';
          
        } else {
        
          InfoElement.innerHTML = 'Location Services disabled';
        
        }
      
      });
    
    });
  
  }
  
  document.addEventListener('DOMContentLoaded', GetControl);

})();

```