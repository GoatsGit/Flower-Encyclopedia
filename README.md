# Flower-Encyclopedia(꽃 백과사전)
사용자가 사진을 카카오톡 플러스 친구에게 전송하면, 꽃에 대한 설명을 카카오톡 메세지로 사용자에게 전송해주는 챗봇 만들기 프로젝트입니다.

![image](https://user-images.githubusercontent.com/43947747/46928029-73f43200-d073-11e8-8c26-8577c0ede4b9.png)
![image](https://user-images.githubusercontent.com/43947747/46928033-7f475d80-d073-11e8-9a72-d926d8d8f418.png)
![image](https://user-images.githubusercontent.com/43947747/46928044-879f9880-d073-11e8-89c7-157b29cbec5a.png)
![image](https://user-images.githubusercontent.com/43947747/46928054-91c19700-d073-11e8-925a-99b14316f5ae.png)
![image](https://user-images.githubusercontent.com/43947747/46928110-e06f3100-d073-11e8-87d9-8993d130247a.png)
![image](https://user-images.githubusercontent.com/43947747/46928129-ef55e380-d073-11e8-96de-fbb3a8dface5.png)
![image](https://user-images.githubusercontent.com/43947747/46928157-1c09fb00-d074-11e8-926b-3af5b8245b80.png)

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
- 카카오톡 api 서버와 라즈베리파이가 서로 통신하려면 [`포트포워딩`](https://blog.naver.com/roboholic84/221052591741)을 하여 해당 포트를 열어놓아야 한다.

## 참고 문헌
- [카카오톡 챗봇 만들기](https://blog.naver.com/roboholic84/221361971666)
- [라즈베리파이를 이용하여 사물을 설명해보자](https://blog.naver.com/zeta0807/221300685644)
