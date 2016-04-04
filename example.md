## Example

### WinJS.Class.mix 기본 사용

```
// Robot 이라는 클래스를 새로 생성한다.
var Robot = WinJS.Class.define(function (name) {
    this.name = name;
});

// Movable 이라는 객체를 생성한다.
var Movable = {
    direction: "stopped",
    goForward: function () { this.direction = "going forwards" },
    goBackward: function () { this.direction = "going backwards" },
    turnRight: function () { this.direction = "turning right" },
    turnLeft: function () { this.direction = "turning left" },
};

// Robot 에 Movable 을 mix 한다.
WinJS.Class.mix(Robot, Movable);

// Robotics 라는 네임스페이스를 생성하고, Robot 을 대입한다.
WinJS.Namespace.define("Robotics", {
    Robot: Robot
});

// Robotics.Robot 클래스를 통해 객체를 생성한다.
var myRobot = new Robotics.Robot("Mickey");

// Movable 객체에 있던 메서드를 호출한다.
myRobot.goBackward();

console.log(myRobot.direction);
```

```
"going backwards"
```

### WinJS.Class.mix 심화 사용 1
**WinJS.Utilities.eventMixin**
```
// Robot 이라는 클래스를 새로 생성한다.
var Robot = WinJS.Class.define(function (name) {
        this._name = name;
    }, {
        name: {
            get: function () {
                return this._name;
            },
            set: function (newName) {
                this._name = newName;
                this.dispatchEvent('rename');
            }
        }
});

// 1. 이벤트 수신기 기능을 얻는다.
WinJS.Class.mix(Robot, WinJS.Utilities.eventMixin);

// 2. 이벤트를 정의하게 됩니다.
// 내부적으로 rename 이란 이벤트의 set function 이 addEventListener 로 되어 있기 때문에 
// 미리 WinJS.Utilities.eventMixin 을 mix 해줘야 한다.
WinJS.Class.mix(Robot, WinJS.Utilities.createEventProperties("rename"));

var robot = new Robot("Bob");

/*
robot.addEventListener("rename", function () {
    console.log("Robot renamed to " + this.name);
}.bind(robot));
*/

robot.onrename = function () {

    console.log(this.name);

}.bind(robot)

robot.name = "Jim";
// Output: "Robot renamed to Jim"

```

```
"Jim"
```

### WinJS.Class.mix 심화 사용 2
**WinJS.UI.DOMEventMixin**
```
//
var MyButton = WinJS.Class.define(function (elem) {
    				this._domElement = elem;
   				 elem.winControl = this;
   				 this._numberClicks = 0;
    },
    {
        initialize: function () {

            this._domElement.appendChild(document.createElement('button'));

            function clickHandler(ev) {
                var clicks = ++this._numberClicks;
                document.getElementById("report").innerText = clicks;
            }
            this._domElement.querySelector('button').addEventListener("click", 
												    clickHandler.bind(this));
        }
});

//
WinJS.Class.mix(MyButton, WinJS.UI.DOMEventMixin);

//
var button = new MyButton(document.getElementById("div"));
button.initialize();
```

```
"Jim"
```

**일반 클래스에 통으로 이벤트를 걸때 유용하다. 어차피 하나하나에는 이벤트가 걸린다.**

WinJS.Utilities.eventMixin은 JavaScript에서 완전히 처리되는 형식에 대한 이벤트를 정의하는 데 유용합니다. DOM 요소에 연결된 이벤트를 사용할 때는 이 mixin이 별로 도움이 되지 않습니다. WinJS 컨트롤은 HTML 요소를 래핑하고 조작합니다. 이러한 컨트롤은 주로 연결된 DOM 요소에서 발생된 DOM 이벤트를 기반으로 하는 이벤트를 포함합니다. 예를 들어 DatePicker를 사용할 경우 3개의 select 컨트롤에서 개별 변경 이벤트를 추적하는 것보다 DatePicker 컨트롤의 변경 이벤트에 응답하는 것이 더 쉽습니다.
이벤트를 DOM 요소가 아닌 컨트롤 형식에 연결하면 DatePicker의 구현이 포함된 컨트롤을 바꾸는 경우처럼 코드가 변경되지 않도록 방지할 수 있습니다.
DOM 이벤트 모델은 이벤트 전파를 가능하게 합니다. DOM 이벤트는 DOM 트리까지 전파되며 어떤 수준에서도 처리 가능합니다. 이러한 특성은 클릭 가능 요소가 많이 있을 때 유용합니다. 예를 들어 DIV 요소에 이러한 요소를 포함하는 단일 클릭 처리기 함수를 추가한 다음 버블링될 때 포함된 모든 요소의 모든 클릭 이벤트를 처리할 수 있습니다. DOM 이벤트 처리에 대한 자세한 내용은 이벤트 캡처 및 이벤트 버블링을 참조하세요.
WinJS.UI.DOMEventMixin에는 DOM 트리까지 전파되는 이벤트를 구현하는 메서드가 있습니다. 여기에는 세 개의 함수 addEventListener, removeEventListener 및 dispatchEvent가 있습니다.
만든 형식에 이 mixin을 추가하려면 해당 형식에 대해 이름이 _domElement인 속성을 설정해야 합니다. 이 필드는 이벤트를 발생시킬 때 WinJS.UI.DOMEventMixin 구현이 찾는 필드로, 이벤트에 대한 대상 노드가 됩니다.
다음 코드에서는 DIV 요소에 대해 최소 컨트롤 클래스를 만들고 WinJS.UI.DOMEventMixin을 혼합하는 방법을 보여줍니다. 그런 후 click 이벤트에 대한 이벤트 수신기를 추가한 다음 응답할 수 있습니다.