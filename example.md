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