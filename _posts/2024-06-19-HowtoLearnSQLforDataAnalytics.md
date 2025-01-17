---
title: "데이터 분석을 위한 SQL 배우는 법"
description: ""
coverImage: "/assets/img/2024-06-19-HowtoLearnSQLforDataAnalytics_0.png"
date: 2024-06-19 05:24
ogImage:
  url: /assets/img/2024-06-19-HowtoLearnSQLforDataAnalytics_0.png
tag: Tech
originalTitle: "How to Learn SQL for Data Analytics"
link: "https://medium.com/towards-data-science/how-to-learn-sql-for-data-analytics-5e50fa343b72"
isUpdated: true
---

<img src="/assets/img/2024-06-19-HowtoLearnSQLforDataAnalytics_0.png" />

그래서... 데이터 분석가가 되고 싶으시군요.

혹시 이미 풀타임 직업을 가지고 계시고 데이터 산업으로의 전직을 희망하시는 건가요?

아니면 아직 이 분야에 완전히 처음이시고 분석 분야의 채용정보를 집중적으로 찾으시는 분일 수도 있겠군요.

<div class="content-ad"></div>

어떤 분야에 속하든 상관없이 데이터 분석 인터뷰에서 항상 시험을 받게 되는 하나의 기술이 있습니다: SQL.

이 글에서는 SQL을 처음부터 배우기 위한 완전한 로드맵을 제시하겠습니다.

비디오 버전을 보려면 여기를 클릭하세요:

이 글은 세 가지 섹션으로 나뉘어 있습니다. 원하는 섹션으로 건너뛰어도 괜찮습니다:

<div class="content-ad"></div>

- SQL은 무엇이며 데이터 분석가에게 꼭 필요한 기술인 이유는 무엇인가요?
- SQL을 배우는 방법은 무엇인가요?
- SQL 면접 준비는 어떻게 해야 하나요?

첫 두 가지 항목을 광범위하게 다루는 많은 자료를 본 적이 있지만, 많은 사람들이 SQL 학습 과정에서 가장 중요한 면접 준비 부분을 간과하는 경향이 있습니다.

온라인 강좌를 수강하는 것과 SQL로 비즈니스 문제를 해결하는 것 사이에는 세계적인 차이가 있습니다. 이것은 기술 면접의 SQL 파트에서 처참히 실패한 후에 깨달은 교훈이었습니다.

제 접근 방식을 변경한 후에야 구직 제의를 받기 시작했습니다.

<div class="content-ad"></div>

내 의견으로는, SQL 학습 여정 중 1/4 정도만 강의를 수강하고 콘텐츠를 소비하는 데 사용해야 한다고 생각해요.

나머지 시간은 면접 준비에 할애해야 해요, 왜냐하면 취직에 실패하면 이 모든 노력이 무의미할 수 있거든.

그럼 시작해볼까요?

# 먼저... SQL이 뭔지, 그리고 왜 배워야 하는지를 알아볼게요.

<div class="content-ad"></div>

대부분의 회사들은 데이터를 데이터베이스에 저장합니다.

그리고 데이터 분석가로서 여러분은 이 데이터를 분석하고 비즈니스 인사이트를 도출해야 합니다.

예를 들어, 마케팅팀이 새로운 스타워즈 상품을 홍보해야 할 대상을 알고 싶어할 때 당신이 그 사람이 될 것입니다.

당신은 데이터베이스에서 이러한 인사이트를 질의해야 합니다. 그리고 이 작업을 수행하기 위해 SQL이라는 프로그래밍 언어를 사용할 것입니다.

<div class="content-ad"></div>

SQL은 Structured Query Language의 약자입니다.

스타워즈 상품 예시에서, 회사의 데이터베이스는 다양한 테이블로 이루어져 있다고 상상해보세요.

각 테이블은 다른 종류의 정보를 추적합니다. 고객 세부 정보를 저장하는 "Customers" 라는 테이블, 상품 세부 정보를 저장하는 "Products" 테이블, 그리고 거래 데이터를 유지하는 "Sales" 테이블 등이 있을 수 있습니다:

![Database Tables](/assets/img/2024-06-19-HowtoLearnSQLforDataAnalytics_1.png)

<div class="content-ad"></div>

우리는 SQL 쿼리를 사용하여 이러한 테이블과 상호 작용할 수 있어요.

