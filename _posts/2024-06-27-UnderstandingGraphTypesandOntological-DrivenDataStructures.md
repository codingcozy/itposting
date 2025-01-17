---
title: "그래프 유형 및 온톨로지 기반 데이터 구조 이해하기"
description: ""
coverImage: "/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_0.png"
date: 2024-06-27 19:10
ogImage:
  url: /assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_0.png
tag: Tech
originalTitle: "Understanding Graph Types and Ontological-Driven Data Structures"
link: "https://medium.com/@joehoeller/understanding-graph-types-and-ontological-driven-data-structures-185eb176c3c3"
isUpdated: true
---

안녕하세요 멋진 분들, 링크드인에서 그래프와 인공지능에 대한 일반적인 오해가 돌고 있다는 것을 알게 되어 몇 가지 통찰을 공유하는 것이 도움이 될 것 같아요. 이 정보가 유익하게 느껴지고 복잡한 AI 시스템을 효과적으로 구축하는 데 도움이 되기를 바라며 이해에 도움이 될 것입니다. 여러분과 함께 이에 대한 관련하여 활발한 토론를 기대하고 있어요 — 제 링크드인 페이지에서 만나요.

그래프는 컴퓨터 과학부터 생명정보학까지 다양한 분야에서 본질적으로 중요합니다. 그러나 서로 다른 유형의 그래프를 구분하고 고유한 특성 및 응용을 이해하는 것이 중요합니다. Directed Acyclic Graphs (DAGs), Label Property Graphs (LPGs), Bipartate Graphs, Semantic Knowledge Graphs에 초점을 맞추어 이러한 구별을 명확히 하고 공간추론의 문맥에서 정보적으로 주도되는 데이터 구조로써의 역할에 대해 설명하려고 합니다.

# Directed Acyclic Graphs (DAGs)는 Flowcharts (요컨대)

플로우차트는 프로세스 또는 워크플로우를 나타내는 다이어그램 유형으로, 종종 Directed Acyclic Graph (DAG)으로 시각화됩니다. DAG는 방향성이 있고 사이클이 없는 그래프로, 한 노드에서 다른 노드로의 단방향 경로가 있지만 루프는 없다는 것을 의미하여 "비순환적"이에요. 이는 작업흐름이나 계산과정의 단계와 같이 명확한 선형 진행을 가진 프로세스를 나타내는 데 적합하게 만들어 주어요.

<div class="content-ad"></div>

플로우차트는 DAG를 시각화하는 흔한 방법이지만, DAG 자체가 지식 그래프는 아니라는 점을 알아두는 것이 중요합니다. DAG는 일정정렬과 조합적 열거와 같은 다양한 알고리즘에서 활용되어 일정 조정, 데이터 처리 단계 등과 같은 문제를 해결하는 데 사용됩니다. DAG의 주요 관심사는 작업의 순서와 의존성에 있으며, 의미적 관계나 고수준 추론에 대한 것은 아닙니다.

## 의미 지식 그래프

반면에, 의미 지식 그래프는 추론과 추론을 가능하게 하는 방식으로 지식을 표현하도록 설계되어 있습니다. 이러한 그래프는 엔티티를 나타내는 노드와 관계를 나타내는 엣지를 포함하며 의미 정보로 풍부해집니다. 이를 통해 고수준 쿼리와 추론이 가능해지면서 단순한 데이터 검색을 넘어선다.

의미 지식 그래프의 핵심 기능은 엔티티 간의 관계를 설명하는 요소인 데이터 술어의 사용입니다. 이러한 술어는 상세 정보를 보다 폭넓은 개념에 연결시키는데 기여해 복잡한 쿼리와 추론을 가능케 합니다. DAG와 달리 의미 지식 그래프는 정보를 구조화하는 데 사용되는 체계적인 프레임워크인 온톨로지를 활용합니다. 온톨로지는 엔티티 유형, 관계, 추론 규칙을 정의하고 도메인 간 데이터 지점을 연결하며 하위 도메인 내에서 상호 연결되어 데이터의 보다 깊은 이해를 용이하게 합니다.

<div class="content-ad"></div>

# 레이블 속성 그래프 (LPGs)

