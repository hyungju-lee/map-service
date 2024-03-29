## Node.js

Node.js는 JavaScript 런타임이다.  
런타임이란 프로그래밍 언어가 구동되는 환경을 뜻한다.  
JavaScript는 원래는 브라우저에서만 돌아가는 언어였음에도 불구하고 현재는 현재는 Node.js를 통해서 다양한 부분, 
서버라던지 다른 부분에서 활용되고 있다.

## npm (Node Package Manager)

npm이란 node package manager를 뜻하는데, 모듈에 대한 개념을 먼저 알고가면 좋을 것 같다.  

## 모듈

모듈이란 어플리케이션을 구성하는 개별적 요소를 뜻한다.  
모듈을 사용함으로써 기능적으로 분리가 되고 개발 효율성과 유지보수성이 향상된다.  
npm은 이러한 모듈들을 패키지화 하여 모아둔 저장소 역할을하고 또 이를 설치하고 관리해주는 툴이다.  

## Node 설치확인 명령어

```bash
node --version
node -v

npm --version
npm -v
```

## express 및 nodemon 설치, 실행하기

```bash
npm i -g nodemon
```

`-g` 플래그는 글로벌로 설치하여 프로젝트 폴더경로 상관없이 모든 곳에서 **nodemon** 패키지를 쓸 수 있도록 해주는 것이다.  
**nodemon** 패키지는 서버를 껐다 켰다하는 그런 불편함을 좀 해소시켜주는 패키지라고 보면 되겠다.  

```bash
npm i -g express-generator
```

동일하게 `global`로 설치를 할 거고 `express`는 웹 서버를 쉽게 만들 수 있는 프레임워크이다.  

## express 를 활용하여 프로젝트 생성하기

```bash
express --ejs (프로젝트명)
express --ejs myfirstmap
```

위와 같은 명령어를 실행하게 되면 myfirstmap 폴더가 생성되고 자연스럽게 프레임워크가 생성되는 것을 알 수 있다.

![](/img/image00.jpg)

```bash
cd myfirstmap
```

myfirstmap 폴더로 이동하고

```bash
npm i
```

해당 `package.json`에 명시되어있는 패키지를 설치한다.

---

이제 기본 준비는 끝났다.  
아까 설치했던 **nodemon** 패키지를 통해서 서버를 한번 켜 보도록 하겠다.  

```bash
nodemon ./bin/www
```

![](/img/image01.jpg)
![](/img/image02.jpg)

---

이번 시간엔 네이버 api를 통해서 지도 서비스를 웹 페이지에 띄우는 작업을 해보도록 하겠다.  
우선 네이버를 키고 검색창에 '네이버 클라우드 플랫폼'을 적어주시고 첫번째 검색되는 사이트에 들어가면 된다.  

이 사이트는 다양한 api 서비스를 사용할 수 있는 개발자 플랫폼이다.  

회원가입을 하시고 로그인을 완료하시고나서 console 버튼을 클릭하시면 다양한 어플리케이션을 볼 수 있는 사이트에 들어올 수 있는데, 
`AI NAVER API` 섹션을 클릭한 후 Application 섹션을 클릭해주시면 

![](/img/image03.png)
![](/img/image03.jpg)
![](/img/image04.jpg)

위와 같이 어플리케이션을 등록할 수 있는 화면이 나온다.  

![](/img/image05.jpg)

여기서 Application 등록 버튼을 클릭하고 

![](/img/image06.jpg)

위와 같이 application 이름을 적어주시고,, 이번에 우리는 Naver 지도를 사용할 것이다.  
네이버 지도 API 중에 Web Dynamic Map을 체크를 해주신 다음에 

![](/img/image07.jpg)
![](/img/image08.jpg)

위와 같이 추가해주신 다음에 '등록' 버튼을 누르면

![](/img/image09.jpg)

네이버 지도를 이제 활용할 수 있는 준비가 끝이 났다.

---

이제 지도 api를 웹에 띄워보는 시간을 가져보도록 하겠다.  

