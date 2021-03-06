# Vanilla JS

바닐라 JS는 날 것 그대로의 JavaScript를 말한다. 간단히 말해 각종 Library나 Framework가 없는 순수한 JavaScript다. Browser를 통해 user에게 제공된 JS를 말한다.

JavaScript는 HTML과 같이 오래전부터 웹 상에서 정보를 보여주기 위해 사용해왔다. 그 만큼 현대의 JS는 초기의 것과는 많이 다르다. 이렇게 업데이트 해온 데이터를 잘 보여주는 문서가 존재하는데, 이를 Specification이라 한다. JS에 관해서는 흔히 ES5, ES6라 부르는데 이는 ECMAScript5 Specification을 말한다.

JavaScript의 Code 작성 단계는 다음과 같다. 오류가 났을 때는 다시 한 번 살펴보자!

1. Create
2. Initiation
3. Use

JS는 API로 부터 데이터를 가져오고 refresh하지 않아도 된다. 왜냐면 JS가 보이지 않는 곳에서 계속 데이터를 가져오고 있기 때문이다.

# Vanilla JS 프로젝트 생성하기

Windows의 cmd창을 열어 다음 명령문을 입력한다. 

아래 명령문은 workspace로 이동하여 project를 생성을 수행한다.

```powershell
cd workspace
npx create-react-app project-name
```

## JavaScript Grammar

JS는 Camel case로 변수명을 적는 것을 원칙으로 한다. 

여기서 Camel case란 변수명을 낙타등처럼 대소문자 구분해서 쓰는 것을 말한다.

```jsx
// let: 변수 초기화 및 생성
let a = 220;
// const: 변수 상수(constant)화
const b = a-5;

// : 한 줄 주석처리
/* : 여러 줄 주석처리
     를 수행한다. */

console.log(b, a);
```

```jsx
//  Data Type  //
what = "Nico"; // String
what = true;  // Boolean
what = 88;    // Number
what = 36.5;  // Float
daysOfWeek = ["Mon", 22, "Wed"];  // Array
info = { 
	name: "Nico", 
	age: 33, 
	favMov: ["lov", "los"] 
}  // Object
```

```jsx
function sayHello(name, age) {
  console.log('Hello!', name, 'my age is', age);
  // backtick을 이용
  console.log(`Hello! ${name} my age is ${age}`);
} 
sayHello("Hana", 25);

// 함수를 변수에 저장 가능
const calc= {
  plus: function(a, b) {
    return a+b;
  }
}
console.log(calc.plus(5, 5));
```

```jsx
//  DOM example  //
title = document.getElementById("title");
title.innerHTML = "Hi, I'm changed By JS!"
console.dir(title);
title.style.color = "green";
document.title = "Example page";

// resize Event가 발생할 때마다 쿼리실행
// querySelector : document의 자식들을 탐색 후 조건부합 1개
title = document.querySelector("#title");
function handleResize() {
  console.log("I have been sized!");
}
window.addEventListener("resize", handleResize);

// user에게 age묻고 조건문 수행
const age = prompt("How old are you?");
if (age > 18 && age < 21) {
  console.log("you can drink but you should't ");
} else {
  console.log("ok");
}
```

### [Ref] JavaScript DOM Event MDN

[Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)

# 1. Make a Clock

WebPage 상의 JavaScript는 쉬지않고 계속해서 코드를 읽어들인다. 다음 코드를 실행하면, Web를 통해 실시간으로 시간이 변화하는 것을 확인할 수 있다. 

시계의 특성상 1초마다 함수를 수행하고 싶다면 setInterval이라는 함수를 사용한다. 이 함수는 2개의 매개변수를 통해 실행하고 싶은 함수와 수행하고 싶은 시간 간격(milli-second)을 필요로 한다. 

