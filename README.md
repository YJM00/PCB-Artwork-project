# 🧠 NE555 Capacitive Sensing Module (Astable Mode)

> NE555를 이용한 정전용량 센싱 모듈 설계 및 PCB 아트웍 프로젝트

---

## 📌 About NE555 Timer IC
<img width="408" height="248" alt="image" src="https://github.com/user-attachments/assets/b00a1449-254c-426f-bb82-b0640908dc95" />

NE555는 내부에 **2개의 비교기(Comparator), RS 래치, 방전 트랜지스터, 출력 드라이버**를 포함한 범용 타이머 IC입니다.

기본적으로 다음 3가지 모드로 동작할 수 있습니다:

- **Astable Mode (비안정 모드)** : 외부 트리거 없이 지속적인 발진 출력
- **Monostable Mode (단안정 모드)** : 트리거 입력 시 일정 시간 펄스 출력
- **Bistable Mode (쌍안정 모드)** : 두 상태 유지 (RS 래치 동작)

본 프로젝트에서는 **Astable 모드**를 사용하여  
정전용량 변화에 따른 발진 주파수 변화를 측정하도록 설계하였습니다.

---


## 📖 1. Schematic Design

<p align="center">
  <img width="522" height="391" alt="image" src="https://github.com/user-attachments/assets/af902b75-aa67-4b04-ad99-b0a409e0b461" />
  <img width="752" height="701" alt="image" src="https://github.com/user-attachments/assets/7c10c282-a8f8-43ef-a10c-30b73a37dcb2" />
</p>

- Astable 모드 구성
- RA, RB, C를 통한 RC 타이밍 설계
- CONT 핀 0.01µF 노이즈 안정화
- RESET 핀 VCC 고정

### ⏱ Astable Mode 동작 원리

- 캐패시터는 1/3 Vcc ~ 2/3 Vcc 사이에서 충·방전 반복
- 내부 비교기와 RS 래치에 의해 OUT 핀이 토글
- 출력은 사각파(Square Wave) 형태



---

## 🧩 2. PCB Layout (Top View)

<p align="center">
  <img width="856" height="807" alt="image" src="https://github.com/user-attachments/assets/82b5bb42-c7e8-439a-8a30-0e867433194d" />
</p>

- 고임피던스 노드 최소 배선
- 디커플링 캐패시터 IC 근접 배치
- 측정용 2Pin Header 배치
- 캐패시터 교체용 소켓 설계

---

## 🖥 3. 3D Viewer

<p align="center">
  <img width="857" height="742" alt="image" src="https://github.com/user-attachments/assets/ff4c0abb-4845-420e-bba3-dbe2ff7810b0" />
</p>

- USB 전원 입력
- 전원 표시 LED
- 2.54mm Header Pin
- Compact Board Design

---

## 📊 4. Oscilloscope Measurement

<p align="center">
  <img width="402" height="455" alt="image" src="https://github.com/user-attachments/assets/af4471ba-2d09-4d18-9b86-df1c10e8b3ea" />
</p>

- Output: Square Wave
- Capacitor Voltage: Exponential Charge/Discharge
- Period 측정 후 C 계산
### 🔢 Timing Equation

\[
t_H = 0.693 (R_A + R_B) C
\]

\[
t_L = 0.693 (R_B) C
\]

\[
T = 0.693 (R_A + 2R_B) C
\]

\[
f = \frac{1.44}{(R_A + 2R_B)C}
\]

정전용량 C가 증가하면 주기 T가 증가하고, 주파수 f는 감소합니다.
\[
C = \frac{T}{0.693 (R_A + 2R_B)}
\]

---

## 5. 구현도 설명
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

## 🎯 6. Applications of Capacitive Sensing Module

본 정전용량 센싱 방식은 다음과 같은 분야에서 활용됩니다:

### 🔹 1. Touch Sensor
- 터치 버튼
- 유리 패널 입력 장치
- 가전제품 터치 인터페이스

### 🔹 2. Proximity Detection
- 비접촉 스위치
- 근접 감지 모듈
- 손 접근 감지

### 🔹 3. Liquid Level Detection
- 물통/탱크 수위 감지
- 비접촉 액체 센싱
- 산업용 레벨 모니터링

### 🔹 4. Presence Detection
- 착석 감지
- 인체 감지 보조 센서
- 간단한 안전 감지 시스템

본 프로젝트는 **정전용량 변화 → 주파수 변화 → 측정 및 계산**의 구조를 이용하여  
센싱의 기본 원리를 이해하는 데 목적이 있습니다.

---


## 7. 개발환경
<img width="1280" height="523" alt="img" src="https://github.com/user-attachments/assets/8dea7cfb-de0a-4c6b-84a8-ac4ef61a1b83" />