![](/img/image10.jpg)

위와 같이 책자 모양을 클릭하게 되면, 

![](/img/image11.jpg)

위와 같이 설명서가 나오게 된다.  
위 화면에서 **Web Dynamic Map v3 사이트 바로가기**를 클릭해주시면 Naver Map api를 사용할 수 있는 Document 사이트가 나오게 된다.  

![](/img/image12.jpg)

시작하기를 누르시면, 

![](/img/image13.jpg)

네이버 클라우드 플랫폼에서 제공하는 코드를 확인할 수 있다.  
위의 코드들을 그대로 복붙하시면 지도가 뜨는 것을 확인할 수 있다.  

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
    <title>간단한 지도 표시하기</title>
    <script type="text/javascript" src="https://openapi.map.naver.com/openapi/v3/maps.js?ncpClientId=YOUR_CLIENT_ID"></script>
</head>
<body>
<div id="map" style="width:100%;height:400px;"></div>

<script>
var mapOptions = {
    center: new naver.maps.LatLng(37.3595704, 127.105399),
    zoom: 10
};

var map = new naver.maps.Map('map', mapOptions);
</script>
</body>
</html>
```

위 코드를 `myfirstmap`에 그대로 복붙해보도록 하겠다.  
`myfirstmap/views/index.ejs` 파일에 그대로 복붙해주면 된다.  

위 코드에서 중요한 부분은

```html
<script type="text/javascript" src="https://openapi.map.naver.com/openapi/v3/maps.js?ncpClientId=YOUR_CLIENT_ID"></script>
```

위 부분인데, 네이버 지도를 띄울 수 있는 코드이다.  
위에서 **YOUR_CLIENT_ID**라는 곳에 아까 만들었던 myfirstmap 프로젝트의 Client id를 입력해야된다.  

![](/img/image14.jpg)

사이트이 '인증정보'라는 탭이 있다.  
클릭을 해보시면

![](/img/image15.jpg)

여기에 Client_id, Client_secret이 있다.  
여기서 Client_id를 복사하신 후에 

```html
<script type="text/javascript" src="https://openapi.map.naver.com/openapi/v3/maps.js?ncpClientId=vf2sd1hd65"></script>
```

**YOUR_CLIENT_ID** 부분에 넣어주면 된다.  
그리고 저장을 해주시고, 서버를 한번 켜봐야겠지?  

```bash
nodemon ./bin/www
```

`localhost:3000` 으로 접속하면

![](/img/image16.jpg)

위와 같이 지도가 나오는 화면을 볼 수 있다.  
앞으로 위 지도 서비스를 활용해서 코로나맵 클론 프로젝트를 천천히 하나씩 진행해보는 시간을 갖도록 하겠다.

---

## 지도 페이지 CSS 적용하기

```html
<link rel="stylesheet" href="/stylesheets/style.css">
```

![](/img/image17.jpg)

실제 경로는 위와 같지만 `link` 태그에 경로는 다르게 적어준다.

## 지도 배너 만들기

```html
<div id="navbar">myfirstmap</div>
```

```css
#navbar {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 50px;
  background-color: #262626;
  color: #fff;
  font-weight: bolder;
  font-size: 25px;
}
```

## 인포박스 만들기

```html
<div id="infoBox">
  <div id="infoTitle">현재날짜</div>
  <div id="infoContent">2020.11.08</div>
</div>
```

```css
#infoBox {
  position: absolute;
  top: 100px;
  left: 20px;
  z-index: 10;
  padding: 15px;
  border: 1px solid rgba(0,0,0,0.2);
  border-radius: 4px;
  background-color: #fff;
  text-align: center;
}