데이터베이스의 모든 고객을 선택하려면 다음과 같은 쿼리를 작성하면 돼요:

```js
Select * from Customers
```

쉽죠? 😊

<div class="content-ad"></div>

SQL은 실제로 꽤 간단해요.

일반 영어와 비슷해서 직관적이에요.

사실, 엑셀을 알고 있다면 - 셀 추가하거나 피벗 테이블로 데이터를 그룹화하는 등 - SQL을 쉽게 배울 수 있어요.

# SQL 배우는 방법?

<div class="content-ad"></div>

이제 SQL이 무엇인지 알았으니 어떻게 이 언어를 배울 수 있을까요?

SQL을 가르치는 수천 개의 부트캠프와 온라인 강좌가 있습니다.

여기서 설명되는 데이터 분석을 위한 핵심 SQL 개념에 대해 다루는 한 이러한 학습 자료 중 하나를 선택할 수 있습니다.

## 단계 1: SQL 환경 설정

<div class="content-ad"></div>

SQL 구문 배우기 전에 데이터베이스 관리 시스템(DBMS)을 설정해야 합니다.

이것은 SQL 쿼리를 작성하고 실행할 데이터베이스 시스템 설정입니다.

여기 10분 이내에 설정하는 데 도움이 되는 YouTube 비디오가 있습니다.

MySQL, PostgreSQL, SQLite 등 여러 유형의 데이터베이스 시스템을 선택할 수 있습니다.

<div class="content-ad"></div>

이 글에서는 이러한 데이터베이스 시스템 간의 세세한 차이에 대해서 다루지 않을 거예요.

지금은 SQL과 PostgreSQL이 가장 인기 있는 선택지인 것을 알고 계시면 충분할 거예요.

## 단계 2: SQL 명령어 배우기

데이터 분석가로서 데이터베이스에서 통찰을 추출하고 그것을 비즈니스 결정에 활용할 거예요.

<div class="content-ad"></div>

아래는 배워야 할 명령어를 세 가지 섹션으로 나누어 놓았어요:

## 초보자

SQL 초보자 레벨의 쿼리에는 다음과 같은 기본 개념이 포함되어 있어요:

- Select
- Where clause
- From clause
- Data types
- Order by
- Limit

<div class="content-ad"></div>

이러한 개념들은 직관적이며, 배우는 데 단 1~2일이 걸릴 것입니다.

## 중급

다음 수준의 SQL 쿼리에는 다음이 포함됩니다:

- Group by
- Having
- Joins (inner, outer, left, right, self)
- Subqueries
- Case statements

<div class="content-ad"></div>

이 SQL 쿼리들 또한 꽤 쉽습니다. 데이터를 병합하거나 피벗 테이블을 만들거나 지난번에 "if" 문을 작성했다면, 이 SQL 개념들을 아주 빠르게 습득할 수 있을 겁니다.

그렇지 않다면, 위의 명령어들을 배우는 데 약 4~5일이 소요될 것입니다.

## 고급

언어의 기본을 마스터 했다면, 다음과 같은 더 고급 개념들을 배우실 수 있습니다:

<div class="content-ad"></div>

- 공통 테이블 표현식 (CTEs)
- Pivot 테이블
- 윈도우 함수
- 성능 최적화

위의 개념들을 이해하고 그 원리를 파악하는 데 약 일주일이 소요될 것입니다.

# 이 SQL 개념을 배울 수 있는 곳은?

다음은 위의 개념을 가르쳐줄 무료 학습 자료 3가지입니다:

<div class="content-ad"></div>

## 1. 4시간 만에 SQL 배우기 (Luke Barousse)

이것은 데이터 분석가로서 알아야 할 거의 모든 SQL 명령을 다루는 무료 YouTube 강의입니다.

이 비디오의 제작자인 Luke Barousse는 데이터 분석가이기 때문에 이 강의를 분석 분야에 맞게 제작했습니다.

튜토리얼에 나오는 모든 사용 사례와 문제 설명은 기타 강의에서 산업 범위를 벗어난 내용을 다루는 반면, 데이터 분석가에게 관련이 있습니다.

<div class="content-ad"></div>

## 2. 초보자를 위한 MySQL (모쉬와 함께 프로그래밍)

