# ETA, 선박 일정은 왜 자꾸 늦어질까?
## 물류 데이터 엔지니어 관점에서 본 ETA 불일치, 항만 병목, 공급망 가시성의 실질적 가치

## Article Information
- Source: Tradlinx
- Title: ETA, 선박 일정은 왜 자꾸 늦어질까? 데이터로 본 물류 가시성의 실질적 가치와 대안
- Article: [Read the original article](https://www.tradlinx.com/blog/market-trend/eta-%ec%84%a0%eb%b0%95-%ec%9d%bc%ec%a0%95%ec%9d%80-%ec%99%9c-%ec%9e%90%ea%be%b8-%eb%8a%a6%ec%96%b4%ec%a7%88%ea%b9%8c-%eb%8d%b0%ec%9d%b4%ed%84%b0%eb%a1%9c-%eb%b3%b8-%eb%ac%bc%eb%a5%98-%ea%b0%80/)
- Date Reviewed: 2026-04-21

---

## 1. Why I Chose This Article

이 기사를 고른 이유는 ETA 문제가 단순히 “배가 늦는다”는 운영 불편이 아니라,  
물류 데이터 엔지니어 입장에서는 **예측 정확도, 이벤트 반영, 항만 병목, 비용 전가 구조**가 모두 연결된 문제이기 때문이다.

특히 이 기사는 다음 질문으로 이어진다.

- 왜 선박 ETA는 계속 틀어지는가?
- 왜 해상 스케줄은 출항 시점 기준 계획과 실제 운영이 다르게 움직이는가?
- ETA 오차는 어떤 방식으로 트럭, 창고, 하역 계획까지 무너뜨리는가?
- 실무자는 단순 조회가 아니라 어떤 예측형 데이터를 가져야 하는가?

이런 점에서 이 기사는 물류 가시성을 단순 추적 기능이 아니라  
**예측 기반 운영 인프라**로 봐야 한다는 점을 잘 보여주는 사례라고 생각했다.

---

## 2. Article Summary

트레드링스 기사에 따르면, ETA는 수출입 담당자에게 단순한 참고 시간이 아니라  
내륙 운송, 터미널 하역, 창고 입고, 바이어 납기까지 연결되는 핵심 기준점이다.

하지만 실제 현장에서는 ETA가 자주 빗나간다. 기사에서 인용한 포르투갈 에보라 대학교와 리스본 대학교 연구진의 2026년 연구는 이를 수치로 보여준다. 포르투갈 시네스 항구에서 2009년부터 2023년까지 15년간 축적된 선박 도착 데이터를 분석한 결과, 사전 보고된 ETA와 실제 도착 시간이 정확히 일치한 비율은 1.77%에 불과했다.

또한 늦게 도착한 선박들의 평균 지연은 6시간 52분이었고, 24시간을 초과한 극단적 지연 사례도 1,623건에 달했다. 기사에 따르면 컨테이너 터미널의 경우 평균 지연 시간이 10시간 26분으로 특히 길었고, 다른 터미널 유형과 달리 지연 도착 선박이 조기 도착 선박보다 많았다.

원인으로는 기상 악화, 선사의 감속 운항, 항만 입항 전 도선사와 예인선 배정 대기, 터미널 내 크레인 고장과 인력 부족 같은 병목이 제시된다. 여기에 선장이나 해운 대리인이 초기에 실제보다 이른 도착을 보고하는 전략적 낙관주의 편향까지 겹치면서 ETA 신뢰도가 떨어진다고 설명한다.

기사는 마지막으로, ETA 오차가 단순한 시간 차이에서 끝나지 않고 선석 운영, 장비·인력 배치, 트럭 대기, free time 초과에 따른 Demurrage & Detention 비용까지 연쇄적으로 번진다고 짚는다.

---

## 3. Why It Matters in Logistics

이 기사가 중요한 이유는 ETA가 단순한 “예상 시간”이 아니라  
공급망 전체를 연결하는 운영 기준값이라는 점을 보여주기 때문이다.

실무에서는 ETA 하나를 기준으로 다음이 움직인다.

- 항만 선석 배정
- 갠트리 크레인 및 하역 인력 스케줄
- 내륙 트럭 배차
- 창고 입고 계획
- 바이어 납기 커뮤니케이션
- free time 관리와 D&D 비용 통제

즉, ETA가 틀리면 단순히 선박만 늦는 게 아니라  
**항만-육상-창고-고객 대응까지 연쇄적으로 흔들린다.**

그래서 이 문제는 “배가 늦었네”로 끝나는 게 아니라,  
공급망 운영의 핵심 기준 데이터가 얼마나 불안정한지 보여주는 문제라고 생각한다.

---

## 4. Data Engineering Analysis

### 4-1. ETA Inaccuracy = Prediction Model Problem

기사에서 가장 중요한 메시지는 ETA 오차가 예외가 아니라 구조적이라는 점이다.

정확 일치 비율이 1.77%에 불과하고, 지연 선박 평균 지연도 6시간 52분 수준이라면  
기존 ETA는 사실상 운영 확정값이 아니라 **확률적 예측값**으로 다뤄야 한다.

즉, 데이터 엔지니어 관점에서는 단순히 선사 제공 ETA를 적재하는 데서 끝나면 안 된다.

필요한 것은:

- initial ETA
- revised ETA
- actual arrival time
- ETA revision history
- prediction confidence
- delay reason classification

즉, ETA는 단일 컬럼이 아니라  
**버전 관리와 신뢰도 관리가 필요한 예측 데이터**라고 생각한다.

---

### 4-2. Port Bottleneck = Event Stream Problem

기사에 따르면 선박이 목적지 항구 인근에 도착해도 바로 입항하지 못할 수 있다.  
도선사 승선, 예인선 배정, 선석 대기, 앞선 선박 하역 지연 등으로 인해  
항구 밖에서 대기하는 시간이 크게 달라진다.

이건 ETA 문제를 단순 항해 속도 문제로 보면 안 된다는 뜻이다.

즉, 필요한 건 단순 위치 데이터가 아니라 다음 같은 이벤트 데이터다.

- anchorage arrival time
- pilot boarding time
- tug assignment time
- berth allocation time
- crane availability event
- discharge start time
- discharge completion time

이런 이벤트 스트림이 있어야  
“왜 늦어졌는가”를 구조적으로 설명할 수 있다.

---

### 4-3. Strategic Optimism = Data Quality Problem

기사에서 특히 흥미로웠던 부분은  
ETA가 순수 자동 계산값이 아니라 선장이나 해운 대리인의 수동 보고에 의해 영향을 받을 수 있다는 점이다.

초기 항해 단계에서 실제보다 짧은 시간을 보고하는 전략적 낙관주의는  
데이터 품질 관점에서 보면 매우 중요한 문제다.

이 경우 시스템은 단순 수집보다 더 나아가:

- source type 구분
- manual vs system-generated ETA 구분
- early-stage ETA bias 측정
- route/carrier별 수정 패턴 분석
- 특정 구간의 낙관 편향 보정

같은 처리가 필요하다.

즉, ETA는 단순 운영 데이터가 아니라  
**사람의 행동 편향이 섞인 데이터 품질 문제**이기도 하다.

---

### 4-4. ETA Delay = Cost Propagation Problem

기사에서 말하듯 ETA가 1~2시간만 어긋나도 특정 항만에서는 조수 시간대를 놓쳐  
10~12시간 이상 추가 대기가 발생할 수 있다.

또 배차된 트럭이 헛돌고, 장비·인력이 유휴 상태가 되며,  
free time 초과 시 체선료와 체류비가 발생한다.

이건 결국 ETA 오차가 시간 문제를 넘어  
**비용 전파(cost propagation)** 문제라는 뜻이다.

따라서 데이터적으로는 ETA 오차와 함께 아래 값도 연결해야 한다.

- truck waiting cost
- crane idle cost
- berth delay cost
- D&D charge
- customer penalty risk
- rescheduling frequency

즉, ETA 예측 개선은 단순 편의 기능이 아니라  
실제 비용 절감과 직결되는 과제라고 생각한다.

---

## 5. KPI Ideas

| KPI | Definition | Why It Matters |
|---|---|---|
| ETA Accuracy Rate | ETA와 ATA가 허용 오차 내 일치한 비율 | 예측 정확도 평가 |
| Average ETA Deviation | 평균 도착 오차 시간 | 운영 불확실성 측정 |
| Delay Over 24h Rate | 24시간 초과 지연 비율 | 극단적 리스크 파악 |
| Container Terminal Delay Avg | 컨테이너 터미널 평균 지연 시간 | 핵심 병목 구간 식별 |
| ETA Revision Frequency | ETA 수정 횟수 | 스케줄 불안정성 측정 |
| Anchorage Waiting Time | 입항 전 대기 시간 | 항만 병목 파악 |
| Delay Cost per Shipment | 건별 ETA 오차로 인한 비용 | 예측 개선 효과 정량화 |

---

## 6. Data Model Idea

### Fact Tables

#### `fact_eta_prediction`
- shipment_id
- vessel_id
- voyage_no
- carrier_code
- route_code
- initial_eta
- revised_eta
- eta_version_no
- prediction_timestamp
- source_type
- confidence_score

#### `fact_vessel_arrival_event`
- vessel_id
- port_code
- anchorage_arrival_time
- pilot_boarding_time
- tug_assigned_time
- berth_allocation_time
- discharge_start_time
- actual_arrival_time

#### `fact_delay_reason`
- shipment_id
- event_date
- delay_reason_type
- delay_hours
- weather_flag
- congestion_flag
- labor_flag
- equipment_flag

#### `fact_delay_cost`
- shipment_id
- truck_waiting_cost
- berth_delay_cost
- crane_idle_cost
- demurrage_cost
- detention_cost
- customer_penalty_estimate

### Dimension Tables

- `dim_carrier`
- `dim_port`
- `dim_route`
- `dim_source_type`
- `dim_delay_reason`
- `dim_terminal_type`

---

## 7. Project Ideas Inspired by This Article

### Project 1. ETA Accuracy Monitoring Dashboard
**Goal:**  
선사/노선/항만별 ETA 정확도와 수정 패턴을 시각화

**Possible Stack:**  
Python / SQL / Power BI

**Output:**  
- ETA deviation dashboard
- carrier comparison page
- revision frequency trend

---

### Project 2. Port Bottleneck Event Model
**Goal:**  
입항 전후 이벤트를 구조화해 ETA 오차 원인을 분석

**Output:**  
- event timeline schema
- bottleneck analysis model
- port waiting time report

---

### Project 3. ETA Delay Cost Propagation Analysis
**Goal:**  
ETA 오차가 트럭 대기, D&D, 장비 유휴 비용으로 어떻게 번지는지 분석

**Output:**  
- delay-to-cost mapping model
- shipment cost impact dashboard
- rescheduling risk score

---

## 8. What I Learned

이 기사를 통해 느낀 점은,  
물류 데이터 엔지니어는 단순히 위치 정보를 보여주는 사람이 아니라  
**불확실한 ETA를 더 신뢰할 수 있는 운영 신호로 바꾸는 사람**이어야 한다는 것이다.

더 구체적으로는,

- 초기 ETA와 수정 ETA를 이력으로 관리하고
- 항만 이벤트 스트림을 붙여 지연 원인을 설명하며
- 사람의 낙관 편향이 섞인 데이터를 보정하고
- ETA 오차가 비용으로 전파되는 구조를 수치화하는 역할

이 중요하다고 생각한다.

앞으로도 물류 이슈를 볼 때  
단순히 “왜 늦었지?”에서 멈추지 않고,  
**예측값 → 이벤트 발생 → 오차 확대 → 비용 전가 → 운영 대응** 구조로 해석하는 연습을 계속하고 싶다.

---

## 9. Reference

- Tradlinx Blog, *ETA, 선박 일정은 왜 자꾸 늦어질까? 데이터로 본 물류 가시성의 실질적 가치와 대안*