데이터 및 그 관계를 나타내는 데이터 구조입니다. LPGs에서 노드와 엣지는 각각 다양한 속성을 가질 수 있어 엔티티와 네트워크 내에서의 상호 연결성을 상세히 표현할 수 있습니다. 이 속성이 풍부한 구조는 단순한 쿼리 뿐만 아니라 복잡한 분석도 지원하여 데이터 관계를 심층적으로 탐색해야 하는 애플리케이션에 이상적입니다. 그들의 견고성에도 불구하고 LPGs의 표현 능력은 구조에 의해 제한됩니다. 이는 단순한 이진 관계 이상을 나타내야 하는 시나리오에서 어려움을 겪을 수 있습니다. 이는 맥락적 추론의 기초가 되지 않는 것입니다.

# 이분 그래프

이분 그래프는 교점이 없도록 두 개의 상이한 부분 집합으로 정점의 집합을 나눌 수 있는 특수한 그래프 유형입니다. 즉, 동일 부분 집합 내의 두 정점이 서로 인접하지 않습니다. 이는 그래프의 모든 엣지가 한 부분 집합에 속하는 정점을 다른 부분 집합에 속하는 정점에 연결한다는 것을 의미합니다. 이분 그래프는 노동자와 작업을 나타내는 것과 같이 두 가지 서로 다른 객체 클래스 사이의 관계를 모델링하는 데 특히 유용합니다. 여기서 하나의 부분 집합은 노동자를 나타내고 다른 부분 집합은 작업을 나타내며, 엣지는 어떤 노동자가 어떤 작업에 할당되어 있는지를 나타냅니다. 이분 그래프는 매칭 문제를 해결하거나 네트워크 흐름을 최적화하며, Hopcroft-Karp 알고리즘과 같은 이분 매칭 알고리즘을 위한 알고리즘을 설계하는 데도 필수적입니다. 이분 그래프의 구조는 많은 계산 문제를 단순화하여 많은 실용적 응용분야에서 강력한 도구로 작용합니다.

<div class="content-ad"></div>

# RDF (Resource Description Framework) 트리플

RDF 트리플은 그래프는 아니지만 시맨틱 웹을 위한 데이터 구조화에 핵심적인 요소로 작용하는 리소스 설명 프레임워크의 중요한 부분입니다. 주어, 술어, 목적어로 구성된 각 RDF 트리플은 특정한 자원에 관한 명세적인 선언을 하여 데이터를 의미 있는 방식으로 연결합니다. 주어는 해당 자원을 나타내고, 술어는 주어와 목적어를 연결하는 관계 유형을 나타내며, 목적어는 다른 자원이나 리터럴 값이 될 수 있습니다. 이러한 구조화된 접근법은 도메인 내에 지식을 형식화하는 온톨로지(ontologies)를 만드는 것을 용이하게 합니다. RDF 트리플은 정확한 시맨틱 관계를 통해 개념을 정의하고 상호 연결하여 복잡한 데이터 검색 및 추론을 가능케 하며, 다양한 정보 시스템이나 도메인 간에 정보를 연결하는 기초를 제공합니다 — 마치 여러 주제 전문가(SME들)의 정보를 한꺼번에 연결할 수 있는 것과 같습니다.

- 시맨틱 관계: RDF 트리플은 URI(Uniform Resource Identifiers)를 사용하여 관계를 표현합니다. URI는 전역적으로 고유하기 때문에 서로 다른 데이터 항목 간에 명확하고 모호하지 않은 연결을 정의하는 데 도움이 됩니다. 이러한 전역 식별 시스템은 서로 다른 데이터 세트에서 동일한 용어가 동일한 개념을 가리키도록 보장하여 다양한 소스에서 데이터를 병합하고 질의하는 작업을 수월하게 합니다.
- 유연한 스키마: RDF는 데이터가 생성되거나 통합되기 전에 고정된 스키마를 요구하지 않습니다. 이 유연성은 RDF가 다양한 도메인에 적응하고 기존 데이터베이스 구조를 재구성하지 않고도 새로운 유형의 데이터를 통합하는 데 도움을 줍니다. 이러한 적응성은 서로 다른 시스템과 구조에서 기인한 데이터 지점을 연결하는 데 중요합니다.
- 표준화된 쿼리 언어 (SPARQL): RDF 데이터는 SPARQL을 사용하여 쿼리할 수 있습니다. SPARQL은 RDF 형식으로 저장된 데이터를 검색하고 조작하기 위해 특별히 설계된 강력하고 표준화된 쿼리 언어이며, 여러 데이터 소스에 걸쳐 복잡한 쿼리를 수행할 수 있습니다. 이와 같이 인터넷 상에 흩어져 있는 데이터 소스를 포함한 여러 데이터를 처리하는 것이 가능하여 다양한 도메인 간의 복잡한 추론과 분석을 용이하게 합니다.
- 온톨로지 추론 제공: RDF는 종종 도메인 지식의 형식화된 어휘인 온톨로지와 함께 사용됩니다. 온톨로지는 개념 사이의 구조화된 관계와 계층을 정의하며, 논리적 추론에 사용될 수 있습니다. 온톨로지에서 RDF를 사용하면 시스템이 명시적인 데이터에서 추가 정보를 추론할 수 있어 더욱 깊은 문맥적 이해와 추론을 가능케 합니다. 예를 들어, "모든 의사는 의료 전문가이다"라는 온톨로지가 있고, RDF 트리플이 "제인은 의사이다"라고 하면, 시스템은 "제인은 의료 전문가이다"를 추론할 수 있습니다.
- 상호 운용성 및 통합: RDF 프레임워크는 상호 운용성을 지원하도록 설계되었으며, 다양한 도메인에서 데이터를 연결하고 통합하는 것을 쉽게 만듭니다. RDF 형식은 데이터가 서로 다른 시스템에서 동일한 방식으로 이해되고 활용될 수 있도록 보장하여 크로스 도메인 데이터 사용 시 일반적으로 마주치는 장벽을 줄입니다.

