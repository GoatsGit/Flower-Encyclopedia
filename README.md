# Flower-Encyclopedia(꽃 백과사전)
사용자가 사진을 카카오톡 플러스 친구에게 전송하면, 꽃에 대한 설명을 카카오톡 메세지로 사용자에게 전송해주는 챗봇 만들기 프로젝트입니다.

![default](https://user-images.githubusercontent.com/43947747/46646985-613bb200-cbc8-11e8-89e5-7e5e59cb81eb.PNG)

## ★ 이 프로젝트에 필요한 준비물 ★
1. Raspberry Pi3
2. Smart Phone(iOS, Android 모두 가능)
3. KaKao Talk 계정

## ★ 프로젝트 구성도 ★
![image](https://user-images.githubusercontent.com/43947747/46646178-9db8df00-cbc3-11e8-931d-4f227ad1d272.png)

## ★ 개발 내용 ★
1. 카카오톡 api 서버를 구축한 후 카카오톡 플러스 친구를 직접 만들어 서비스를 제공한다.
2. 나만의 데이터로 모델을 재학습 시켜야한다.

## ★ Raspbian OS 환경설정 ★
- Raspbian OS 환경 설정은 [Raspberry Pi 웹사이트](https://www.raspberrypi.org/documentation/installation/installing-images/)를 참고하시오.
- `sudo apt-get uprade` 명령을 먼저 실행시킨 후 `sudo apt-get update` 명령을 실행시켜 OS를 업데이트 하시오.

## ★ 필요한 프로그램과 도구 설치하기 ★
### 1. Tensorflow 설치
 ```sudo apt-get install python3-pip //기본적으로 Raspbian OS에 설치되지만 혹시 모르니 해 볼 것!(python3.x 용)
sudo apt install libatlas-base-dev //Atlas 패키지 설치(Numpy 패키지의 선형대수를 이용하기 위해 필요)
pip3 install tensorflow
```

### 2. node.js 설치 및 작업 준비하기
```sudo apt-get install nodejs
node.js -v // 설치 확인
sudo apt-get install npm

// kakaoChat 디렉토리 생성 후 이동하여 npm으로 패키지를 설치
cd ~
mkdir kakaoChat
cd kakaoChat
npm init

// 작업을 원할하게 하기 위한 패키지를 설치
npm install express
npm install body-parser

// DB는 sqlite 이용
sudo apt-get install sqlite3
npm install sqlite3

mkdir db
cd db
sqlite3 kakaodb.db.database
sqlite3
.open kakaodb.db
CREATE TABLE answer ('id' INTEGER NOT NULL PRIMARY KEY. 'Q' VARCHAR[500] NOT NULL. 'A' VARCHAR[500] NOT NULL);
.quit 입력 후 db와 table 생성을 완료한다.
```

### 3. kakaoChat 디렉토리에 main.js를 생성 후 아래 코드 작성(카카오톡 api가 정상적으로 작동하는지 확인하기 위해)
```var express = require('express');
var http = require('http');
var bodyParser = require('body-parser');
var app = express(); // express 엔진 선언
var exec = require('child_process').exec;

var sqlite3 = require('sqlite3').verbose();
var file = "db/kakaodb.db";
var db = new sqlite3.Database(file);

app.use(bodyParser.urlencoded({extended: false}));// url 인코딩 설정
app.use(bodyParser.json());// json 데이터 수집 설정

// 요청 응답 설정
app.get('/keyboard' , function(req, res){

 var data = {
  'type' : 'buttons',
  'buttons' : ['시작']
 };
 res.json(data);
});

// 요청 응답 설정
app.post('/message' , function(req,res){
 //유저가 입력한 데이터
 console.log(req.body)
 var msg = req.body.content;
 console.log('전달받은 메시지: '+msg);
 var send = {}; //응답할 데 이터
 var command = "";

 switch(msg){
  case '안녕':
  send = {
   'message':{
    'text' :'안녕하세요!\n잘 부탁해요!'
   }
  }
  break;

  case '잘가':
  send = {
   'message':{
    'text' :'다음에 또 오세요!'
   }
  }
  break;

  default:
  send = {
   'message' : {
    'text' : '알수 없는 명령입니다.!'
   }
  }
  break;
 }
 res.json(send); //send변수에 저장된 데이터 전달

});

// 5000포트로 서버 실행
http.createServer(app).listen(process.env.PORT || 5000, function() {
 console.log('5000 port Server Startup..');
 console.log('hello ')
})
```

### 4. 카카오톡 플러스친구 개설하기
[카카오톡 플러스친구 개설하기](https://center-pf.kakao.com/)링크로 접속하여 플러스 친구를 개설한다.
- api를 제작하여 사용하기 위해 `스마트 채팅의 API형으로 설정`해야한다.
- 카카오톡 api 서버와 라즈베리파이가 서로 통신하려면 `[포트포워딩]`(https://blog.naver.com/roboholic84/221052591741)을 하여 해당 포트를 열어놓아야 한다.