[https://www.javatpoint.com/javascript-setinterval-method#:~:text=JavaScript setInterval () method. The setInterval () method,expression or calls a function at given intervals](https://www.javatpoint.com/javascript-setinterval-method#:~:text=JavaScript%20setInterval%20%28%29%20method.%20The%20setInterval%20%28%29%20method,expression%20or%20calls%20a%20function%20at%20given%20intervals).

```html
<body>
    <div class="js-clock">
        <h1>00:00</h1>
    </div>
    <script src="clock.js"></script>
</body>
```

```jsx
const clockContainer = document.querySelector(".js-clock"),
  clockTitle = clockContainer.querySelector("h1");

function getTime() {
  const date = new Date();
  const minutes = date.getMinutes();
  const hours = date.getHours();
  const seconds = date.getSeconds();
  clockTitle.innerText = `${hours}:${minutes}:${seconds}`;
}

function init() {
  getTime();
}

init();
```

다음은 위의 JS를 보완한 코드다. 

```jsx
const clockContainer = document.querySelector(".js-clock"),
  clockTitle = clockContainer.querySelector("h1");

function getTime() {
  const date = new Date();
  const minutes = date.getMinutes();
  const hours = date.getHours();
  const seconds = date.getSeconds();
  // hh:mm:ss formating
  clockTitle.innerText = `${hours < 10 ? `0${hours}` : hours}:${
    minutes < 10 ? `0${minutes}` : minutes
  }:${seconds < 10 ? `0${seconds}` : seconds}`;
}

function init() {
  getTime();
  // 1초마다 수행
  setInterval(getTime, 1000);
}

init();
```

# 2. Save by Local storage

일반적으로 Browser에서 F12를 누르면, 개발자 도구를 사용할 패널이 보인다. 

여기서 상단의 '응용 프로그램'을 클릭하고, '저장소'의 '로컬 저장소'를 클릭하면 Local storage(키와 값으로 이루어진 테이블)를 확인할 수 있다. 

```html
<div class="js-clock">
    <h1>00:00</h1>
</div>
<!-- form내에 자식들은 Enter Event 확인가능 -->
<form class="js-form form">
    <input type="text" placeholder="What is your name?" />
</form>
<h4 class="js-greetings greetings"></h4>
<script src="clock.js"></script>
<script src="gretting.js"></script>
```

```jsx
const form = document.querySelector(".js-form"),
  input = form.querySelector("input"),
  greeting = document.querySelector(".js-greetings");

const USER_LS = "currentUser",
  SHOWING_CN = "showing";

function paintGreeting(text) {
  form.classList.remove(SHOWING_CN);
  greeting.classList.add(SHOWING_CN);
  greeting.innerText = `Hello ${text}`;
}

function loadName() {
  const currentUser = localStorage.getItem(USER_LS);
  if (currentUser === null) {
    // she is not
  } else {
    paintGreeting(currentUser);
  }
}

function init() {
  loadName();
}

init();
```

JS는 Event 처리를 제대로 해주지 않으면, 이 Event가  Document에 까지 영향을 미칠 수 있다. 예를 들어, form내의 input에서 enter를 누르는 Event를 제대로 처리하지 않으면 console.log에서 user의 입력값을 마주할 수 있다. 

이를 방지하기 위해 다음과 같은 매커니즘으로 처리하였다. preventDefault 함수를 통해 submit Event를 막고, addEventListener 함수를 통해 자체적으로 Event 처리를 하였다. 

```jsx
function saveName(text) {
  localStorage.setItem(USER_LS, text);
}

function handleSubmit(event) {
  event.preventDefault();
  const currentValue = input.value;
  paintGreeting(currentValue);
  saveName(currentValue);
}

function askForName() {
  form.classList.add(SHOWING_CN);
  form.addEventListener("submit", handleSubmit);
}

function loadName() {
  const currentUser = localStorage.getItem(USER_LS);
  if (currentUser === null) {
    askForName();
  } else {
    paintGreeting(currentUser);
  }
}
```

# 3. Make a To do list

```html
<head>
    <title>Something</title>
    <!-- emoticon 안보이는 오류해결 -->
    <meta charset="utf-8" />
    <link rel="stylesheet" href="index.css" />
</head>
<body>
    <h4 class="js-greetings greetings"></h4>
    <form class="js-toDoForm">
        <input type="text" placeholder="Write a to do" />
    </form>
    <ul class="js-toDoList">
    </ul>
    <script src="clock.js"></script>
    <script src="gretting.js"></script>
    <script src="todo.js"></script>
</body>
```

```jsx
const toDoForm = document.querySelector(".js-toDoForm"),
  toDoInput = toDoForm.querySelector("input"),
  toDoList = document.querySelector(".js-toDoList");

const TODOS_LS = "toDos";

// 동적으로 li element 생성
function paintToDo(text) {
  const li = document.createElement("li");
  const delBtn = document.createElement("button");
  delBtn.innerText = "❌";
  const span = document.createElement("span");
  span.innerText = text;
  li.appendChild(delBtn);
  li.appendChild(span);
  toDoList.appendChild(li);
}

function handleSubmit(event) {
  event.preventDefault();
  const currentValue = toDoInput.value;
  paintToDo(currentValue);
  toDoInput.value = "";
}

function loadToDos() {
  const toDos = localStorage.getItem(TODOS_LS);
  if (toDos !== null) {
  }
}

function init() {
  loadToDos();
  toDoForm.addEventListener("submit", handleSubmit);
}

init();
```

Local storage에는 JS의 데이터를 저정할 수 없다. 다만 string만 저장이 가능하다. 

따라서 JSON.stringify 함수를 통해 JS Object를 string으로 바꿔준다. 여기서 JSON은 JavaScript Object Notation의 준말이다. 반대로 string을 JS Object로 바꿔주기 위해서는 JSON.parse를 사용하면 된다.

```jsx
const toDos = [];

function saveToDos() {
  // JSON.stringify : JS object => string
  localStorage.setItem(TODOS_LS, JSON.stringify(toDos));
}

function paintToDo(text) {
  const li = document.createElement("li");
  const delBtn = document.createElement("button");
  const span = document.createElement("span");
  const newId = toDos.length + 1;
  delBtn.innerText = "❌";
  span.innerText = text;
  li.appendChild(delBtn);
  li.appendChild(span);
  li.id = newId;       // ㄱㅊ?
  toDoList.appendChild(li);
  const toDoObj = {
    text: text,
    id: newId
  };
  toDos.push(toDoObj);
  saveToDos();
}

function loadToDos() {
  const loadedToDos = localStorage.getItem(TODOS_LS);
  if (loadedToDos !== null) {
    // JSON.parse : string => JS object
    const parsedToDos = JSON.parse(loadedToDos);
    // Array.forEach : array 요소들에 대해 한번씩 함수를 실행
    parsedToDos.forEach(function(toDo) {
      paintToDo(toDo.text);
    });
  }
}
```

부모 요소의 속성 등과 같이 해당 요소와 관련된 html 코드를 확인하고 싶다면, console.dir 함수를 이용한다. 

```jsx
let toDos = [];

function deleteToDo(event) {
  const btn = event.target;
  const li = btn.parentNode;
  toDoList.removeChild(li);
  // array.filter : 매개하는 함수(return boolean)가 체크(true)된 아이템들의 array를 반환
  const cleanToDos = toDos.filter(function(toDo) {
    return toDo.id !== parseInt(li.id);
  });
  toDos = cleanToDos;
  saveToDos();
}

function saveToDos() {
  delBtn.innerText = "❌";
  delBtn.addEventListener("click", deleteToDo);
}
```

### [Ref] delete remove child

[Node.removeChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)

### [Ref] array filter

[Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

# 4. Set Image background

이미지 파일 사이즈가 큰 경우 화면에 이미지가 로드되는 것을 눈으로 확인할 수 있다. 하지만 이는 미관상 좋지않다.

따라서 JS에서 이미지를 load한 뒤에 보여주는 것이 좋다.

```jsx
const body = document.querySelector("body");

const IMG_NUMBER = 3;

function paintImage(imgNumber) {
  const image = new Image();
  image.src = `images/${imgNumber + 1}.jpg`;
  // css에서 크기조정
  image.classList.add("bgImage");
  // appendChild이면 이전 element들을 가림
  body.prepend(image);
}

function genRandom() {
  // ex. img_num이 5라면, 0~4까지의 숫자 반환
  const number = Math.floor(Math.random() * IMG_NUMBER);
  return number;
}

function init() {
  const randomNumber = genRandom();
  paintImage(randomNumber);
}

init();
```

```css
body {
  background-color: #2c3e50;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.bgImage {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  animation: fadeIn 0.5s linear;
}
```

# 5. Show Weather info

```jsx
const COORDS = "coords";

function saveCoords(coordsObj) {
  localStorage.setItem(COORDS, JSON.stringify(coordsObj));
}

function handleGeoSuccess(position) {
  const latitude = position.coords.latitude;
  const longitude = position.coords.longitude;
  const coordsObj = {
    latitude,
    longitude
  };
  saveCoords(coordsObj);
}

function handleGeoError() {
  console.log("Can't access Geo location");
}

function askForCoords() {
  navigator.geolocation.geoCurrentPosition(handleGeoSuccess, handleGeoError);
}

function loadCoords() {
  const loadedCoords = localStorage.getItem(COORDS);
  if (loadedCoords === null) {
    askForCoords();
  } else {
    // getWeather
  }
}

function init() {
  loadCoords();
}
init();
```

### Coords [Noun]

= a pair of numbers and/or letters that show the exact position of a point on a map, graph or image.

[coords](https://dictionary.cambridge.org/ko/%EC%82%AC%EC%A0%84/%EC%98%81%EC%96%B4/coords)

# 5-1. Get from Weather API

```jsx
const API_KEY = "241051bf13976dd3ddf8b8d9f247255e";
const COORDS = "coords";

function getWeather(lat, lng) {
  fetch(
    `https://api.openweather.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`
  )
    .then(function (response) {
      return response.json();
    })
    .then(function (json) {
      console.log(json);
    });
}

function handleGeoSuccess(position) {
  saveCoords(coordsObj);
  getWeather(latitude, longitude);
}
```

```jsx
function loadCoords() {
  const loadedCoords = localStorage.getItem(COORDS);
  if (loadedCoords === null) {
    askForCoords();
  } else {
    const parseCoords = JSON.parse(loadedCoords);
    console.log(parseCoords);
    getWeather(parseCoords.latitude, parseCoords.longitude);
  }
}
```

```jsx
const weather = document.querySelector(".js-weather");

function getWeather(lat, lng) {
  fetch(
    `https://api.openweather.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`
  )
    .then(function (response) {
      return response.json();
    })
    .then(function (json) {
      const temperature = json.main.temp;
      const place = json.name;
      weather.innerText = `${temperature} @ ${place}`;
    });
}
```

### API (Application Programming Interface)

= 다른 서버로부터 손쉽게 데이터를 가져올 수 있는 도구.

특정 웹사이트로 부터 데이터를 얻거나 컴퓨터끼리 소통하기 위해 고안.

### [API] By geographic coordinates

[Weather API](https://openweathermap.org/api)

[Free Weather API - WeatherAPI.com](https://www.weatherapi.com/)

# Problem

### Id가 중복되는 문제

```jsx
const newId = toDos.length + 1;
```

### [Sol]

todo의 변경에 관계없이, todo가 생성될 때마다 언제나 1이 증가하는 변수를 생성한다.

```jsx
let idNumbers = 1;

const newId = idNumbers;
idNumbers += 1;
```