---
title: "비기술 직군 팀에 SQL을 가르치면서 얻은 교훈"
description: ""
coverImage: "/assets/img/2024-05-27-LessonsfromTeachingSQLtoNon-TechnicalTeams_0.png"
date: 2024-05-27 13:06
ogImage:
  url: /assets/img/2024-05-27-LessonsfromTeachingSQLtoNon-TechnicalTeams_0.png
tag: Tech
originalTitle: "Lessons from Teaching SQL to Non-Technical Teams"
link: "https://medium.com/towards-data-science/lessons-from-teaching-sql-to-non-technical-teams-7bd8fc9f8289"
isUpdated: true
---

## 조정된 방식에서 더 맞춤화된 방식으로 — 그리고 먼 거리에서의 코칭이 미래라고 생각하는 이유

나의 경력 동안, 내가 내부 SQL 교육을 진행하는 다양한 상황에 처해왔습니다. 이러한 교육 세션은 항상 제게 최우선 순위는 아니었지만, 가장 만족스러운 프로젝트 중 하나였습니다. 누군가가 자신의 쿼리를 실행하는 데 익숙해지고, 스스로 필요한 정보를 찾아 대시보드를 작성하며, 이 새로 습득한 기술에 흥분하는 것을 보게 되면, 나는 몰라요 — 그냥 기분이 좋습니다.

최근에, 예전에 교육받은 한 명의 "학생" 이름이 한 명의 어려운 SQL 질문을 하기 위해 공동 그룹에 등장한 것을 보았는데, 그때 나의 반응은 마치 "다크 나이트 라이즈"에서 알프레드가 브루스 웨인에게 고개를 끄덕이는 것과 같았습니다 (만약 이 참조를 모르시면 여기 있습니다).

이 기사의 목표는 내가 내부 SQL 교육을 운영하면서 처한 내 여정과 배운 점을 전달하여 전체적으로 비기술적인 (또는 적어도 SQL을 잘 알지 못하는) 팀에게 가르칠 수 있는 방법을 알려주어, 당신의 조직에서 지식의 선물을 나누고 나처럼 유사한 기쁨을 느낄 수 있기를 희망합니다.

<div class="content-ad"></div>

<img src="/assets/img/2024-05-27-LessonsfromTeachingSQLtoNon-TechnicalTeams_0.png" />

# 처음으로 이 교육을 진행한 이유

일반적으로, 나를 교육을 진행하게 한 상황은 크게 두 가지 범주로 나뉩니다:

- 역량 강화 필요: 조직 내에서 SQL 역량 부족으로 인해 한계에 부딪히는 경우가 있습니다. 이는 여러 도구와 스프레드시트를 사용하여 최종 보고서에 도달하기 위한 혼잡한 프로세스의 출현으로 일반적으로 드러납니다. 당연히 해결책이 항상 SQL 쪽에 있는 것은 아니지만, 제 경험상 시간이 많이 소요되는 다중 단계 프로세스 중 하나를 보유하고 있고 내면에 더 나은 방법이 있다고 생각한다면, 아마도 그 방법이 있을 확률이 높습니다.
- 자원 부족: 분석 관련 자원이 부족한 조직에서는 "이웃 스킬"을 갖춘 개인들(즉, 스프레드시트 및 데이터 작업에 익숙한 사람들)을 식별하고 역량 개발을 제안하는 것이 조직과 개인 양쪽에 매우 유익하다고 생각했습니다. 개인의 시야를 확대하면서 사업에 더 많은 가치를 창출할 수 있습니다.

<div class="content-ad"></div>

이러한 교육을 진행하고 싶은 이유는 다양할 수 있습니다 (위 목록이 전부가 아닙니다; 이는 상호배타적인 것도 아니라는 주장이 나올 수 있습니다). 이곳에서 이루고자 하는 목표를 명확히 하는 것이 중요합니다. 목표에 따라 교육을 실행하는 방식이 크게 달라질 수 있습니다.

# 초기 반복 사례 또는 "만능" 유형의 교육 한계를 발견한 방법