이 강의는 Luke의 튜토리얼 대안으로 수강할 수 있습니다. 동일한 개념들이 다루어지기 때문이에요.

하지만, 저는 2:18까지만 수강하는 것을 추천드립니다. 그 이후에 가르치는 개념들은 데이터 분석가들이 일반적으로 수행하지 않는 데이터베이스 수정 및 업데이트 작업에 초점을 맞추고 있어요.

## 3. W3Schools

<div class="content-ad"></div>

W3Schools는 다양한 프로그래밍 언어를 다루는 대화식 웹사이트입니다.

위 자료에서 다루지 않은 주제를 학습하려면 이 사이트의 SQL 튜토리얼 섹션을 방문하는 것을 추천합니다.

게다가, 이 플랫폼은 샘플 데이터베이스를 사용하여 직접 쿼리를 실행할 수 있는 대화식 인터페이스를 제공합니다. 따라서 자신의 SQL 환경에 접근할 수 없는 경우에 유용할 수 있습니다.

# SQL 면접 준비하기

<div class="content-ad"></div>

이전에 이 기사에서 언급한 대로, 튜토리얼을 소비하는 것과 문제를 해결하기 위해 SQL 쿼리를 작성하는 것 사이에는 큰 차이가 있습니다.

SQL 인터뷰에서 통과하고 싶다면 문제 해결을 위해 데이터베이스에서 쿼리를 연습해야 합니다.

저는 HackerRank와 LeetCode에 가입하는 것을 추천합니다 — 이 두 사이트는 가장 인기 있는 프로그래밍 챌린지 플랫폼 중 두 곳입니다.

이 사이트들은 쉬운 것에서 어려운 것까지 다양한 난이도의 SQL 연습 문제를 제공합니다.

<div class="content-ad"></div>

간단한 것부터 시작해서 조금씩 어려운 문제로 나아가세요.

이 사이트에서 적어도 50개의 도전 문제를 완료하는 것을 추천합니다.

나의 경험 상, SQL 인터뷰 문제는 이러한 사이트에서 가져온 것이거나 이 플랫폼의 문제와 매우 유사하게 구성되어 있습니다.

또한 SQL 기술을 향상시키는 데 도움이 되는 생성 AI를 사용하는 것을 추천합니다.

<div class="content-ad"></div>

ChatGPT에게 샘플 데이터셋과 연습 문제를 요청하고 답변을 평가해 보세요. 개념을 이해하는 데 어려움을 겪을 때 특히 유용합니다. 저에게는 "셀프 조인"이 그랬어요. 학습 과정 초반에 셀프 조인이 낯설고 언제 적용해야 하는지 잘 모르겠던 걸요.

<div class="content-ad"></div>

저는 테이블을 자기 자신과 결합하는 개념을 상상할 수 없었어요.

이 명령어를 더 잘 이해하기 위해, ChatGPT에게 여러 가지 예시를 들어 설명해달라고 여러 번 요청했어요.

그 후에 챗봇에게 셀프 조인에 관한 다양한 난이도의 연습 문제를 많이 풀게 했어요.

결국 그 주제에 대해 이해하게 되었어요!

<div class="content-ad"></div>

# 데이터 분석을 위한 SQL 학습 — 다음 단계

이 기사에서 많은 내용을 다루었습니다.

끝까지 따라오셨다면, 축하합니다!

이제 SQL이 무엇이고, 분석을 위한 필수 기술인 이유, 그리고 어떻게 배울 수 있는지 알게 되었습니다.

<div class="content-ad"></div>

그 다음 단계로서 매일 SQL을 배우는 것을 권장합니다.

적어도 한 달 동안 매일 약 1-2시간을 SQL 학습에 투자해보세요.

이것을 30일간의 SQL 도전 이라고 부르겠습니다.

첫 주 정도는 SQL 명령어와 데이터베이스 관리에 익숙해지는 데 시간을 투자해보세요.

<div class="content-ad"></div>

그럼, 나머지 시간을 활용하여 HackerRank나 Leetcode와 같은 사이트에서 SQL을 연습해보세요. 이 두 플랫폼을 통해 적어도 50가지 이상의 연습 문제를 완료해보세요.

30일 동안의 도전을 마칠 때쯤에는 어떤 데이터 인터뷰에서도 SQL 부분을 뛰어넘을 준비가 되어 있을 거예요.
