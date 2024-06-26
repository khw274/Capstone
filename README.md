# 캡스톤디자인
4-1/전자공학전공 캡스톤디자인 결과물

```🏆제2회 KOVA 캡스톤디자인 경진대회 입선, (사)벤처기업협회대구경북지회장상🏆```  
```캡스톤디자인 작품 전시회```  
```2023 벤처 기업인의 밤 시상식 및 수상작 부스 운영```

<img src="https://github.com/khw274/Capstone/assets/125671828/5482591b-1cf4-41c4-bc61-caceb55c60c4" width="300" height="340"/> <img src="https://github.com/khw274/Capstone/assets/125671828/facc7f16-7fa6-4f9b-a125-d13bed2717e9" width="300" height="340"/> <img src="https://github.com/khw274/Capstone/assets/125671828/36480f70-d709-41d3-abcf-ca4d3334c6bb" width="300" height="340"/>



## 아이디어 
### 전기차충전기용 비전인식 시스템
#### - 아이디어 선정 배경 
㈜채비, 전기차 충전 통합 솔루션을 개발하는 회사와 협업할 수 있는 좋은 기회를 얻었고, 서로 지향하는 개발 방향이 일치해 아이디어를 정하였다.

아이디어의 핵심은 차량의 번호판을 인식하면 등록된 사용자 정보를 불러옴으로써 기존의 전기차 충전기의 충전 순서를 생략하여 더욱 편리하고 빠른 전기차 충전시스템을 구축하는 것이다.

팀원과의 역할은 충전기 구조물 제작 / 충전 인터페이스 디자인 및 번호판 제작 / SW 설계 및 임베디드로 구분하여 진행하였다.
  
내가 맡은 역할은 ```SW 설계 및 동작 확인, 임베디드``` 이다.


## 개발 과정
### 공통
#### - 아이디어 구체화
전체적인 아이디어의 방향은 정해진 상태이기 때문에 최종 구현 목표를 정하고자 함.

캡스톤디자인의 기간은 한 학기로 정해져있어 짧은 편이고 실제 제작 기간은 3개월 남짓이기에 구현 목표 설정이 중요했다.

원래 목표는 채비의 전기차 충전기와 연계하여 실제로 테스트를 하고 싶었지만, 예산 부족과 시간적인 제한이 상당했다. 

따라서 멘토분과의 논의 끝에 OpenCV를 활용해 번호판 텍스트를 인식하고 준비해놓은 차량 DB와 실제 충전 인터페이스를 구현한 영상을 불러오는 것을 최종목표로 하였다.

### SW / 임베디드
#### - 부품 및 개발 언어 선정
##### 1. 개발 언어 선정
   
  C언어와 PYTHON 둘 중 하나로 정하기로 했다.
  
  C언어는 실행속도가 더 빠르다는 장점이 있지만. 그동안 출전한 경진대회에서 PYTHON을 주로 사용했기에 더 사용하기 쉽고 익숙한 PYTHON을 개발 언어로 선정하였다.

##### 2. MCU 선정

   전기차 충전기용 비전인식 시스템을 개발하기에 앞서 프로그램을 설계하고 구동하기 위해 라즈베리파이4(Raspberry Pi 4 Model B)를 MCU로 선정했다.

   아두이노와 라즈베리파이 중에서 고민을 했었지만, 아두이노는 C언어를 기반으로 사용하고 라즈베리파이는 C언어 뿐만 아니라 JAVA, PYTHON 등 여러 언어를 사용하는 장점이 있다. 개발 언어로 선정한 PYTHON을 더 용이하게 사용하기 위해 라즈베리파이를 사용하기로 했다. 
   
   또한 이전에 라즈베리파이 활용 및 코딩 교육을 수료한 경험도 선택에 있어서 큰 영향을 주었다.   
   <img src="https://github.com/khw274/Capstone/assets/125671828/e031429a-bf32-4e90-a1ee-135e062d7bb7" width="250" height="250"/>

