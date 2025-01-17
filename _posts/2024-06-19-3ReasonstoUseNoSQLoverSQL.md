---
title: "NoSQL을 사용하는 이유와 SQL을 선택하는 3가지 이유"
description: ""
coverImage: "/assets/img/2024-06-19-3ReasonstoUseNoSQLoverSQL_0.png"
date: 2024-06-19 16:25
ogImage:
  url: /assets/img/2024-06-19-3ReasonstoUseNoSQLoverSQL_0.png
tag: Tech
originalTitle: "3 Reasons to Use NoSQL over SQL"
link: "https://medium.com/gitconnected/3-reasons-to-use-nosql-over-sql-b3fe05b09325"
isUpdated: true
---

`<img src="/assets/img/2024-06-19-3ReasonstoUseNoSQLoverSQL_0.png" />`

NoSQL과 SQL 데이터베이스 중에서 결정하는 것은 매우 어려운 선택일 수 있습니다.

둘 다 장단점이 있지만, 오늘은 NoSQL이 SQL에 비해 확실한 3가지 장점에 초점을 맞출 것입니다.

DISCLAIMER ⚠️: SQL 데이터베이스에 대해 반대 의견을 제시하는 것이 아니며, 이 자리는 이러한 훌륭한 기술들에 대한 공식적인 토론을 촉발하는 것을 목표로 합니다.

<div class="content-ad"></div>

그러니 더 이상 망설일 필요 없어요... 바로 시작해 봅시다!

# 1. 샤딩

샤딩은 데이터베이스의 데이터를 여러 서버에 분산시키는 기술입니다.

샤딩은 수평 확장으로도 알려져 있어요.

<div class="content-ad"></div>

대안은 수직 스케일링이며, 이는 데이터베이스를 업그레이드하여 스케일을 조정하는 기술로 단일 서버를 업그레이드하는 것을 의미합니다(예: RAM 추가, CPU 업그레이드).

NoSQL 데이터베이스는 자연적으로 수평 스케일링(Sharding)에 더 적합하며, SQL 데이터베이스는 수직 스케일링에 더 적합합니다.

NoSQL이 샤딩에 더 적합한 이유는 데이터가 자체를 포함하고 있기 때문에 데이터와 해당 테이블 간의 의존성이 없다는 점입니다.

NoSQL에서 샤딩이 더 쉬운 이유를 이해하기 위해 다음 예제를 살펴보십시오:

<div class="content-ad"></div>

마치 미디엄처럼 블로깅 플랫폼을 상상해보세요. 블로그 게시물 객체에는 댓글과 좋아요가 포함됩니다.

![2024-06-19-3ReasonstoUseNoSQLoverSQL_1 이미지](/assets/img/2024-06-19-3ReasonstoUseNoSQLoverSQL_1.png)

NoSQL에서는 이 객체가 다른 서버에 있는 다른 테이블에서 데이터를 조인할 필요 없이 그대로 저장됩니다.

그러나 SQL 데이터베이스에서는 게시물, 댓글 및 좋아요를 조인해야 합니다.

<div class="content-ad"></div>

SQL 데이터베이스가 샤드로 분할되면 어렵습니다. 서로 다른 서버에 위치한 코멘트와 조회수를 JOIN하는 것이 훨씬 어려워집니다.

## 2. 규모별 성능

간단한 데이터 몇 천 개를 다룬다면, NoSQL과 SQL 데이터베이스 간의 성능은 비슷해야 합니다.

이제 수십억 개의 복잡한 관계형 데이터로 확장해 봅시다.

<div class="content-ad"></div>

이 상황에서 NoSQL은 여러 서버에 걸쳐 행을 분할할 수 있기 때문에 성능이 유지됩니다.

게다가, NoSQL 쿼리는 데이터의 복잡성이 증가함에 따라 매우 잘 확장되며, 실제로 쿼리 시간은 비교적 일관적이고 빠릅니다.

반면에 대규모 SQL 데이터베이스를 분할하는 것은 악몽이며, 수직 확장은 가능하지만 샤딩과 비교했을 때 비용 효율적이고 확장 가능하지 않습니다.

더 나쁜 것은 SQL 스키마가 복잡해지면 여러 JOIN 쿼리가 쌓여 데이터베이스의 성능을 떨어뜨릴 수 있습니다.

<div class="content-ad"></div>

# 3. 간편함

NoSQL의 핵심 목적은 사전 정의된 구조를 준수하지 않고 대량의 비구조화된 데이터를 저장할 수 있게 하는 것입니다.

결과적으로 NoSQL 데이터베이스는 SQL 데이터베이스처럼 엄격한 스키마를 강제하지 않습니다.

이는 프로젝트가 시작되기 전에 스키마를 계획하는 시간을 적게 소비하게 되어 빠른 개발을 이끌어낼 수 있습니다.

<div class="content-ad"></div>

그래도 이렇게 계획을 다 해놓았음에도 불구하고, 데이터베이스 스키마를 언젠가는 더 다듬어야 할 가능성이 높습니다.

기존 필드를 제거하거나 수정하여 SQL 스키마를 개선하는 것도 문제가 될 수 있습니다.

기존 테이블에서 데이터를 업데이트된 스키마를 기반으로 새 테이블로 이관해야 하기 때문에 시간이 많이 소요될 수 있습니다.

그러나 NoSQL을 사용하면 간단히 열을 제거하거나 수정할 수 있습니다!

<div class="content-ad"></div>

## 결론

우리는 SQL 대안 대신 NoSQL 데이터베이스를 사용하는 3가지 이유를 탐색했습니다.

NoSQL의 간결함과 성능 장점은 대부분의 애플리케이션에 대해 유망한 선택지로 만들어 주며, 특히 빠르게 확장될 것으로 예상되는 애플리케이션에는 특히 적합합니다.

이는 SQL 데이터베이스가 나쁘다는 것을 의미하는 것이 아니라, 데이터를 확장하는 방법을 다시 생각하고 작업에 적합한 도구를 선택하도록 고려해야 한다는 것을 의미합니다.

<div class="content-ad"></div>

# 제휴사

- All-in-One SaaS 프로젝트 템플릿
- Figma 홈: 제가 모든 프로젝트에서 사용하는 UI 디자인 툴
- Figma 프로페셔널: 당신이 필요로 하는 유일한 UI 디자인 툴
- FigJam: 직관적인 다이어그램 및 아이디어 도출로 마음을 자유롭게 펼치세요
- Notion: 제 인생 전반을 조직하는 데 사용되는 도구
- Notion AI: ChatGPT보다 더 나은 AI 도구로 Notion 업무 흐름을 업그레이드하세요

# 참고 자료

- NoSQL vs RDBMS와 확장성
- 샤딩(Sharding)이란 무엇인가요?
