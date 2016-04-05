## Using the FlipView Control

### 알아야 하는 이유

collection 중에 하나만 볼 필요가 있습니다.

### 해결책

FlipView 컨트롤을 이용한다. photo gallery 앱의 사용을 참고하자.

### 사용법

```
<div id="template" data-win-control="WinJS.Binding.Template">
  <div>
    <h4 data-win-bind="innerText: name"></h4>
    <h6 data-win-bind="innerText: designation"></h6>
  </div>
</div>
<div
  id="flipView"
  data-win-control="WinJS.UI.FlipView"
  data-win-options="{
    itemTemplate: select('#template')
    itemDataSource: recipeData.Employees.dataSource
  }">
</div>
```

```
(function() {
  'use strict';
  
  var Employees = new WinJS.Binding.List([
    {id: 1, name: 'Senthil Kumar', designation: 'Mobile Developer'},
    {id: 2, name: 'Lohith GN', designation: 'Mobile Developer'},
    {id: 3, name: 'Vidyasagar', designation: 'Game Developer'}
  ]);
  
  WinJS.Namespace.define('recipeData', {
    Employees: Employees
  });

})();
```