#infoTitle {
  font-size: 15px;
  font-weight: bolder;
}
```

## 마커 만들고 지도위에 표시하기

```javascript
  var mapOptions = {
    center: new naver.maps.LatLng(37.3595704, 127.105399), // 위도 경도
    zoom: 10
  };

  var map = new naver.maps.Map('map', mapOptions);

  // 아래 만든 marker 개체는 지도위에 표시가 될거다. 
  // 아래 만든 marker는 위에서 선언한 map이라는 개체에서 만들어진다.
  // 아래 마커의 position은 아래 명시되어있는 위도 경도 위치에 만들어진다.
  // 그리고 icon의 경우에는 marker라는 class를 가진 div 태그가 표시될 것이다.
  var marker = new naver.maps.Marker({
    map: map,
    position: new naver.maps.LatLng(37.3595704, 127.105399),
    icon: {
      content: "<div class='marker'></div>"
    }
  })
```

```css
.marker {
  width: 24px;
  height: 24px;
  border: 1px solid black;
  border-radius: 50%;
  background-color: green;
  opacity: 0.8;
}
```

## 여러개의 마커 생성하기

1. public 폴더에 data 폴더 생성
2. data 폴더에 data.js 파일 생성

데이터를 별도로 분리해서 관리하는 방법을 알아보도록 하겠다.  

![](/img/image18.jpg)

위도, 경도를 쉽게 알 수 있는 방법은 구글지도를 활용하는 방법이 있다.  

* [구글지도](https://www.google.co.kr/maps/@37.053745,125.6553969,5z?hl=ko)

![](/img/image19.jpg)

남산을 찾고 우클릭을 하시면 위와 같이 뜨는데, 저기서 '이곳이 궁금한가요'를 누르시면 

![](/img/image20.jpg)

위와 같이 위도와 경도가 표시된 팝업을 볼 수 있다.  
해당 위도 경도를 클릭하시고 복사하셔서 붙여넣으면 된다.

```javascript
// /data/data.js
var data = [
    {
        title: "판교",
        content: "미래에셋벤처타워",
        date: "2020-11-08",
        lat: 37.402801, // 위도
        lng: 127.107345, // 경도
    },
    {
        title: "판교",
        content: "단",
        date: "2020-11-08",
        lat: 37.401222,
        lng: 127.107390,
    }
]
```

```javascript
  var mapOptions = {
    center: new naver.maps.LatLng(37.401092, 127.106288), // 위도 경도
    zoom: 15
  };

  var map = new naver.maps.Map('map', mapOptions);

  for (var i in data) {
    var target = data[i];
    var latlng = new naver.maps.LatLng(target.lat, target.lng);

    var marker = new naver.maps.Marker({
      map: map,
      position: latlng,
      icon: {
        content: "<div class='marker'></div>"
      }
    })
  }
```

## info window 생성 준비

커스텀 마커를 사용하는 것이기 때문에 중심좌표를 설정해주는 것이 굉장히 중요하다.  

```css
.marker {
  width: 24px;
  height: 24px;
  border: 1px solid black;
  border-radius: 50%;
  background-color: green;
  opacity: 0.8;
}
```

marker 의 width, height를 각각 24px로 설정해주었기 때문에 아래와 같이 (12, 12)로 중심을 잡아준다.

```javascript
  var mapOptions = {
    center: new naver.maps.LatLng(37.401092, 127.106288), // 위도 경도
    zoom: 15
  };

  var map = new naver.maps.Map('map', mapOptions);

  var markerList = [];
  var infoWindowList = [];

  for (var i in data) {
    var target = data[i];
    var latlng = new naver.maps.LatLng(target.lat, target.lng);
    var marker = new naver.maps.Marker({
      map: map,
      position: latlng,
      icon: {
        content: "<div class='marker'></div>",
        anchor: new naver.maps.Point(12, 12)
      }
    })

    var content = `<div class="infowindow_wrap">
        <div class="infowindow_title">${target.title}</div>
        <div class="infowindow_content">${target.content}</div>
        <div class="infowindow_date">${target.date}</div>
    </div>`;

    var infowindow = new naver.maps.InfoWindow({
      content: content,
      backgroundColor: "#00ff0000", // 투명색 - 이렇게 하는 이유는 해당 info window 의 스타일은 css 파일에서 커스텀할 것이기 때문에 초기화해주는 의미이다.
      borderColor: "#00ff0000",
      anchorSize: new naver.maps.Size(0, 0), // 앵커사이즈는 info window가 뜰 경우 말풍선 꼬리를 뜻하는 것인데 그걸 이번 예제에선 설정하지 않을 것이기 때문에 0,0으로.
    })
  }
