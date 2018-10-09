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
- Raspbian OS 환경 설정은 [Raspberry Pi 웹사이트](https://www.raspberrypi.org/)를 참고하시오.
- 표준시간대 설정은 필수이니 변경하시오.
- `sudo apt-get uprade` 명령을 먼저 실행시킨 후 `sudo apt-get update` 명령을 실행시켜 OS를 업데이트 하시오.

## ★ 필요한 프로그램과 도구 설치하기 ★
```
sudo apt-get install python3-pip
sudo pip3 install chainer==1.19.0
sudo pip3 install scipy
sudo pip3 install h5py
sudo apt-get install python-h5py
sudo apt-get install libopen-jp2-7-dev
sudo apt-get install libtiff5
sudo pip3 install Pillow
sudo apt-get install libatlas-base-dev
```