##### 3. 기타 부품 선정

  카메라: 차량의 번호판을 인식하기 위해 L사의 웹캠을 사용했다. 초기에 라즈베리파이 카메라를 사용하려 했지만 외관상의 문제와 각도 조절의 이점 등의 이유로 변경하게 되었다.

  스위치 센서: 프로그램을 구동시킬 수 있도록 라즈베리파이와 연결하기 용이한 구조의 버튼형 스위치 센서(VCC, GND, INPUT 구조)로 선정함.

  모니터: 라즈베리파이 전용 모니터를 구매하려고 했지만 구매할 수 없는 부품이라고 학교측에서 연락을 받았다.  그 대안으로 학교에서 S사 태블릿 PC를 대여받을 수 있었다.

  
#### - 프로그램 설계
코드를 짜기 전 다음과 같은 5개의 틀로 코드의 구성을 계획함. 
1. 스위치 센서
2. 카메라 작동 및 촬영/저장
3. 촬영된 파일을 불러온 뒤 번호 추출
4. 추출된 번호에 따라 적합한 영상 실행
5. 저장된 image를 삭제하고 초기화

최종. 라즈베리파이와 태블릿 연결

##### 1. 스위치 센서
  사용자가 전기차 충전기 앞에 주차를 한 후 스위치를 눌러 프로그램을 동작시키는 방법으로 구상을 했기에 스위치 센서는 필수적인 요소이다.

  직관성 있고 뚜렷한 형태, 그리고 라즈베리파이와의 연결을 위해 (VCC, GND, INPUT) 구조로 구성된 스위치 센서를 사용했다.  
  <img src="https://github.com/khw274/Capstone/assets/125671828/33540e10-fcd2-46a1-a645-bef2583eabcf" width="250" height="250"/>


  라즈베리파이에는 용도별로 GPIO핀이 구성되어 있다. 브레드보드를 이용해 라즈베리파이와 스위치 센서의 전원(VCC), 접지(GND), 입력(INPUT)을 서로 연결하였다.  
  <img src="https://github.com/khw274/Capstone/assets/125671828/ac4e6b82-3dce-44a3-b4d4-64138fd459ab" width="400" height="400"/>  <img src="https://github.com/khw274/Capstone/assets/125671828/8424dd25-ae0f-4f1d-bcc4-2f13f23cae89" width="400" height="400"/>
  
  사용했던 핀을 색깔별로 표시해두었다.(초록색: INPUT, 빨간색: 라즈베리파이 연결, 파란색: 스위치 센서 연결)
  
  스위치 센서의 입력값이 들어올 핀은 18번으로 설정했다. 

  이제 스위치 센서 입력값을 불러올 코드를 설계해야 한다.

```python
import RPi.GPIO as GPIO  # 라즈베리파이 GPIO 제어 라이브러리

GPIO.setmode(GPIO.BCM)  # GPIO 핀 번호 체계를 BCM 모드로 설정
GPIO.setup(18, GPIO.IN, GPIO.PUD_UP)  # GPIO 18번 핀을 입력 모드로 설정하고 풀업 저항 활성화

while 1:  # 무한 루프 시작
    x = GPIO.input(18)  # GPIO 18번 핀의 입력 값을 읽어 변수 x에 저장
    # print(x)  # 디버깅용: 스위치가 눌리면 x = 0, 눌리지 않으면 x = 1

    if x == 0:  # 스위치가 눌렸을 때
        print('스위치 ON')  # '스위치 ON' 메시지 출력

        # 이후 코드들 실행
```
라즈베리파이 GPIO 제어 라이브러리를 불러오고 실제 핀과 동일하게 사용할 수 있도록 BCM 모드로 설정했다.

18번핀의 입력값을 우선 확인해야 하는데, 스위치를 켰을 시 LOW(0), 스위치를 껐을 시 HIGH(1)를 출력하는 것을 print를 통해 확인.

그 후 조건문을 통해 스위치를 눌렀을 시 이후 코드들을 모두 작동할 수 있도록 설계했다.

