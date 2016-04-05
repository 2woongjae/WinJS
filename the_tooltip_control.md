## The Tooltip Control

### 알아야 하는 이유

유저가 어떤 엘리먼트에 호버할 경우 툴팁이 뜰 필요가 있다.

### 해결책



### 사용법

```
<button
  id="btnSace"
  data-win-control="WinJS.UI.Tooltip"
  data-win-options="{
    innerHTML: 'Saves the <b>Employee</b> record'
  }">
  Save
</div>
```

**.win-tooltip 의 css 를 조작하여, 디자인을 변경할 수 있다.**

```
.win-tooltip {
  background-color: bisque;
  border-radius: 30px;
  border-color: red;
}
```

**툴팁을 담은 컨테이너가 div 일 경우 div 의 default 가 block 이기 때문에 display 를 inline 으로 변경해줘야 한다.**