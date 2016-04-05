## Using the Repeater Control

### 알아야 하는 이유

WinJS Repeater 콘트롤을 이용하여 data 의 collection 을 보여줄 칠요가 있다.

### 해결책

WinJS Repeater 컨트롤은 collection data 를 UI 로 보여줄 수 있는 WinJS 라이브러리 중 하나이다.
data-win-control 로, WinJS.UI.Repeater 를 설정하여, 사용할 수 있다. 그리고 나서 data-win-bind 를 이용하여, 프로퍼티를 컨트롤에 바인딩할 수 있다.

### 사용법

```
<table>
  <thead>
    <tr>
      <th> Employee ID </th>
      <th> Employee Name </th>
      <th> Employee Designation </th>
    </tr>
  </thead>
  <tbody id="repeaterData" data-win-control="WinJS.UI.Repeater">
    <tr>
      <td data-win-bind="textContent:id"></td>
      <td data-win-bind="textContent:name"></td>
      <td data-win-bind="textContent:disignation"></td>
    </tr>
  </tbody>
</table>
```

```
(function() {
  'use strict';
  
  function Initialize() {
  
    WinJS.UI.processAll().done(function() {
    
      var repeaterControl = document.getElementById('repeaterData').winControl;
      
      var Employees = new WinJS.Binding.List([
        {id: 1, name: 'Senthil Kumar', designation: 'Mobile Developer'},
        {id: 2, name: 'Lohith GN', designation: 'Mobile Developer'},
        {id: 3, name: 'Vidyasagar', designation: 'Game Developer'}
      ]);
      
      repeaterControl.data = Employees;
    
    });
  
  }
  
  document.getElementById('DOMContentLoaded', Initialize);

})();
```

**만약에 아이템을 호출 선택 가능하게 하려면, WinJS.UI.ItemContainer 를 이용하는 방법이 있다.**

```
<div id="repeaterData" data-win-control="WinJS.UI.Repeater">
  <div data-win-control="WinJS.UI.ItemContainer" data-win-bind="dataset.name:name">
    <div data-win-bind="textContent:name"></div>
  </div>
</div>
```

```
(function() {
  'use strict';
  
  function Initialize() {
  
    WinJS.UI.processAll().done(function() {
    
      var repeaterControl = document.getElementById('repeaterData').winControl;
      
      var Employees = new WinJS.Binding.List([
        {id: 1, name: 'Senthil Kumar', designation: 'Mobile Developer'},
        {id: 2, name: 'Lohith GN', designation: 'Mobile Developer'},
        {id: 3, name: 'Vidyasagar', designation: 'Game Developer'}
      ]);
      
      repeaterControl.data = Employees;
      repeaterControl.addEventListener('invoked', function(e) {
      
        var name = e.target.dataset.name;
        var message = new Windows.UI.Popups.MessageDialog(name);
        
        message.showAsync();
      
      });
    
    });
  
  }
  
  document.getElementById('DOMContentLoaded', Initialize);

})();
```