온톨로지 생성의 기초를 탐구하고 싶다면 다른 기사를 확인해보세요.

<div class="content-ad"></div>

# 그래프 구조 해제: 그래프 네트워크를 목적에 매핑하는 수학 공식들

![Image](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_0.png)

# 맥락적 추론을 위한 주요 공식 (또는 아님)

# DAGs에 대한 선형 프로세스

<div class="content-ad"></div>

- 무사이클의 정점과 간선:

![Vertices and Edges with no cycles](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_1.png)

2. 위상 정렬:

![Topological Sort](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_2.png)

<div class="content-ad"></div>

3. 선형 관계:

![Image](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_3.png)

# 온톨로지 주도 시맨틱 지식 그래프

- 관계를 나타내는 세트:

<div class="content-ad"></div>

![이미지](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_4.png)

2. 온톨로지가 도메인 간 데이터 포인트를 연결:

   ![이미지](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_5.png)

C는 개념을, R은 관계를 나타냅니다. 이러한 온톨로지는 복잡한, 상호 연결된 데이터 표현을 가능하게 하며, 고급 시맨틱 쿼리와 도메인 간 추론을 지원합니다.

<div class="content-ad"></div>

# 레이블 속성 그래프 (LPG)는 이진 관계로 연결됩니다.

- 속성을 가진 정점과 간선:

![image](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_6.png)

2. 속성을 가진 간선:

<div class="content-ad"></div>

![이미지](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_7.png)

선형, 다중 이진 관계를 나타내는 그래프입니다. 이는 Named Entity Recognition (NER) 모델과 같은 애플리케이션에 적합하며, 각 엔티티와 관계가 특정 속성을 가지지만 복잡하지 않고 도메인 간의 연결된 데이터 포인트를 지원하지 않아 문맥적 의미 추론에 한계가 있습니다.

# 이분 그래프에서의 최대 매칭

- 최대 매칭:

<div class="content-ad"></div>

![그림](/assets/img/2024-06-27-UnderstandingGraphTypesandOntological-DrivenDataStructures_8.png)

이것은 두 가지 이상의 간선이 공통 정점을 공유하지 않는 최대 가능한 에지 집합을 나타냅니다. 이는 "최적 맞춤" 및/또는 자원 할당을 최적화하는 데 중요합니다.

주의할 점: 이러한 개념을 이해하는 것이 중요합니다. DAGs, 이분 그래프 및 기타 그래프 알고리즘은 그래프 이론에서 잘 알려져 있습니다. 각 그래프 유형은 특정한 수학적 속성과 공식을 갖고 있으며, 조합적 열거 및 위상순서와 같은 내용을 포함합니다. 의미론적 지식 그래프의 경우, 데이터 술어와 같은 추가 요소가 있어 고수준 추론을 가능하게 하고 세부 해결책 또는 최종 상태에 연결시킵니다.

워크플로우 및 Named Entity Recognition (NER) 모델의 그래프 표현은 가치가 있으며 특정 사용 사례가 있지만, 올바른 구현과 적용을 인식하는 것이 중요합니다. 이러한 개념을 오해하면 그 기능과 목적에 대해 잘못된 결론을 내릴 수 있습니다.

<div class="content-ad"></div>

"이것이 AI 그래프를 활용하는 여정에서 도움이 되길 바라며, 읽어주셔서 감사합니다!"