```

## info window 만들고 클릭 이벤트 추가하기

```javascript
var mapOptions = {
    center: new naver.maps.LatLng(37.401092, 127.106288), // 위도 경도
    zoom: 15
  };

  var map = new naver.maps.Map('map', mapOptions);

  var markerList = [];
  var infoWindowList = [];

  for (var i in data) {
    var target = data[i];
    var latlng = new naver.maps.LatLng(target.lat, target.lng);
    var marker = new naver.maps.Marker({
      map: map,
      position: latlng,
      icon: {
        content: "<div class='marker'></div>",
        anchor: new naver.maps.Point(12, 12)
      }
    })

    var content = `<div class="infowindow_wrap">
        <div class="infowindow_title">${target.title}</div>
        <div class="infowindow_content">${target.content}</div>
        <div class="infowindow_date">${target.date}</div>
    </div>`;

    var infowindow = new naver.maps.InfoWindow({
      content: content,
      backgroundColor: "#00ff0000", // 투명색 - 이렇게 하는 이유는 해당 info window 의 스타일은 css 파일에서 커스텀할 것이기 때문에 초기화해주는 의미이다.
      borderColor: "#00ff0000",
      anchorSize: new naver.maps.Size(0, 0), // 앵커사이즈는 info window가 뜰 경우 말풍선 꼬리를 뜻하는 것인데 그걸 이번 예제에선 설정하지 않을 것이기 때문에 0,0으로.
    })

    markerList.push(marker);
    infoWindowList.push(infowindow);
  }

  for (var j = 0; j < markerList.length; j++) {
    // 네이버 지도에 이벤트를 설정해주는 방법이다.
    // markerList를 클릭했을 때 getClickHandler 라는 콜백 함수를 실행시키겠다 라는 의미이다.
    naver.maps.Event.addListener(markerList[j], "click", getClickHandler(j));
  }

  function getClickHandler (index) {
    return function () {
      var marker = markerList[index];
      var infowindow = infoWindowList[index];
      if (infowindow.getMap()) { // infowindow가 현재 지도의 띄워져있는지 아닌지를 true / false로 반환
        infowindow.close();
      } else {
        infowindow.open(map, marker); // map의 marker 위에다가 infowindow를 열리게해라.
      }
    }
  }
```

```css
.infowindow_wrap {
  padding: 20px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  background-color: #fff;
}

.infowindow_title {
  font-size: 15px;
  font-weight: bolder;
}

.infowindow_content {
  font-size: 13px;
  font-weight: normal;
}

