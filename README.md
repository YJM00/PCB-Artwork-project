# 🧠 NE555 Capacitive Sensing Module (Astable Mode)

> NE555를 이용한 정전용량 센싱 모듈 설계 및 PCB 아트웍 프로젝트

---

## 📌 About NE555 Timer IC
<img width="1040" height="488" alt="image" src="https://github.com/user-attachments/assets/85df0124-470d-487d-9564-da83c68ea6ea" />


NE555는 내부에 **2개의 비교기(Comparator), RS 래치, 방전 트랜지스터, 출력 드라이버**를 포함한 범용 타이머 IC입니다.

기본적으로 다음 3가지 모드로 동작할 수 있습니다:

- **Astable Mode (비안정 모드)** : 외부 트리거 없이 지속적인 발진 출력 (발진기)
- **Monostable Mode (단안정 모드)** : 트리거 입력 시 일정 시간 펄스 출력 (타이머)
- **Bistable Mode (쌍안정 모드)** : 두 상태 유지 (RS 래치 동작)

본 프로젝트에서는 **Astable 모드**를 사용하여  
정전용량 변화에 따른 발진 주파수 변화를 측정하도록 설계하였습니다.

---


## 📖 1. Schematic Design

  <img width="522" height="391" alt="image" src="https://github.com/user-attachments/assets/af902b75-aa67-4b04-ad99-b0a409e0b461" />
  <img width="752" height="701" alt="image" src="https://github.com/user-attachments/assets/7c10c282-a8f8-43ef-a10c-30b73a37dcb2" />

- Astable 모드 구성
- RA, RB, C를 통한 RC 타이밍 설계
- CONT 핀 0.01µF 노이즈 안정화
- RESET 핀 VCC 고정



## 🔄 1-1. Operating Flow (Astable Mode)

### 🧭 동작 흐름

1️⃣ 전원 인가 (VCC 공급)  
2️⃣ 캐패시터 C가 1/3 Vcc 이하 → TRIG 비교기 동작  
3️⃣ RS 래치 SET → OUT = HIGH  
4️⃣ DISCH 트랜지스터 OFF → C 충전 시작  
5️⃣ C 전압이 2/3 Vcc 도달  
6️⃣ THRES 비교기 동작  
7️⃣ RS 래치 RESET → OUT = LOW  
8️⃣ DISCH 트랜지스터 ON → C 방전  
9️⃣ C 전압이 다시 1/3 Vcc 이하  
🔁 2번으로 반복 (발진 지속)


### 📊 전압 변화 요약

- 캐패시터 전압 : 1/3 Vcc ↔ 2/3 Vcc 반복
- 출력 : HIGH ↔ LOW 토글
- 발진 주기 : RC 값에 의해 결정



---

## 🧩 2. PCB Layout (Top View)

<p align="center">
  <img width="856" height="807" alt="image" src="https://github.com/user-attachments/assets/82b5bb42-c7e8-439a-8a30-0e867433194d" />
</p>


---

## 🖥 3. 3D Viewer

<p align="center">
  <img width="857" height="742" alt="image" src="https://github.com/user-attachments/assets/ff4c0abb-4845-420e-bba3-dbe2ff7810b0" />
</p>


---

## 📊 4. Oscilloscope Measurement

<p align="center">
  <img width="402" height="455" alt="image" src="https://github.com/user-attachments/assets/af4471ba-2d09-4d18-9b86-df1c10e8b3ea" />
</p>

- Output: Square Wave
- Capacitor Voltage: Exponential Charge/Discharge
- 스코프로 출력 전압값 주기 측정 후 캐패시턴스 계산


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
C = T/(0.693 (R_A + 2R_B))
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

## 6.🧠 NE555 활용 예

### 🔁 1) Astable Mode (비안정 모드, 발진기)

> 외부 트리거 없이 지속적으로 HIGH/LOW를 반복하며 **사각파(Square Wave)** 를 생성하는 모드

**✅ 활용 예시**
- **Clock / Pulse Generator** : 카운터, 쉬프트레지스터 등 디지털 회로 테스트용 클럭
- **LED Blinker / Flasher** : 상태 표시용 점멸 회로
- **PWM Generator** : 간단한 모터 속도 제어, LED 밝기 조절
- **Tone / Buzzer Driver** : 경고음(사이렌) 및 간단 신호음 발생
- **Frequency-based Sensing** : RC 변화(정전용량/저항)에 따른 주파수 변화 측정


### ⏱ 2) Monostable Mode (단안정 모드, Timer / One-shot)

> 트리거 입력이 들어오면 한 번만 HIGH 펄스를 출력하고,  
> 설정된 시간이 지나면 자동으로 LOW로 복귀하는 **원샷(One-shot) 타이머** 모드

**✅ 활용 예시**
- **Delay Timer** : 전원 인가 후 일정 시간 지연 후 동작(릴레이/부저/Enable)
- **Pulse Generator** : 버튼 입력을 일정한 펄스 폭으로 변환
- **Debounce / Pulse Stretching** : 스위치 바운스 제거, 짧은 신호를 길게 만들어 MCU가 읽기 쉽게
- **Power-On Reset (POR) 보조** : 특정 시점까지 시스템을 강제 대기시키는 신호 생성

---

## 🎯 7. Applications of Capacitive Sensing Module

본 정전용량 센싱 방식은 사람/물체가 접근시 정전용량이 변화하는 원리를 이용하여 다음과 같은 분야에서 활용됩니다:

### 🔹 1. Touch Sensor
- 터치 버튼
- 유리 패널 입력 장치
- 가전제품 터치 인터페이스

### 🔹 2. Proximity Detection
- 비접촉 스위치
- 근접 감지 모듈
- 손 접근 감지

1. 터치 감지 2. 근접감지 용도로 활용됨

---


## 8. 개발환경
<img width="1280" height="523" alt="img" src="https://github.com/user-attachments/assets/8dea7cfb-de0a-4c6b-84a8-ac4ef61a1b83" />