##### 2. 카메라 
다음은 자동차 번호판 인식을 위한 카메라를 라즈베리파이와 연결하고, 이미지를 촬영하고 지정한 이름으로 저장하는 코드를 설계해야 한다.   

<img src="https://github.com/khw274/Capstone/assets/125671828/b361163e-b686-4c73-b774-4b7b413ba983" width="380" height="380"/>  

USB 형태로 라즈베리파이에 쉽게 연결할 수 있는 구조이며 위아래로 각도 조절이 가능해 위치를 조절하는데 용이한 장점이 있었다.

카메라를 연결했으므로 연결이 잘 됐는지 작동 테스트를 위해 코드를 설계하였다.

코드를 설계하기 전 기본적으로 라즈비안에 OpenCV 4.5.5 버전을 설치했다.
```python
import time, cv2, os
import numpy as np

# 카메라 초기화 및 설정
cap = cv2.VideoCapture(0)
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 1920)  # 카메라 해상도 너비 설정
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 1080)  # 카메라 해상도 높이 설정

# 이미지 캡처 및 표시
ret, image = cap.read()  # ret: 이미지 읽기 성공 여부, image: 캡처된 이미지
if ret == True:
    cv2.imshow('CAMERA', image)  # 캡처된 이미지 창에 표시
    img_captured = cv2.imwrite('test.jpg', image)  # 이미지 파일로 저장
    resize_img = cv2.resize(image, (1435, 800))  # 이미지 크기 조정
    cv2.imshow('CAMERA', resize_img)  # 조정된 이미지 창에 표시
    cv2.waitKey(3500)  # 3.5초 대기 (밀리초 단위)

# 자원 해제
cap.release()  # 카메라 자원 해제
cv2.destroyAllWindows()  # 모든 OpenCV 창 닫기

time.sleep(1)  # 1초 대기 
```
코드는 다음과 같다. 

카메라의 해상도과 너비를 기본적으로 설정해두고 이미지 잘 읽어들이면 캡처된 이미지를 창에 표시해 확인할 수 있도록 했다.

처음 코드를 실행했을시 이미지가 화면보다 훨씬 작게 표시가 되어 여러번 이미지 크기를 재조정해 resize된 이미지를 띄워 사이즈 문제를 해결하였다.  
<img src="https://github.com/khw274/Capstone/assets/125671828/99aa23f3-a7d5-4962-93d9-286f602b031b" width="380" height="480"/>  <img src="https://github.com/khw274/Capstone/assets/125671828/7152c736-953f-4782-b028-5e50304618c5" width="380" height="480"/>       
사진은 사이즈 조절 전으로 카메라가 잘 작동되고 이미지 촬영 또한 정상 작동되는 것을 확인할 수 있었다.

##### 3. 번호 추출
이제 자동차 번호판을 인식하고 번호를 추출할 차례이다.

해당 코드를 작성하면서 오류가 많이 발생했다. 수많은 디버깅과 확인 작업을 해가면서 코드를 설계하느라 꽤나 긴 시간이 소요되었다.

```python
~~코드 설명~~
```


##### 4. 영상 실행
자동차 번호판 번호를 정상적으로 추출이 되었으면 이제 번호에 적합한 충전 인터페이스를 실행할 차례이다.

