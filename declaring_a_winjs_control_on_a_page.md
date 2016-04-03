## Declaring a WinJS Control on a Page

### 알아야 하는 이유

당신의 앱에 페이지에 WinJS 콘트롤을 추가할 필요가 있다.

### 해결책

div 태그에 data-win-control 속성을 사용하여 추가할 수 있다.

### 사용법

```
<!DOCTYPE html>
<html>
<head>

  <meta charset="utf-8" />
  <title>UWP</title>
  
  <link href="WinJS/css/ui-light.css" rel="stylesheet" />
  <script src="WinJS/js/base.js"></script>
  <script src="WinJS/js/ui.js"></script>
  
  <link href="/css/default.css" rel="stylesheet" />
  <script src="/js/main.js"></script>
  
</head>
<body class="win-type-body">
  <div data-win-control="WinJS.UI.Rating"></div>
</body>
</html>
```

**컨트롤을 인스턴스화하려면 페이지에 WinJS JavaScript 파일을 포함하고 코드에서 WinJS.UI.processAll 함수를 호출해야 합니다.**