.infowindow_date {
  font-size: 13px;
  font-weight: normal;
}
```

## 지도 클릭 이벤트 설정하기

```javascript
var mapOptions = {
    center: new naver.maps.LatLng(37.401092, 127.106288), // 위도 경도
    zoom: 15
  };

  var map = new naver.maps.Map('map', mapOptions);

  var markerList = [];
  var infoWindowList = [];

  for (var i in data) {
    var target = data[i];
    var latlng = new naver.maps.LatLng(target.lat, target.lng);
    var marker = new naver.maps.Marker({
      map: map,
      position: latlng,
      icon: {
        content: "<div class='marker'></div>",
        anchor: new naver.maps.Point(12, 12)
      }
    })

    var content = `<div class="infowindow_wrap">
        <div class="infowindow_title">${target.title}</div>
        <div class="infowindow_content">${target.content}</div>
        <div class="infowindow_date">${target.date}</div>
    </div>`;

    var infowindow = new naver.maps.InfoWindow({
      content: content,
      backgroundColor: "#00ff0000", // 투명색 - 이렇게 하는 이유는 해당 info window 의 스타일은 css 파일에서 커스텀할 것이기 때문에 초기화해주는 의미이다.
      borderColor: "#00ff0000",
      anchorSize: new naver.maps.Size(0, 0), // 앵커사이즈는 info window가 뜰 경우 말풍선 꼬리를 뜻하는 것인데 그걸 이번 예제에선 설정하지 않을 것이기 때문에 0,0으로.
    })

    markerList.push(marker);
    infoWindowList.push(infowindow);
  }

  for (var j = 0; j < markerList.length; j++) {
    // 네이버 지도에 이벤트를 설정해주는 방법이다.
    // markerList를 클릭했을 때 getClickHandler 라는 콜백 함수를 실행시키겠다 라는 의미이다.
    naver.maps.Event.addListener(markerList[j], "click", getClickHandler(j));
    naver.maps.Event.addListener(map, "click", clickMap(j));
  }

  function clickMap (index) {
    return function () {
      var infowindow = infoWindowList[index];
      infowindow.close();
    }
  }

  function getClickHandler (index) {
    return function () {
      var marker = markerList[index];
      var infowindow = infoWindowList[index];
      if (infowindow.getMap()) { // infowindow가 현재 지도의 띄워져있는지 아닌지를 true / false로 반환
        infowindow.close();
      } else {
        infowindow.open(map, marker); // map의 marker 위에다가 infowindow를 열리게해라.
      }
    }
  }
```

## 현재 위치 버튼 만들기

```html
<div id="current">현재 위치</div>
```

```css
#current {
  position: absolute;
  top: 180px;
  left: 20px;
  z-index: 10;
  padding: 15px;
  border: 1px solid rgba(0,0,0,.2);
  border-radius: 4px;
  background-color: #fff;
  text-align: center;
  cursor: pointer;
  font-weight: bolder;
}
```

## jQuery 적용 및 사용해보기, 현재 위치 표시하기

* [jQuery site](https://code.jquery.com/)

```javascript
$("#current").on("click", () => {
    if ('geolocation' in navigator) {
        navigator.geolocation.getCurrentPosition(function (position) {
            const lat = position.coords.latitude;
            const lng = position.coords.longitude;
            const latlng = new naver.maps.LatLng(lat, lng);
            const marker = new naver.maps.Marker({
                map: map,
                position: latlng,
            icon: {
                content: '<img class="pulse" draggable="false" unselectable="on" src="https://myfirstmap.s3.ap-northeast-2.amazonaws.com/circle.png">', // drag 불가능, 선택도 불가능
                anchor: new naver.maps.Point(11, 11),
            }
        })
        map.setZoom(15, false); // zoom은 15정도로 하고 이동하는 애니메이션은 주지 않겠다.(false)
        map.panTo(latlng); // 현재위치로 이동
    })
    } else {
        alert("위치정보 사용 불가능");
    }
})
```

## 현재 위치 마커에 css 적용하기


```javascript
const marker = new naver.maps.Marker({
  map: map,
  position: latlng,
  icon: {
    content: '<img class="pulse" draggable="false" unselectable="on" src="https://myfirstmap.s3.ap-northeast-2.amazonaws.com/circle.png">', // drag 불가능, 선택도 불가능
    anchor: new naver.maps.Point(11, 11),
  }
})
```

```css
.pulse {
  display: block;
  width: 22px;
  height: 22px;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 0 0 rgb(255,0,0);
  animation: pulse 1.7s infinite;
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 rgba(204, 49, 44, 0.4);
    -moz-box-shadow: 0 0 0 0 rgba(204, 49, 44, 0.4);
  }
  70% {
    box-shadow: 0 0 0 20px rgba(204, 49, 44, 0);
    -moz-box-shadow: 0 0 0 20px rgba(204, 49, 44, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(204, 49, 44, 0);
    -moz-box-shadow: 0 0 0 0 rgba(204, 49, 44, 0);
  }
}