2015년의 초기 버전에서 저는 점진적인 방식을 시도해 보았습니다. 보통의 교실 형식으로, X주 동안의 프로그램을 제공했습니다. 매주 1시간씩 수업을 진행했으며(항상 같은 요일 같은 시간에), SQL을 배우고자 하는 모든 관심 있는 사람들에게 열려 있었습니다. 주로 SQL에 초점을 맞춰 진행되었습니다.

- 매주 그룹은 무언가 새로운 것을 배웠으며, SQL의 "Hello World"부터 시작해 (SELECT \* FROM TABLE LIMIT 1) CTE 여러 개로 윈도우 함수를 사용하는 방법, 쿼리 최적화까지 모두 포함했습니다.
- 각 수업 간에 그룹은 수업에서 배우는 지식을 시험하고 고착화하기 위해 숙제를 수행해야 했습니다.

<div class="content-ad"></div>

일부 사람들은 끝까지 계속했지만 성공률(성공은 누군가가 교육 후에 새롭게 습득한 SQL 기술을 계속 사용하는 경우로 정의됨)은 극히 낮았습니다. 매 세션마다 오는 사람들이 점점 줄어들었습니다. 수업 외에 제안된 연습을 하는 사람은 소수였습니다. 사실적으로 말하자면 성공하지 못했어요.

하지만 이로부터 많은 교훈을 얻었습니다:

- 멘토링을 즐겼습니다: 다른 사람들에게 새로운 기술을 가르치고 지도하는 즐거움에 대해 배웠고, 결국 이 블로그와 다른 다양한 활동을 통해 보상을 얻었다.
- SQL이 "너무 기술적이다"는 두려움: 많은 사람들이 그 무료 교육에 참여하지 않았거나 매우 첫 번째 장애물에서 포기했던 이유는 SQL을 기술적인 사람들만을 위한 것으로 생각했기 때문이고, 그들은 자신을 기술적인 사람으로 생각하지 않았기 때문입니다.
- "유지" 메커니즘 없이 교육을 실시하는 것은 실패할 운명이다: 사람들이 이 교육을 완수할 수 있을 것이라는 사람들의 자율을 믿는 것은 합리적인 생각이 아님을 이해하게 되었습니다. 어떤 조직에서든 지속적인 교육을 완수하지 않을 수 있는 많은 경쟁 우선 순위와 사유가 있습니다. 따라서 학생들을 찾아내어 교육을 듣기 위해 강한 내재적 동기부여가 있는 사람들(예: SQL을 배우기 위한 명확한 목표가 있는 경우)이나 강력한 외부적 동기부여를 제공해야 합니다(예: 그들의 매니저가 SQL을 배우라고 요구하여 더 기술적인 프로젝트를 맡을 것을 기대하는 경우).
- SQL을 가르치는 것은 방정식의 한 부분일 뿐입니다: 마지막으로, 더 중요한 것은 SQL을 가르치기 위해 SQL만을 가르치는 것이 중요하지 않다는 것을 깨달았습니다. 누구나 SQL을 고립시키지 않고 사용합니다. SQL의 현실은 다음과 같습니다:

- SQL 코드를 작성하기 전에 조직 내에서 올바른 데이터 세트를 찾아야 합니다(성숙한 조직에서 쉬울 수 있지만, 성장하기 시작한 조직이나 존재하지 않는 조직에서는 복잡할 수 있습니다).
- 데이터 세트를 찾았다면, 쿼리에 쓸 올바른 필드를 찾아야하고 이 필드가 원하는 정보를 담고 있는지 확인해야 합니다(이것 또한 하나의 기술입니다).
- 그러고 나서 데이터 세트에 액세스 권한을 요청해야 하며, 액세스 권한이 승인되면 특정 가이드라인과 기능이 있는 특정 도구에 SQL 코드를 작성해야 합니다.
- 쿼리를 작성하는 동안, 컴퓨팅 비용을 주시하고 쿼리를 실행하기 전에 필요에 따라 다시 구조를 잡아야 합니다.
- 등등. 만약 이러한 요소들을 가르치지 않는다면, 학생들이 SQL을 사용하기 어려울 것입니다.

