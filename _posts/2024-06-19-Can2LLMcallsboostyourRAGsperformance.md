---
title: "RAG 성능 향상에 2개의 LLM 호출이 도움이 될까요"
description: ""
coverImage: "/assets/img/2024-06-19-Can2LLMcallsboostyourRAGsperformance_0.png"
date: 2024-06-19 20:26
ogImage:
  url: /assets/img/2024-06-19-Can2LLMcallsboostyourRAGsperformance_0.png
tag: Tech
originalTitle: "Can 2 LLM calls boost your RAG’s performance?"
link: "https://medium.com/@mpattadkal/can-2-llm-calls-boost-your-rags-performance-f3d13adcbba1"
isUpdated: true
---

데이터 열정가로서, 기ꁵ적으로 우리 조직 프로젝트용 첫 번째 검색 증강 생성 (RAG) 시스템을 구축해서 정말 기뻤어요! 이 블로그에서는 현재 직장에서 차이를 만드는 실제 세계 RAG 시스템을 개발하는 과정 속에서의 좋은 일과 나쁜 일을 함께 공유하고자 해요.

![image](/assets/img/2024-06-19-Can2LLMcallsboostyourRAGsperformance_0.png)

독자 여러분을 초대해서, RAG 프로젝트 중에 직면하는 현실 세계 문제들과 이러한 도전을 극복하는 데 도움이 된 나의 사고 과정을 나누는 여행을 안내해보고 싶어요.

참고: 여기서 코드 조각은 공유하지 않겠습니다. 제 목적은 기본적인 개념과 간단한 아이디어를 결합하여 지성을 가진 제품을 만드는 방법을 보여주는 것이기 때문이에요.

<div class="content-ad"></div>

만약 RAG가 무엇인지 모르고 빠르게 이해하고 싶다면, 저의 블로그 "RAG를 활용한 RCB 경기 깊게 파헤치기"를 참고해보세요. 거기에서는 RAG를 설명하는 흥미로운 비유를 사용하고 있어요.

# 현재 상황:

내 조직의 부서는 PDF 형식의 월간 보고서로 계속 공격 받고 있어요. 이 보고서들은 우리 회사와 제휴사의 성과에 대한 정보들을 담고 있어요. 받는 PDF의 수는 진짜 수수께끼야 — 한 달에 10개를 받을 수도 있고, 다음 달에는 놀랄 만큼 25개를 받을 수도 있어! 결국 이 PDF들의 수와 구조는 아이의 기분 조절과 같이 예측할 수 없어.

# 부서가 필요로 하는 것은 무엇인가요?

<div class="content-ad"></div>

실시간 정보를 제공해주는 챗봇이 필요하다해요. 이 챗봇은 보고서 데이터에 기반하여 사용자 쿼리에 즉각적으로 답변할 수 있어야 해요. 근데 여기서 중요한 점은, 우리 사용자들은 데이터 초보자가 아니에요. 그들은 최고경영자(CXOs), 성공을 거둔 사람들이에요. 그들의 질문들은 신뢰할 수 있는 정확한 답변을 요구해요. 어떠한 불규칙성이나 모순이라도 절대 안돼요!

간단히 말해서, 우리는 PDF 보고서의 변화무쌍에 대처할 수 있는 스마트한 데이터 중심 챗봇이 필요해요. 이 챗봇이:

🌊 PDF 보고서의 변화무쌍을 처리할 수 있어야 해요.
🤖 복잡한 사용자 쿼리에 정확하고 실시간으로 답변할 수 있어야 해요.
💼 우리 경영진팀의 신뢰할 수 있는 조언자가 되어야 해요.

# 기본 솔루션은 무엇인가요?

<div class="content-ad"></div>

내 첫 번째 생각은 전통적인 NLP 기술을 사용하지 않는 것입니다. 데이터가 구조화되지 않은 형식이며 전통적인 NLP 기술은 사전 처리를 많이 필요로 하며 시간이 오래 걸립니다. RAG의 장점은 사전 처리의 복잡성을 제거하고 정보에 직접 액세스할 수 있다는 것입니다. Llama 지수 프레임워크는 더 높은 수준의 멋있음을 더했습니다. 가장 멋진 것은 PDF 리더를 기본으로 탑재하여 문서를 실시간으로 구문 분석할 수 있다는 것입니다. 이는 RAG가 PDF에서 텍스트와 테이블을 스스로 직접 수집할 수 있다는 것을 의미합니다.

