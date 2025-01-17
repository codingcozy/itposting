---
title: "데이터에서의 마이크로서비스 대 모놀리식 접근 방식"
description: ""
coverImage: "/assets/img/2024-06-19-MicroservicesvsMonolithicApproachesinData_0.png"
date: 2024-06-19 05:26
ogImage:
  url: /assets/img/2024-06-19-MicroservicesvsMonolithicApproachesinData_0.png
tag: Tech
originalTitle: "Microservices vs. Monolithic Approaches in Data"
link: "https://medium.com/towards-data-science/microservices-vs-monolithic-approaches-in-data-8d9d9a064d06"
isUpdated: true
---

# 소개

데이터 공간에서 도구를 선택하는 일이 어렵다는 것을 설득하는 데 많은 단어를 쏟을 필요가 없습니다. 이 작업에는 수백 가지, 혹은 몇 천 가지의 방법이 있을 수도 있습니다.

사람들이 종종 간과하는 것은 아키텍처가 이러한 결정에 어떻게 영향을 미치는지입니다.

약 20년 전에는 응용프로그램이 필요한 회사가 소유한 컴퓨터에 있었습니다 – 이를 "온프레미스"라고 합니다. 이 컴퓨터를 소유하는 것은 아키텍처적인 결정이었습니다. 그 결과, 그 시기의 아키텍처와 호환되지 않아 클라우드 소프트웨어에 대한 수요가 없었기 때문에 클라우드 소프트웨어 업체는 존재하지 않았습니다.

<div class="content-ad"></div>

2024년으로 빨리 이동하면 반대로 됩니다 - 대부분의 사람들이 완전히 클라우드로 이동했습니다. 그러나 우리 중 일부는 아직도 자체 서버를 운영하고 있습니다. 다른 사람들은 하이브리드 모델을 갖고 있습니다. 이는 아키텍처가 선택한 솔루션에 미치는 영향을 이해하는 것이 이전보다 더 중요하다는 것을 의미합니다. 이 글에서는 데이터 아키텍처에 대한 마이크로서비스 대 모놀리식 접근 방식이 도구 구매에 어떻게 영향을 미치는지 살펴보겠습니다.

# 마이크로서비스 vs. 모놀리식 아키텍처

데이터에서 일어나는 일 중 하나는 마이크로서비스 대 모놀리스 논쟁이 다시 시작된 것입니다. 이게 무엇인지 이해하려면:

데이터 내에서 10년 전에는 모놀리식 응용프로그램이 꽤 흔했습니다. 이것의 예로는 대규모 Airflow 저장소가 있습니다. 이 저장소에는 데이터 수집 코드, 데이터 변환 코드 및 비즈니스 자동화가 포함되어 있을 수 있습니다.

<div class="content-ad"></div>

비지니스 자동화에는 대시보드 새로 고침, 보고서 전송 또는 작업 실패 시 알림 전송과 같은 것이 포함될 수 있습니다.

한편 클라우드의 폭발성 증가는 부분적으로 벤처 투자를 통해 주어진 것이며 (이 보고서 참조), 데이터 아키텍처의 등장을 불러왔습니다. 이러한 데이터 아키텍처는 마이크로서비스를 밀접하게 닮았습니다. 마이크로서비스에는 일괄 데이터 이동, 데이터 변환 및 데이터 웨어하우스 관리용 애플리케이션이나 스트리밍 데이터 관리용 애플리케이션이 포함됩니다.

데이터 스택을 단일체(monolith) 또는 마이크로서비스로 볼지 여부는 소프트웨어 선택에 영향을 미쳐야 합니다.

<img src="/assets/img/2024-06-19-MicroservicesvsMonolithicApproachesinData_0.png" />

<div class="content-ad"></div>

# 마이크로서비스 데이터 아키텍처: 가정

마이크로서비스 아키텍처를 선택하면, 당신은 당신의 마이크로서비스가 무엇을 수행하길 원하는지, 그리고 어떻게 통신하길 원하는지에 대한 몇 가지 가정을 암묵적으로 한다. 이러한 것들이 당신이 작업을 수행할 때 무엇을 선택해야 하는지에 영향을 미칠 것이다.

## 가정 1: 분산 인프라