<div class="content-ad"></div>

이 모든 배움이 나의 프로그램을 개선하는 데 길을 열었다 - 더 맞춤화된 방식으로.

# 더 최근에 - 더 맞춤화된 방향으로의 전환

위와 같이 개선된 몇 차례의 반복 뒤, 길을 따라 얻은 모든 배움을 반성하고 새로운 방식을 시도해 보았습니다: 규모를 잊고 완전히 반대 방향으로 나아갔습니다. 전체 반에서 매주 1시간 수업을 듣는 대신, 몇 명 선택된 개인들과 매주 짧은 1:1 세션을 갖기 시작했습니다.

프로그램은 여전히 누구에게나 열려 있었지만, 이제는 참여할 수 있는 사람을 선정하는 프로세스가 있었습니다. "들어가고 싶은" 사람들은 다음을 보여 주어야 했습니다:

<div class="content-ad"></div>

- SQL 학습에 대한 명확한 필요성: 잠재적인 학생들은 SQL을 배우고 싶은 이유와 SQL이 필요한 프로젝트를 설명하는 양식을 작성해야 했습니다(예: "X 보고서를 자동화하고 싶어요, Y 대시보드를 구축하고 싶어요"). 선택되면, 이 프로젝트가 프로그램 전체 기간 동안 작업할 프로젝트가 되었을 것입니다.
- 이미 있는 인접한 기술들: 잠재적인 학생들은 "인접 기술"이라고 부르는 것을 보여줘야 했습니다. 즉, SQL이나 데이터 분석을 위한 필요한 기술과 유사한 기술들을 보여주어야 했습니다.
- 일정에 충분한 시간을 할애할 수 있는 능력(및 의지): 프로그램에 대한 "신청"의 일환으로 - 학생들은 자신의 "학습" 프로젝트를 자신의 관리자와 검증하고 다음 X 주 동안 적어도 X0%의 시간을 학습에 할애할 의지가 있어야 했습니다. X0%는 많이 보일 수 있지만 - 사실 그것은 X0%에 관한 것이 아닌 메시지를 보내는 것이었습니다. 이 프로그램은 시간이 많이 소요되므로 잠재적인 학생들은 성공하기 위해 필요한 시간을 할애할 수 있는지 확인해야 했습니다.

교육 자체에 대해서 - 초점은 SQL에서 프로젝트로 전환되었습니다. 교육의 첫 세션은 그들의 프로젝트를 마일스톤으로 나누는 데 시간을 보냈습니다. 첫 번째 마일스톤은 모두에게 동일했습니다: SQL 기초를 배울 수 있는 (온라인 또는 오프라인, 무료 또는 유료 - 본인이 선호하는 것으로) 자원을 찾아내고 완료하는 것입니다.

저는 이것이 약간 실망스러울 수 있다는 것을 인식하고 싶습니다 - "SQL 가르치기"에 대한 글을 "SQL 학습" 부분에서 그렇게 탐내지 않을 것이라고 기대할 수 있습니다. 저의 일반적인 신념은 SQL의 주요 개념을 매우 짧은 시간에 배울 수 있지만, 실제로 여러 달 또는 몇 년이 걸려야 진정으로 뛰어난 수준에 도달할 것이라고 생각하며, 가능한 빨리 실제 문제에 적용하기 시작하면 더 빨리 견고한 수준에 도달할 수 있다고 생각합니다. 따라서 프로그램의 대부분은 실제 문제에 적용하는 데 소요되며, 기본적인 SQL을 이해하는 데 (인터넷의 훌륭한 것을 통해 쉽게 얻을 수 있는 것) 소요되는 시간에 대해 많은 시간이 소요되는 것은 아닙니다.

위의 첫 번째 단계가 완료되면, 우리는 다음 마일스톤을 향해 노력할 것입니다. 예를 들어, 대시보드를 구축하고 싶은 사람을 위해 프로젝트를 분할해보면:

<div class="content-ad"></div>

- SQL 기초 학습
- 적절한 데이터셋 및 쿼리 로직 찾기 (필요한 정보 획득 방법 학습)
- 필요한 경우 데이터베이스 구축 (데이터베이스 구축과 관련된 역할 및 책임)
- 이 데이터베이스를 대시보드 도구에 연결
- 대시보드 설계
- 대시보드 작성

그리고 여기서, 매주 다양한 이정표에 도달할 것으로 예상했습니다. 학생들은 주에서 어디서 걸릴 경우 언제든지 제게 피드백을 요청하거나 이메일을 보낼 수 있었지만, 일반적으로 진행 상황에 따라 독립적으로 이정표를 완수해야 했습니다.

이 시스템을 통해 낮은 실패율을 관찰했습니다 (성공은 훈련 후에 새로 습득한 SQL 기술을 계속 사용하는 사람으로 정의됩니다). 이때 뒷받침되는 이유들을 곰곰히 생각해보면 이러한 이유가 있습니다:

- 선발 과정 추가: 더해진 선발 과정은 실제 프로젝트를 가진 가장 동기가 부여된 사람들만 훈련의 일부가 되도록 보장했습니다.
- 이정표 시스템은 강제 기능이 좋았습니다: 목표를 설정하는 것은 훌륭한 시작입니다, 그러나 목표를 달성하기 위해 필요한 단계나 궁극적으로 목표를 달성할 때 필요한 작업에 대해 고민해보지 않으면 목표를 달성할 가능성이 적습니다. 명확한 마감일 아래에서 명확한 결과물을 제공하는 이정표 시스템은 학생의 성장을 크게 도와주는 책임감과 피드백 루프를 만들어냅니다.
- 처음부터 올바른 기대 설정이 모든 것을 더욱 단순하게 만들었습니다: 어떤 것을 성공으로 이끌어가는 큰 부분은 마음가짐과 일에 대한 우리의 인식과 연관이 있다고 믿습니다. 이 프로그램을 시작하자마자, 올바른 기대 설정을 하려고 노력했습니다: (1) 시간이 많이 들 것이다 (2) 도전적일 것이다 (3) 오랜 기간이 걸릴 것이다
- (4) 그러나 시간을 투자하고 도전을 하나씩 극복하겠고, 궁극적으로 승리할 것입니다
- 사람들에게 SQL 학습 방법을 가르치는 것 대 SQL을 가르치는 것: 마지막으로 — 이 주요 변경 사항이 프로그램에서 큰 차이를 만들었습니다. 이것은 사용자들이 필요한 핵심 정보를 찾아내고 실험하며 배우면서 익숙해지도록 했습니다. 그들이 더 자립적이 되어 계속成长할 수 있도록 했고, 프로그램이 종료된 후에도 지속적으로 발전할 수 있도록 했습니다.

<div class="content-ad"></div>

지금까지 위의 방법은 제가 시도한 가운데 가장 성공적인 하나입니다. 그러나 시간이 많이 소요되고 개선할 여지가 많이 보입니다.

# 보다 하이브리드 방식으로

이 시점에서 가장 중요한 질문은 다음과 같습니다: 위의 프로그램을 어떻게 확장할 수 있을까요? 이 교육에서 제가 한 역할을 반성해보면, 주로 방향을 제시하고 사람들을 정직하게 유지하는 데 중점을 두었습니다:

- 처음에: 학생들이 프로젝트를 구조화하고 단계별로 나누는 데 도움을 주었습니다.
- 각 단계마다: 각 장애물에 접근하는 가장 좋은 방법에 대한 조언을 했습니다. 만약 막힌다면, 어떻게 해제할지에 대한 지침을 제공했습니다.
- 프로그램 전반에 걸쳐: 그들의 승리를 축하하고 도전하며, 힘들 때 동기부여를 시도했지만, 동시에 그들이 설정한 일정 내에 무슨 일을 해야 하는지 제시했습니다.