내 첫 단계는 간단한 RAG 시스템을 구축하는 것이었습니다 (기초부터 구축한다고 생각해보세요). 그 모든 PDF를 사용하여 거대한 인덱스를 만들었습니다 — 정보의 검색 가능한 보물창고입니다. 사용자가 질문을 할 때마다, 그것은 슈퍼 강력한 사서처럼 인덱스에서 가장 관련 있는 문서를 검색했습니다.

이러한 최종 후보들과 사용자의 질의는 그런 다음 Mistral 7B로 보내졌습니다(우리의 내부 LLM으로 8k 토큰의 컨텍스트 길이를 가지고 있습니다). Mistral 7B는 이 정보를 사용하여 답변을 만들었습니다.

간단한 RAG를 평가한 결과, 이는 고수준 쿼리(예: 성능 요약, 메트릭 값을 비교하는 질문)에 대해 잘 작동하지만 구체적인 답변이 필요한 질문의 경우에는 완전히 실패했다는 것을 이해했습니다.

<div class="content-ad"></div>

사용자 쿼리 - "2024년 1월 XYZ 범주의 성과 지표 값은 무엇인가요?"

간단한 RAG는 사용자 쿼리에 "1월"이라고 언급되었기 때문에 2022년, 2023년 및 2024년 1월에 모든 문서를 검색했습니다. 그런 다음, 가장 관련성이 높은 상위 10개의 문서가 LLM(언어 모델)에게 문맥을 제공하도록 전송되었습니다. 이것은 합리적으로 보였습니다. 더 많은 1월 정보, 더 나은 답변이 되는 것이 맞죠?

안타깝게도, 그것은 그렇게 간단하지 않았습니다. LLM은 때때로 특정 사용자 쿼리에 가장 관련성이 높은 것이 아닌 2022년 1월 문서를 기반으로 응답을 생성했습니다. 이것은 retriever가 "1월"과 같은 일반 키워드로 인해 해당 문서들이 순위가 더 높게 매겨졌기 때문입니다. 결과는 잘못된 답변들이었습니다!

이 순간에 저는 YouTube 채널/블로그에서 가르쳐지는 간단한 RAG가 샘플 데이터에서만 잘 작동하는 것을 깨달았습니다. 실제 시나리오에서는 종종 실험을 해보지 않으면 답을 찾을 수 없는 도전에 마주하게 됩니다. 그래서 이제 각 구성 요소를 실험하여 무엇이 작동하고 무엇이 실패하는지 이해하기로 결정했습니다.

<div class="content-ad"></div>

시도 번호 1:

개선을 위한 초기 탐색 작업은 두 가지 옵션을 포함했습니다: 더 큰 LLM 사용 또는 재랭킹 모델 구현. 먼저 더 큰 LLM을 선택했고, 인상적인 32k 토큰 컨텍스트를 갖춘 GPT-4로 전환했습니다. 놀랍게도 성능 향상이 크지 않았습니다. 이것이 나를 "아하!"하게 만드는 순간이었는데, 가장 관련 있는 문서들이 초기에 나오도록 해야 했고, GPT-4는 초기 문서들을 우선시하는 것으로 보였습니다.

GPT-4를 재랭킹 모델과 결합하는 것이 유망한 해결책으로 보였습니다. 따라서 제가 설계한 RAG를 그림 3에 표시한 대로 만들었습니다.

평가 결과, 결과가 좋아 보여서 RAG를 배포하고 테스트를 진행하기로 확신을 갖게 되었습니다. 그러나 여기서 또 다른 변화가 있었습니다 - 비용 및 보안 이유로 조직이 사내 LLM인 Mistral 7B를 사용하기를 선호했습니다.

<div class="content-ad"></div>

그래서, 그림판에 다시 들어가 보죠! Mistral 7B와 Reranker 모델에 갇혀 있네요.

시도 번호: 2

성능을 향상시킬 수 있는 견고한 검색기가 필요했다는 문제를 알았어요. 그래서 다양한 검색기를 실험해봤는데, 하이브리드 검색기, 쿼리 퓨전 검색기 등을 사용해보았지만, 결국 어느 것도 제게 만족스러운 결과를 주지 못했어요.