마이크로서비스를 사용하면 데이터 팀은 클라우드와 온프레미스 인프라의 다른 부분에 인프라를 분배할 수 있다. 이는 각 마이크로서비스가 자신의 일에 특화될 수 있음을 의미한다. 이에는 두 가지 이점이 있다.

<div class="content-ad"></div>

- 전문화와 효율성

데이터 수집, 변환 등에 동일한 인프라를 사용하는 대신, 각각 다른 용도에 다른 부분을 사용할 수 있습니다. 이는 더 높은 전문화 수준과 궁극적으로 더 큰 효율성으로 이어집니다.

2. 더 쉬운 확장성

일반적으로 워크로드를 다른 마이크로서비스로 분리하면, 메모리 및 저장 공간과 같은 컴퓨팅 성능이 다양한 위치로 분할됩니다. 이는 서비스를 확장하거나 축소하는 작업이 덜 복잡해집니다. 예를 들어, 쿠버네티스 클러스터를 유지하는 대신 기본 워크로드를 서버리스 기능(자동으로 확장)에서 실행할 수도 있습니다.

<div class="content-ad"></div>

![image](/assets/img/2024-06-19-MicroservicesvsMonolithicApproachesinData_1.png)

## 가정 2: 높은 상호 운용성과 거버넌스

마이크로서비스 인프라를 가정할 때, 이 서비스들이 서로 통신하고 상호 운용 가능하다는 것을 암시합니다. 소프트웨어 엔지니어링에서는 계약, 이벤트 기반 통신 및 Datadog와 같은 중앙 집중식 로깅 시스템을 통해 이를 가능하게 합니다.

이를 데이터로 옮기는 것은 까다로울 수 있습니다. 데이터 수집 서비스, 데이터 웨어하우스에 위치한 데이터 변환 서비스 및 BI 도구(제3자 SAAS)가 있다면, 이들을 어떻게 연결하고 함께 거버넌스할 수 있을까요?

<div class="content-ad"></div>

전통적인 방법은 Airflow와 같은 도구를 사용하여 그들을 함께 엮는 것인데, 이 방법은 매번 점을 연결하려면 코드를 작성해야 한다는 것입니다. 이 비용은 높습니다. 이 때문에 상호 운용성이 줄어들어 가정을 위반합니다.

게다가, 많은 "현대 데이터 스택" 아키텍처에서, 엔드 투 엔드 가시성과 거버넌스를 얻는 유일한 방법은 데이터 카탈로그나 가시성 도구와 같은 추가 도구를 구매하는 것입니다. 이러한 도구들은 매우 비싸기 때문에 많은 데이터 팀이 마이크로서비스 아키텍처를 가정하는 상황에서 상호 운용성 부재와 거의 기본적인 거버넌스를 수용하게 됩니다.

## 가정 3: 허용 가능한 데이터 이그레스와 저장

데이터 아키텍처 내의 마이크로서비스에서 생성된 데이터와 메타데이터에는 많은 가치가 있습니다. 이는 여러 곳에 저장되지만 서비스 간에 공유됩니다. 이는 마이크로서비스 스타일 아키텍처에서 허용 가능하다고 가정되는 "데이터 이그레스" 비용을 필요로 합니다.

<div class="content-ad"></div>

예를 들어 “ELT” 패턴을 채택하고 간단히 “Snowflake에 모든 데이터를 덤프” 한다면, 모든 데이터를 먼저 처리하는 것보다 입력 요금이 더 많이 발생할 수 있습니다. 일반적으로 아키텍처가 이벤트 주도 방식으로 통신하길 원한다면 먼저 "T"를 수행하는 것이 좋습니다. 예를 들어 Kafka는 이를 지원합니다.

최근에 많이 확산된 일부 다른 도구에도 일감을 비쳐 줍니다. 예를 들어 Observability, Lineage 또는 이상 탐지 도구를 살펴보세요. 모든 이 도구는 기본 시스템에서 데이터를 (상당량의 데이터로) 가져옵니다. 이는 이 도구를 사용함으로써 이러한 데이터에 대한 출발 요금을 지불해야 한다는 것을 의미합니다.