```python
if '77차1004' in chars:  # '77차1004'가 입력된 경우
    print('          * 인식 성공 *')  # '인식 성공' 메시지를 출력

    file = open('77차1004.txt', mode='r')  # '77차1004.txt' 파일을 읽기 모드로 오픈
    print(file.read()) 

    Vid = cv2.VideoCapture('car1.mp4')  # 미리 저장해둔 'car1.mp4' 비디오 파일을 읽어옴

    # 비디오가 열렸는지 확인하고, 속성들을 변수에 저장합니다.
    if Vid.isOpened():  
        fps = Vid.get(cv2.CAP_PROP_FPS)  # 프레임 속도
        f_count = Vid.get(cv2.CAP_PROP_FRAME_COUNT)  # 프레임 수
        f_width = Vid.get(cv2.CAP_PROP_FRAME_WIDTH)  # 프레임 너비
        f_height = Vid.get(cv2.CAP_PROP_FRAME_HEIGHT)  # 프레임 높이

    # 비디오가 열려있는 동안 실행
    while Vid.isOpened():
        ret, frame = Vid.read()  # 비디오에서 프레임을 읽어옵니다.
        if ret:  # 프레임을 성공적으로 읽어왔다면,
            # 프레임 크기를 조정함
            re_frame = cv2.resize(frame, (round(f_width / 1.33), round(f_height / 1.35)))
            # 조정된 프레임을 화면에 표시합니다.
            cv2.imshow('Car_Video', re_frame)
            key = cv2.waitKey(10)  # 키 입력을 대기하며, 10밀리초마다 프레임을 업데이트합니다.

            if key == ord('q'):  # 'q' 키가 눌리면,
                break  # 비디오 재생을 멈춥니다.
        else:
            break  # 프레임을 더 이상 읽어올 수 없으면 비디오 재생을 멈춥니다.
    Vid.release()  # 비디오 장치를 닫습니다.
    cv2.destroyAllWindows()  # 모든 OpenCV 창을 닫습니다.

elif '96쇼2962' in chars:  # 두 번째 차
    print('          * 인식 성공 *')

    file = open('96쇼2962.txt', mode = 'r')
    print(file.read())

    Vid = cv2.VideoCapture('car2.mp4')  # 두 번째 차 인터페이스

    if Vid.isOpened():
        fps = Vid. get(cv2.CAP_PROP_FPS)
        f_count = Vid.get(cv2.CAP_PROP_FRAME_COUNT)
        f_width = Vid.get(cv2.CAP_PROP_FRAME_WIDTH)
        f_height = Vid.get(cv2. CAP_PROP_FRAME_HEIGHT)

    while Vid.isOpened() :
        ret, frame = Vid. read() 
        if ret:
            re_frame = cv2.resize(frame, (round(f_width/1.33), round(f_height/1.35)))
            cv2.imshow('Car_Video',re_frame)
            key = cv2.waitKey(10)

            if key == ord('q'):
                break
            
        else:
            break
    Vid.release()
    cv2.destroyAllWindows()

elif '86타8558' in chars:  # 세 번째 차
    print('          * 인식 성공 *')

    file = open('86타8558.txt', mode = 'r')
    print(file.read())

    Vid = cv2.VideoCapture('car3.mp4')  # 세 번째 차 인터페이스

    if Vid.isOpened():
        fps = Vid. get(cv2.CAP_PROP_FPS)
        f_count = Vid.get(cv2.CAP_PROP_FRAME_COUNT)
        f_width = Vid.get(cv2.CAP_PROP_FRAME_WIDTH)
        f_height = Vid.get(cv2. CAP_PROP_FRAME_HEIGHT)

    while Vid.isOpened() :
        ret, frame = Vid. read() 
        if ret:
            re_frame = cv2.resize(frame, (round(f_width/1.33), round(f_height/1.35)))
            cv2.imshow('Car_Video',re_frame)
            key = cv2.waitKey(10)

            if key == ord('q'):
                break
            
        else:
            break
    Vid.release()
    cv2.destroyAllWindows()
    
else:
    print('인식 실패')  # 인식 실패시 '인식 실패' 를 출력

time.sleep(1)
```
추출한 문제에 맞게 미리 준비한 영상을 불러와 화면에 띄웠으며 화면 크기에 맞게 프레임을 조정했다.  
![image](https://github.com/khw274/Capstone/assets/125671828/5135af75-da6b-4bb3-a028-f3cc4d0f577f)  
다음과 같이 번호판 인식 후 제작 영상이 불러와지는 것을 확인할 수 있다.


##### 5. 초기화
마지막으로 다음 프로그램을 언제든지 실행할 수 있도록 하는 초기화 작업이 필요하다.

초기화 방법을 고민하다가 항상 같은 이름의 파일명을 가져와서 사용하는 코드의 특성을 활용해 저장한 파일을 삭제하는 방법을 선택했다.
```python
# 파일 삭제(초기화)
file = 'test.jpg'
if os.path.exists(file):
    os.remove(file)
    # print('파일삭제 완료')


break
```
정해둔 파일을 삭제하는 간단한 코드로 초기화를 진행했다

##### 최종. 라즈베리파이와 태블릿 연결
이제 코드 설계가 끝나고 시각적으로 사용자에게 보여줄 수 있도록 태블릿과 라즈베리파이를 연결하는 작업이 남았다.

태블릿과 라즈베리파이를 연결하기 위해 VNC Viewer를 사용했다.

VNC VIEWER로 연결하기 위해 다음과 같은 기초 설정이 필요하다.
![image](https://github.com/khw274/Capstone/assets/125671828/2a4dd0b5-9e2a-4ab0-82c6-00f369ea9811)  
```
adb devices  # Android Debug Bridge(ADB)를 사용하여 연결된 Android 디바이스 목록을 표시하는 명령,
               정상적으로 연결되었으면 해당 디바이스의 고유 식별자가 목록에 표시된다

adb reverse tcp:5900 tcp:5900  # 로컬(노트북)의 TCP 포트와 장치(태블릿)의 TCP 포트를 VNC에 사용하는 5900 포트로 설정,
                                 즉 두 장치의 TCP 포트 번호를 통일시켜 VNC 서버에 접속할 수 있도록 함
```

VNC 사용 설정을 했으니 이제 VNC View를 사용해 라즈베리파이에 접속할 차례이다.

외부 장치에서 라즈베리파이에 접속을 하려면 같은 공유기를 사용해야 하는데. 이유는 공유기가 연결된 라즈베리파이, 노트북 등에 고유 IP 주소를 할당해주기 때문이다.

기본적으로 나는 쓸만한 모니터 장치가 없었기에 핫스팟을 이용해 노트북으로 라즈베리파이에 원격접속을 했었다. 그 방법과 상당히 유사한 방법을 사용해서 수월하게 해결할 수 있었다.

내가 사용한 방법을 단계별로 정리해보았다.

1. 우선 노트북을 인터넷 환경에 접속시킨다.
2. 라즈베리파이에 미리 설정한 SSID와 PSK와 동일하게 노트북 핫스팟을 설정해 라즈베리파이와 노트북이 동일한 핫스팟에 연결될 수 있도록 한다.
3. 핫스팟에 연결된 라즈베리파이 정보를 보면 IP 주소를 확인할 수 있는데, 해당 IP를 사용해 VNC VIEWER로 라즈베리파이에 접속한다.
4. 짜잔 라즈베리파이 화면을 태블릿으로 볼 수 있게 된다.

![image](https://github.com/khw274/Capstone/assets/125671828/9de9d11a-2562-483e-90a9-9bdfbabc9c90)

### 충전기 구조물 제작
충전기 구조물 제작에 있어서 차량 번호판의 위치 파악과 사용자가 사용하기 편리한 위치에 화면을 부착하는 것이 중요 포인트이다. 

따라서 구조물의 정확한 위치를 재기 위해 차량 별 평균적인 번호판 위치를 측정하고, 측정한 값들을 기반으로 정확한 규격의 구조물 모델링 작업을 실시했다.   
<img src="https://github.com/khw274/Capstone/assets/125671828/062b8f0b-3e57-4e01-827b-a2fab8897c7c" width="250" height="300"/>

인터페이스 역할을 할 태블릿과 카메라, 라즈베리파이 설치를 위해 정면에서 보이지 않는 위치에 거치대를 구조하고 단단하게 고정할 수 있도록 구조물 3D 도면을 설계했다.

기구물은 전기차 충전기를 소형화한 것이므로 실내 뿐만 아니라 야외에서도 차질 없이 사용되어야 하는 점을 고려, 밑면과 윗면에 넓은 면적의 지지대를 부착해 넘어짐을 방지했다.

외부 충격에도 파손되지 않아야 하고 데모 영상 촬영과 전시회 개최를 위해 이동에 용이한 가벼운 재질이어야 한다. 그에 적합한 폴리카보네이트(PC)를 사용해 구조물을 제작했다.  
![image](https://github.com/khw274/Capstone/assets/125671828/05e6c0c7-3244-4e18-bf9c-7d4c94d45efa)


### 충전 인터페이스 디자인 및 번호판 제작
#### - 충전 인터페이스 디자인
번호 인식을 끝내고 전기차 충전 과정을 구현한 충전 인터페이스를 송출해야 한다. 사용자가 본인의 개인정보와 충전과정을 한 눈에 알아보기 쉽도록 인터페이스 화면 디자인을 구성하였다.   
<img src="https://github.com/khw274/Capstone/assets/125671828/a7f1b41a-59b6-47af-92da-e67a365dad10" width="330" height="200"/> <img src="https://github.com/khw274/Capstone/assets/125671828/7e256425-f7ae-44bd-aa11-b5efa0e9f794" width="330" height="200"/> <img src="https://github.com/khw274/Capstone/assets/125671828/f1f95c02-04bf-4067-b091-a1928517aa74" width="330" height="200"/>

#### - 번호판 제작
차량 번호는 현재 존재하지 않는 번호판 한글 문자인 "차, 타, 쇼"를 넣어 제작했다.
![image](https://github.com/khw274/Capstone/assets/125671828/14d58198-0f1d-4f8b-a810-80db84da1a9a)


번호판은 실제 전기차 번호판 규정에 맞춰 파란색 바탕에 검은색 문자로 제작하였으며 크기는 520 x 110(mm)에 맞춰서 제작했다.

또한 실제 번호판과 동일하게 숫자는 D-DIN 서체, 한글은 헤드라인M을 사용해 제작했고 규격에 맞춰 디자인 후 프린트하여 우드락에 부착했다.
<img src="https://github.com/khw274/Capstone/assets/125671828/c266cdd1-7ad2-4886-9a54-35bc0f3a9831" width="450" height="400"/>

## 최종 
최종적으로 캡스톤 발표를 위해 실제 차를 렌트해 데모 영상을 촬영하였다.

전시회 등에서 실제 차를 끌고 갈 수는 없기에 영상을 촬영하는 방법을 선택했다.

차량 앞에 충전기 구조물을 설치했고 실제 충전기 사용과 최대한 비슷하게 구현하기 위해 노력했다.

차량을 직접 운전해 주차하고 스위치를 눌러 프로그램을 구동시키는 과정을 영상에 담았다.  
<img src="https://github.com/khw274/Capstone/assets/125671828/2fd9297d-d761-422f-a50c-a4759335c96b" width="400" height="550"/> <img src="https://github.com/khw274/Capstone/assets/125671828/ffcee714-0c5e-4178-b1fd-a92cf02cb02b" width="400" height="550"/>  
죄측 사진은 완성된 구조물 모습이고 우측 사진은 구조물 뒤 설치한 장치의 모습이다. 위로는 모니터를 부착해놓았다.

최종적으로 영상을 제작했으며 영상의 구성은 아래와 같은 과정으로 이루어져있다.
1. 프로젝트 소개
2. 기존 전기 자동차 충전기 작동 메뉴얼
3. 전기차 충전기용 비전인식 시스템 데모 영상
4. 비전인식 시스템 설계 코딩 설명
5. 번호판별 비전인식 데모 영상

캡스톤 디자인을 하면서 가장 어려웠던 부분은 코드를 수정할 때마다 발생하는 오류를 고치는 것이었다.

하지만 오랜 시간을 투자해 고쳐나갔고 팀원들과의 효과적인 분업 끝에 완성까지 도달할 수 있었다고 생각한다. 

  