시도 번호: X (카운트를 잃어버렸네요)

<div class="content-ad"></div>

이 곳에서 Llama 지수에서 "메타데이터 필터"를 발견했어요. "메타데이터 필터"를 사용하면 특정 태그가있는 문서 세트를 필터링할 수 있어요. 리트리버는 이러한 필터링 된 문서만 사용하여 관련 문서를 검색할 거예요. 여기서 전략을 생각해봐요. 만약 모든 문서에 연도, 분기 또는 월과 같은 메타데이터를 표시하면 검색 시에 이러한 태그를 찾아볼 수 있겠죠.

처음 단계는 각 문서에 메타데이터를 할당하여 지수를 재생성하는 것이었어요.

예: 문서에 다음과 같은 텍스트가 있는 경우

"XYZ 부서는 2023년 Q1에 대단히 잘 수행되었습니다. 2022년 Q1의 성과와 비교하면, 이 숫자는 정말 기분 좋아요"

<div class="content-ad"></div>

메타데이터 필드를 감지하기 위해 정규식 표현식을 사용했지만 결국 정규식이 작동하지 않는 경우가 있음을 깨달았어요.

예: "ABC의 반기 성과는 2023년에 대단한 것이었습니다"라는 문서 텍스트가 있다면,

정규식 표현식은 문서에 언급된 연도만 감지하지만, 이 문서는 반기를 나타내는 Q1과 Q2에 대한 언급도 있습니다. 이 때, 돌파 아이디어가 떠올랐죠. LLM을 사용하여 메타데이터를 식별하고 태깅하는 것이 어떨지요. 이 문서를 LLM에 전달하자, LLM은 반응했어요.

이것 좋지 않나요? LLM을 사용하여 문서를 정확하게 태깅하고 그 주변에 메타데이터를 만드는 것. 모든 문서를 LLM에 전달하는 것은 비용이 많이 들 것 같다고 생각할 수 있어요. 솔직히 말하자면, 이것은 N개의 문서를 LLM에 전달한다면 비용 부담이 크지만, 이것은 일회성 활동이기 때문에 고정비용이며 RAG 시스템을 사용하는 사용자 수와는 무관합니다.

<div class="content-ad"></div>

문서마다 메타데이터를 생성한 후 색인을 재생성했어요. 이제 고급 RAG의 플로우 다이어그램은 Figure 4와 같이 보여요.

Figure 4에서 알 수 있듯이, 색인에는 메타데이터가 있는 문서가 포함되어 있어요. 이제 사용자 쿼리가 접수되면 먼저 LLM(화살표 no. 1)로 보내져 메타데이터 필드를 식별하고, 이 필드들은 사용자 쿼리에 추가되어 검색기(화살표 no. 2)로 보내져요. 검색기는 메타데이터를 기반으로 문서를 필터링하고 관련 문서를 가져와요. 나머지 과정은 앞서 소개한 RAG들과 유사해요. 이 RAG를 평가한 결과, GPT-4를 사용했던 이전 최고의 RAG보다 성능이 더 좋았어요.

# 결론

Mistral 7B와 같은 작은 LLM이 제한처럼 보일 수 있지만, 사실은 비밀병기였어요! 핵심은 내가 그것을 어떻게 활용했느냐였어요 — 한 번이 아니라 두 번이나! 비결은 여기 있었어요: 먼저 Mistral 7B를 사용해 사용자 쿼리에서 중요 정보(메타데이터)를 추출했어요. 이를 통해 검색 프로세스는 가장 관련성 높은 문서를 정확히 찾을 수 있었어요. 그런 다음, Mistral 7B는 이러한 집중된 문서 집합과 원래 쿼리를 사용해 최종 응답을 만들어냈어요.

<div class="content-ad"></div>

"더블 역할" 접근법 덕분에 GPT-4와 같은 강력한 LLM을 능가할 수 있었어요. 결론은 더 작은 LLM의 힘을 과소평가하지 말아야 한다는 거죠! 전략적으로 활용하면 검색과 응답 생성에 굉장히 효율적일 수 있어요.

의견란에 어떠한 제안이나 질문이 있으면 말씀해 주세요.