둘째, 이러한 데이터를 저장하므로 여기에도 저장 요금을 내야 합니다. 셋째, 제공되는 데이터 제품을 전달하는 데 사용하는 일정과 관련이 없는 일정에 실행되기 때문에 비용 부담이 될 수 있습니다. 마지막으로, 그리고 중요하게, 이미 갖고 있는 것과 상관없는 새로운 마이크로서비스인 경우에 컨텍스트를 함께 모아서 결과를 얻지 못하는데, 이는 불필요하게 높은 연산 비용으로 이어집니다. 결과적으로 이 비용을 지불하게 됩니다.

`/assets/img/2024-06-19-MicroservicesvsMonolithicApproachesinData_2.png`의 이미지를 확인해보세요.

<div class="content-ad"></div>

나는 거대한 건물에 대한 건축적 고려에 대해 다루지 않겠어요, 그것은 다음 포스트에서 다룰 주제일 거예요!

# 마이크로서비스 또는 모듈식 아키텍처를 위한 배운 점

많은 데이터 응용 프로그램이 상호 작용하거나 조정되는 것은 정말 마이크로서비스가 아니에요 – 이 글을 읽는 소프트웨어 엔지니어들은 이에 대해 제게 비난할 거에요! 그러니까 이를 “모듈식”이라고 부르자구요.

이 "모듈식" 방법론은 최신 데이터 스택에 부합되어 있어요. 그러나 최신 데이터 스택은 가정 2와 3을 위반해요.

<div class="content-ad"></div>

가정 2를 위반합니다. MDS가 상호 운용 가능하고 자체와 통신할 수 있는 정도가 매우 낮기 때문입니다. 실제로 작동시키기 위한 유일한 방법은 많은 코드가 포함된 거대한 Airflow 저장소가 있는 것입니다. 이는 단일체 아키텍처를 구축할 때 자연스러운 일입니다.

가정 3을 위반합니다. 이집트 및 저장 비용의 수용 가능한 수준이 실제로 없습니다. 공간/계산이 분리된 여러 응용 프로그램을 갖는 경우, 새로운 소프트웨어를 추가할 때마다 데이터에 대해 두 배의 비용을 지불해야 합니다.

보다 명확히 설명하기 위해 종종 "만약 내가 직접 이것을 구축해야 한다면 어떻게 보였을까요?"라는 질문을 합니다.

대답은 항상 "[클라우드 제공자 이름을 여기에 삽입]"의 내부 개발 서비스입니다. 대부분의 데이터가 이미 클라우드에 있으므로 클라우드 제공업체가 원하는 서비스를 제공한다면, 데이터 전송 및 저장에 대해 두 번 지불할 필요가 없습니다.

<div class="content-ad"></div>

데이터 카탈로그에 대해 생각해보세요. 아키텍처 측면에서 데이터 카탈로그는 데이터 웨어하우스(예: BigQuery)로부터 모든 메타데이터를 가져와 저장하고, 해당 데이터를 기반으로 일부 계산을 수행하고 UI를 제공합니다.

이러한 종류의 아키텍처를 사용하여 직접 구축하면 이직료를 지불해야 하고 추가 저장 공간을 지불해야 하며 약간의 추가 컴퓨팅 리소스를 사용해야 합니다(카탈로깅 컴퓨팅은 매우 간단하므로 저렴합니다). 또한 내 클라우드에 배포하지 않는 한 보안 문제도 생길 수 있습니다.

이러한 대부분의 비용은 불필요합니다. 이미 데이터를 소유한 서비스에서 이러한 작업을 수행해야 합니다. 또는 데이터가 레이크하우스/가상화 패턴과 같이 여러 서비스에서 이용할 수 있어야 합니다. 그러나 이것을 카탈로그처럼 구축하지 않을 것입니다 - 이전 다이어그램의 갈색 상자들처럼 말이죠.

하지만 기다려보세요 - GCP에 이와 비슷한 기능이 있지 않나요? 이름이 기억이 나지 않는데, 입에서 막 말하려 했는데... 아! 기억했어요! 바로 데이터 카탈로그입니다!

<div class="content-ad"></div>

