---
title: "호두 판매 사례 연구"
description: ""
coverImage: "/assets/img/2024-06-23-WalnutSalesCaseStudy_0.png"
date: 2024-06-23 16:51
ogImage:
  url: /assets/img/2024-06-23-WalnutSalesCaseStudy_0.png
tag: Tech
originalTitle: "Walnut Sales Case Study"
link: "https://medium.com/@shivaniwac/walnut-sales-case-study-cea9916a12c1"
isUpdated: true
---

호두 판매 탐험: 사례 연구 여정

데이터 분석을 깊게 이해하고 실무 경험을 쌓기 위해 호두 판매에 초점을 맞춘 사례 연구를 시작했습니다. 이 프로젝트를 통해 고객 행동과 제품 수익 동태에 대한 소중한 통찰을 얻을 뿐만 아니라 데이터베이스 관리와 SQL 쿼리 작성 기술을 연마할 수 있었습니다.

![Image](/assets/img/2024-06-23-WalnutSalesCaseStudy_0.png)

데이터셋 획득 및 초기 설정~

<div class="content-ad"></div>

먼저, 캐글에서 포괄적인 월넛 판매 데이터셋을 확보하여 다양한 측면을 아우르도록 세심하게 정리했습니다. 이 데이터셋을 사용하여 `walnut_sales`라는 전용 데이터베이스를 설정하고 그 안에 철저히 구조화된 테이블을 만들었습니다. 각 테이블은 적합한 열과 데이터 유형으로 세심하게 설계되어 이후 분석을 위해 최적의 구성과 사용성을 보장합니다.

![Walnut Sales Case Study](/assets/img/2024-06-23-WalnutSalesCaseStudy_1.png)

데이터 변환 및 준비

기본 단계로, SQL 함수를 사용하여 `day_name` 및 `time_of_day`와 같은 보조 열을 생성했습니다. `DAYNAME()` 및 `MONTHNAME()`과 같은 기능을 활용하여 거래를 의미 있는 시간 및 요일 범주로 분류했습니다 — 아침, 오후, 저녁 또는 주중 구체적인 일 등. 이러한 분할은 자세한 시간적 분석과 추세 식별을 위한 기초를 마련했습니다.

<div class="content-ad"></div>

<img src="/assets/img/2024-06-23-WalnutSalesCaseStudy_2.png" />

초기 탐색적 분석

분석의 초기 단계에서는 다음과 같은 핵심적인 통찰력을 발견하기 위해 노력했습니다:

- 데이터셋에서 대표되는 독특한 도시와 지점 식별.
- 고객들 사이에서 일반적인 결제 수단 분석.
- 인기 있는 제품 라인과 해당 매출 분석.
- 다양한 제품 라인에서 가장 큰 부가가치세(VAT) 기여를 계산하여 중요한 재정적 영향을 밝혀냈습니다.

고급 분석 기술

<div class="content-ad"></div>

기본 통찰력을 바탕으로, 나는 심층적인 통찰력을 추출하고 정교한 분석을 수행하기 위해 고급 SQL 기술을 활용했습니다:

- CASE 문을 활용한 질적 평가: 수익성 지표나 고객 만족도 지수에 기반하여 각 제품 라인을 "좋음" 또는 "나쁨"으로 레이블링하여 제품 라인 데이터를 보완적으로 분석했습니다.
- HAVING 절을 활용한 집계 필터링: 집계된 데이터를 필터링하기 위해 HAVING 절을 적용하여 매출 성과에 중대한 영향을 미치는 고객 세그먼트나 제품 카테고리를 식별했습니다.
- 사용자 정의 함수: SQL 쿼리 내에서 복잡한 계산이나 비즈니스 로직을 캡슐화하기 위해 사용자 정의 함수를 개발하고 배포하여 반복적인 작업을 간소화하고 분석 효율성을 향상시켰습니다.

# 결론 및 다음 단계

이 심도있는 사례 연구를 통해 SQL 쿼리 및 데이터베이스 관리에 대한 능숙성을 향상시키는 동시에 소비자 선호도부터 재정적 영향까지 왈넛 판매 역학에 대한 세심한 이해를 개발했습니다. 실무 경험은 내 기술 세트를 풍부하게 해줄 뿐만 아니라 다양한 분야에 적용 가능한 실용적인 통찰력을 제공했습니다.

<div class="content-ad"></div>

해당 연구 중 수행된 SQL 쿼리 및 분석 내용을 자세히 살펴보려면 Walnut 케이스 스터디를 여기에서 확인해보세요.

호두 판매 데이터를 통해 진행된 이 여정은 데이터 기반 의사 결정의 힘을 보여주며, 심도 있는 사례 연구가 분석 능력을 갖추는 데 있어 혁신적 잠재력을 강조합니다.