@-webkit-keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 rgba(204, 49, 44, 0.4);
    -moz-box-shadow: 0 0 0 0 rgba(204, 49, 44, 0.4);
  }
  70% {
    box-shadow: 0 0 0 20px rgba(204, 49, 44, 0);
    -moz-box-shadow: 0 0 0 20px rgba(204, 49, 44, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(204, 49, 44, 0);
    -moz-box-shadow: 0 0 0 0 rgba(204, 49, 44, 0);
  }
}
```

현재위치 최초 1회만 실행되게 처리  
아래 코드도 수정해야될 부분이 있어 보인다.

```javascript
  let currentUse = true;

  $("#current").on("click", () => {
    if ('geolocation' in navigator) {
      navigator.geolocation.getCurrentPosition(function (position) {
        const lat = position.coords.latitude;
        const lng = position.coords.longitude;
        const latlng = new naver.maps.LatLng(lat, lng);
        
        if (currentUse) {
          const marker = new naver.maps.Marker({
            map: map,
            position: latlng,
            icon: {
              content: '<img class="pulse" draggable="false" unselectable="on" src="https://myfirstmap.s3.ap-northeast-2.amazonaws.com/circle.png">', // drag 불가능, 선택도 불가능
              anchor: new naver.maps.Point(11, 11),
            }
          })
          currentUse = false;
        }

        map.setZoom(15, false); // zoom은 15정도로 하고 이동하는 애니메이션은 주지 않겠다.(false)
        map.panTo(latlng); // 현재위치로 이동
      })
    } else {
      alert("위치정보 사용 불가능");
    }
  })
```

## 지도위에 검색창 만들기 - 카카오 api 활용

```html
<div id="search">
  <input type="text" placeholder="목적지를 입력해주세요." id="search_input">
  <button id="search_button">검색</button>
</div>
```

```css
#search {
  position: absolute;
  top: 100px;
  left: 140px;
  z-index: 10;
  padding: 15px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 4px;
  background-color: #fff;
  text-align: center;
}

#search_input {
  border: none;
}

#search_input:focus {
  outline: none;
}
```

## 카카오 api key 발급 및 적용하기

* 네이버에서는 주소를 통해 좌표를 제공해주는 api를 제공해주고 있고,  
* 카카오에서는 키워드 검색, 저희가 일반적으로 지도에서 목적지 검색을 했을 때 좌표를 제공하는 api를 제공해주고 있다.

그래서 해당 지도서비스는 비록 네이버 api를 통해서 지도 구축을 했지만, 이번에는 카카오에서 제공하는 api를 통해서 
목적지 검색을 구현해보도록 하겠다.  

**그렇기 때문에 네이버 지도 api를 적용했을 때처럼 키 발급을 해줘야된다.**  

1. 구글 - '카카오 개발자' 검색 [카카오개발자 사이트](https://developers.kakao.com/)
2. '내 애플리케이션' 클릭
3. 로그인 -> 애플리케이션을 추가할 수 있는 사이트가 나온다.
4. '애플리케이션 추가하기' 클릭
5. 앱 이름 : myfirstmap  
   회사 이름 : myfirstmap
6. 저장

이렇게하면 카카오에서 제공하는 api 서비스들 중 하나를 할당받은게 된다.

![](/img/image21.jpg)

그럼 네이버 API 제공받았을 때처럼 키값을 확인할 수 있는데, 우리가 여기서 필요한 것은 **REST API 키**이다.  
**REST API 키**를 가지고 우리 지도 서비스에 적용해보도록 하겠다.

```html
<script src="https://dapi.kakao.com/v2/maps/sdk.js?appkey=복사한RESTAPI키&libraries=services"></script>
```

```javascript
  let ps = new kakao.maps.services.Places(); // 앞으로 목적지 검색을 하는데 있어서 중요한 역할을 하게되는 함수 중에 하나다.

  $("#search_input").on("keydown", function (e) {
    if (e.keyCode === 13) { // enter key 눌렀을 때,
      let content = $(this).val();
    }
  })
