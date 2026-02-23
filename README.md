# PCB-Artwork-project

## 모듈 선정
<img width="755" height="57" alt="image" src="https://github.com/user-attachments/assets/3595ffb3-5a8c-4bee-a6f7-b314ff55e177" />

<img width="522" height="391" alt="image" src="https://github.com/user-attachments/assets/af902b75-aa67-4b04-ad99-b0a409e0b461" />

----
## NE555 심볼 제작
<img width="564" height="613" alt="image" src="https://github.com/user-attachments/assets/cc5aab02-fa3e-4680-afaf-30905d758e77" />

----

## NE555 풋프린트 제작
<img width="578" height="658" alt="image" src="https://github.com/user-attachments/assets/f7b29558-9f30-4e1a-aa59-20f09f7b73e4" />


---
## 회로도
<img width="752" height="701" alt="image" src="https://github.com/user-attachments/assets/7c10c282-a8f8-43ef-a10c-30b73a37dcb2" />

---

## PCB편집기
<img width="856" height="807" alt="image" src="https://github.com/user-attachments/assets/82b5bb42-c7e8-439a-8a30-0e867433194d" />


---

## 3D뷰어
<img width="857" height="742" alt="image" src="https://github.com/user-attachments/assets/ff4c0abb-4845-420e-bba3-dbe2ff7810b0" />


---

## 구현도 설명
① 회로도 편집기

1.NE555 소자의 심볼을 직접 제작하여 사용하였다.

2.오실로스코프를 통한 오실레이션 측정을 위해 2.54Pitch 2Pin HeaderPin 심볼을 추가하였다.

3.손쉽게 캐패시터를 교체할 수 있도록 2.54Pitch 2Pin HeaderSocket 심볼을 추가하였다.

4.전원 공급은 USB 2.0 A Connector 심볼을 이용하여 외부에서 받을 수 있도록 구성하였다.

5.전원이 인가되는지를 확인할 수 있도록 스루홀 타입 LED 1개를 추가하였다.

6.전체 회로는 Astable(비안정) 모드로 NE555 주변회로를 구성하였으며, 저항/캐패시터 소자의 값은 직접 계산하여 결정하였다. 결정 근거는 보고서에 기술하였다.

② PCB 편집기

1.NE555 소자의 풋프린트를 직접 제작하였다.

2.8Pin SOIC Package를 기준으로 풋프린트를 구성하였다.

3.PCB 보드의 외곽 크기는 5 cm × 5 cm로 설정하였고, 모서리 부분에는 모깎기를 적용하였다.

4.PCB 보드의 네 귀퉁이에 마운팅 홀 4개를 배치하였다.

5.저항/캐패시터는 2012 [mm] (0805 [inch]) 사이즈의 SMD 타입 풋프린트를 사용하였다.

6.모든 배선(선폭: 0.5mm)을 마친 후, Copper pour를 앞/뒷면 모두에 GND 기준으로 적용하였다.

7.PCB Bottom 면에는 학번과 이름을 실크스크린으로 표기하였다.

8.마지막으로 PCB 제작 외주를 위한 Gerber 파일을 생성하였다.

---
## 개발환경
<img width="1280" height="523" alt="img" src="https://github.com/user-attachments/assets/8dea7cfb-de0a-4c6b-84a8-ac4ef61a1b83" />