만약 BigQuery를 사용 중이라면, 이미 존재하는 데이터 카탈로그를 사용하는 것이 아키텍처적으로 훨씬 더 합리적일 것입니다. 데이터가 나가거나 중복 저장, 추가적인 보안 위험도 없으며, 아마도 동일한 용어를 사용하고 동일한 위치(Chrome 탭)에 있는 더 나은 UI를 제공할 것입니다.

따라서, "그 곳에 있어야 하는" 것들은 항상 다른 제3자 SaaS 도구 대비 우위를 가지게 될 것이며, 제공 비용이 낮기 때문에 장점을 가질 수 있습니다.

이것은 아래 다이어그램에서 설명할 수 있으며, GCP는 Collibra와 같은 회사에 비해 배송 비용이 낮습니다. 장기적으로, 이러한 서비스들은 클라우드 제공업체가 제작한 내부 도구에 비해 매우 효율적이고 탁월해야 합니다.

<img src="/assets/img/2024-06-19-MicroservicesvsMonolithicApproachesinData_3.png" />

<div class="content-ad"></div>

장기적인 관점에서 GCP의 데이터 카탈로그는 항상 Collibra보다 저렴할 것입니다. 기억하세요, GCP는 중앙 비용을 고용하고 다른 회사를 설립할 필요가 없습니다. 단지 데이터 카탈로그를 제공하기 위해 100명의 개발자들을 고용합니다.

같은 가격으로, 클라우드 공급업체가 실행 및 효율적이라면, 제공 비용이 너무 높기 때문에 제3자 SaaS 공급업체가 경쟁할 수 없습니다. 물론 그들의 서비스가 현재 상당히 더 나은 경우(현재 그렇다고 말할 수 있습니다).

# 결론

이 기사에서는 데이터 구조가 데이터 엔지니어와 아키텍트가 응용 프로그램이 어떻게 실행되고 서로 작동하는지에 대한 가정을 만들도록 강제한다는 것을 보았습니다. 마이크로서비스 또는 "모듈식" 아키텍처를 채택하는 경우, 좋은 아키텍처는 몇 가지 가정을 해야 한다는 것을 보았습니다.

<div class="content-ad"></div>

이 가정들은 Modern Data Stack을 통합하여 사용하고 마이크로서비스를 사용할 때도 깨져요. 또한 낮은 상호 운용성 및 높은 외부 통신/저장 비용 때문에 별도의 SAAS로도 사용됩니다.

재미있는 점은 클라우드 인프라 제공 업체가 독립 소프트웨어 공급 업체와 비교하여 추가 기능을 개발할 때 우위에 있는 것입니다. 그 이유는 그들이 이미 모든 데이터를 보유하고 있기 때문에 더 많은 자원과 구조 이점이 있기 때문입니다.

예시로 클라우드 제공 업체 (GCP)를 데이터 카탈로그 제공 업체 (Collibra)와 비교해 보았습니다. 이것은 소프트웨어 제공 업체 중 많은 업체에 확장될 수 있지만 모든 업체에는 해당하지 않습니다. 일반적으로 감사, 카탈로그, 데이터 품질 등과 같은 제어 평면의 도구들이 기존 인프라에 잘 맞습니다.

클라우드 인프라로 데이터를 가져오는 데 많은 컴퓨팅을 필요로 하는 도구들은 외부에 배치하는 것이 합리적해요. 예시로는 스트리밍 플랫폼이나 데이터 수집 도구 등이 있습니다.

<div class="content-ad"></div>

가장 흥미로운 점은 Airflow와 Monte Carlo와 같은 Orchestration 및 Observability 도구가 모던 데이터 스택에서 사용되는 모듈식 아키텍처에 아키텍처적으로 매력적이지 않은 패턴을 부담한다는 것이죠.

아키텍처와 비용이 데이터 영역에서 사람들이 내리는 선택에 어떻게 영향을 미치기 시작하는지를 보는 것은 흥미로울 것 같습니다. 자유 시장은 신비로운 방식으로 작용합니다. 그 영향력은 다른 곳보다 데이터에서도 덜하지 않습니다! 💸

만약 단일체 아키텍처, 다른 도구 또는 올인원 데이터 플랫폼에 이 관점을 적용하는 방법에 대해 알고 싶다면 언제든 연락해 주세요.