```

## 카카오 api를 활용한 목적지 검색 기능 구현하기

![](/img/image22.jpg)
![](/img/image23.jpg)

이런식으로 검색한 데이터가 json 형태로 전달되는 것을 알 수 있다.  
위도 경도 값도 담겨있는 것을 볼 수 있다.  
카카오 같은 경우는 x에 경도 y에 위도가 담겨있다.  

**배열의 첫번째 값이 검색결과에 가장 근접하다고 인식되어지는 값이다.**  
그렇기 때문에 첫번째 결과값을 지도에 표시해보도록 하겠다.

```javascript
  let ps = new kakao.maps.services.Places(); // 앞으로 목적지 검색을 하는데 있어서 중요한 역할을 하게되는 함수 중에 하나다.

  $("#search_input").on("keydown", function (e) {
    if (e.keyCode === 13) { // enter key 눌렀을 때,
      let content = $(this).val();
      ps.keywordSearch(content, placeSearchCB); // content 를 통해서 api를 요청하게 되고 그거에 대한 결과값이 placeSearchCB 라는 함수를 통해서 처리된다.
    }
  })

  function placeSearchCB (data, status, pagination) {
    // data - 검색결과
    // status - api를 카카오 서버를 활용할 것이기 때문에 그 서버에 대한 상태를 status를 통해 받을 수 있다.
    // pagination - 검색 결과가 얼만큼 있는지 번호를 통해 알 수 있게 해준다.
    if (status === kakao.maps.services.Status.OK) {
      let target = data[0];
      const lat = target.y;
      const lng = target.x;
      const latlng = new naver.maps.LatLng(lat, lng);
      const marker = new naver.maps.Marker({
        map: map,
        position: latlng,
      })
    } else {
      alert("검색 결과가 없습니다.");
    }
  }
```

---

이전 검색결과가 남는 것이 문제다.  
이점도 해결해보자.

```javascript
  let ps = new kakao.maps.services.Places(); // 앞으로 목적지 검색을 하는데 있어서 중요한 역할을 하게되는 함수 중에 하나다.
  let search_arr = [];

  $("#search_input").on("keydown", function (e) {
    if (e.keyCode === 13) { // enter key 눌렀을 때,
      let content = $(this).val();
      ps.keywordSearch(content, placeSearchCB); // content 를 통해서 api를 요청하게 되고 그거에 대한 결과값이 placeSearchCB 라는 함수를 통해서 처리된다.
    }
  })

  $("#search_button").on("click", function () {
    let content = $("#search_input").val();
    ps.keywordSearch(content, placeSearchCB); // content 를 통해서 api를 요청하게 되고 그거에 대한 결과값이 placeSearchCB 라는 함수를 통해서 처리된다.
  })

  function placeSearchCB (data, status, pagination) {
    // data - 검색결과
    // status - api를 카카오 서버를 활용할 것이기 때문에 그 서버에 대한 상태를 status를 통해 받을 수 있다.
    // pagination - 검색 결과가 얼만큼 있는지 번호를 통해 알 수 있게 해준다.
    if (status === kakao.maps.services.Status.OK) {
      let target = data[0];
      const lat = target.y;
      const lng = target.x;
      const latlng = new naver.maps.LatLng(lat, lng);
      const marker = new naver.maps.Marker({
        map: map,
        position: latlng,
      })

      if (search_arr.length === 0) {
        search_arr.push(marker);
      } else {
        search_arr.push(marker);
        let pre_marker = search_arr.splice(0, 1); // splice 메서드는 search_arr 배열 자체에 영향을 끼치는 메서드이다. 맨 앞에값 한개 지운다는 뜻이다.
        pre_marker[0].setMap(null); // 아, setMap 메서드는 naver maps 메서드인가보다. 이전 마커 지우는 역할이다.
      }

      map.setZoom(15, false); // zoom은 15정도로 하고 이동하는 애니메이션은 주지 않겠다.(false)
      map.panTo(latlng); // 현재위치로 이동
    } else {
      alert("검색 결과가 없습니다.");
    }
  }
```