<div class="content-ad"></div>

위의 내용을 자동화하는 것은 어렵지 않을까요? 혹은 혹시 LLMs를 이용해서 가능할지도 모르겠네요. 요즘 세상은 뭐가 되는지 모르겠어요. 그래도 어떻게든 표준화하고 최적화할 수 있고, 비동기적으로 많은 작업을 처리할 수 있으니 매주 회의를 필요로 하지 않는 방식으로 개선할 수 있을 거예요. 다음 반복에서 저는 학생 당 소요 시간을 줄여서 더 많은 학생들을 교육할 수 있는 방법을 시도해보고 싶네요.

저자 주: 요즘 피트니스 인플루언서들이 “거리에서의 코칭”을 제공하고 있는 것을 점점 더 많이 보게 되는데, 여기서 코치와 이메일로 소통하고 훈련 영상을 보내며 맞춤형 프로그램을 받을 수 있어요. 데이터 분석에서도 비슷한 방법이 있을 수 있을까요?

프로그램 자체에 대해, “커뮤니티” 요소를 통합하고 싶어요. 특히, 페이만 기법을 강력하게 신봉하는 편인데요. 페이만 기법은 배운 것을 가르치는 것인데요. 구체적으로 말하자면, 학생들이 배운 내용을 문서화하고 새로운 학생들에게 공유하도록 유도하고 싶어요 (마치 영화 “이웃에게 선물하기”처럼 말이에요). 여기에는 몇 가지 장점이 있을 거 같아요:

- 이를 통해 프로그램의 규모를 확장할 수 있고, 더 많은 사람들이 지식을 활용할 수 있게 될 거예요
- 이제는 선생님인 학생들이 이해해야 할 핵심 개념을 내재화하고 자신의 이해의 빈틈을 찾아낼 수 있게 도와줄 거에요
- 거대한 지식 베이스를 시작할 수 있고, 그러면 프로그램에 참여할 수 없는 고도로 동기 부여된 개인들을 위한 자기 서비스 접근 방식을 더 활용할 수 있게 될 거에요.

<div class="content-ad"></div>

항상 그렇지만, 아이디어는 쉽게 얻을 수 있어요. 실행 단계에서 어떤 것이 잘 작동하고 어떤 것이 그렇지 않은지를 이해하게 돼요. 곧 그것을 실험해 보고, 나중에 미래의 글에서 결과를 공유할 예정이에요.

# 결론

지난 8년 동안, 동료와 보고서를 SQL 전문가로 발전시키는 여러 프로그램을 시도해봤어요. 항상 성공한 것은 아니었지만, 몇 년 전에 광범위한 프로그램에서 좀 더 맞춤화된 멘토십으로 전환한 것이 많은 성공과 유익한 교훈을 안겨줬어요.

지금 나의 진정한 도전은 그 방법을 확장하는 것이에요. 어떻게 하면 선택된 개인들을 위해 최대한 가치를 창출하는 데 집중하기 위해 모든 불필요한 것을 단순화하고 제거할 수 있을까요? 그렇게 하면 그들이 자신의 조직에서 일으키는 영향력을 10배로 향상시킬 수 있게 될 거에요. 아마도 피트니스 인플루언서들이 뭔가를 알고 있을지도 몰라요…

<div class="content-ad"></div>

# 이 글을 즐겁게 읽으셨기를 바랍니다! 공유하고 싶은 조언이 있으시면 댓글 섹션에 남겨주세요!

그리고 더 많이 읽고 싶으시다면, 아마도 다음 게시물들도 맘에 드실지도 몰라요:

PS: 본 글은 다양한 분석 업무 경험을 바탕으로 얻은 지식을 담은 뉴스레터인 'Analytics Explained'에 동시 게시되었습니다. 싱가폴 스타트업부터 SF 대형 기업까지에서 배운 내용을 요약하고, 독자들의 분석, 성장, 경력에 관한 질문에 답변하고 있습니다.
