---
title: "마라톤 결과의 연령 그레이딩을 위한 더 나은 시스템이 있을까요"
description: ""
coverImage: "/assets/img/2024-06-19-IsThereaBetterSystemforAgeGradingMarathonResults_0.png"
date: 2024-06-19 01:33
ogImage:
  url: /assets/img/2024-06-19-IsThereaBetterSystemforAgeGradingMarathonResults_0.png
tag: Tech
originalTitle: "Is There a Better System for Age Grading Marathon Results?"
link: "https://medium.com/runners-life/is-there-a-better-system-for-age-grading-marathon-results-71ffdc1fc138"
isUpdated: true
---

<img src="/assets/img/2024-06-19-IsThereaBetterSystemforAgeGradingMarathonResults_0.png" />

서로 다른 두 명의 러너 사이에 경주 결과를 공정하게 비교하려면 어떻게 해야 할까요?

예를 들어, 세 명의 러너가 모두 3:00에 마라톤을 완주했다고 가정해 봅시다. 표면적으로 보면 세 명 모두 잘 한 것으로 말할 수 있습니다.

하지만 그 세 명의 러너가 25세 남성, 40세 여성, 60세 남성이라면 어떨까요? 그 시간은 각각의 러너에게 동일한 만큼 힘든 것이 아닙니다. 그렇다면 누가 가장 우수한 성적을 거뒀을까요?

<div class="content-ad"></div>

지난 몇 십 년 동안 연령 등급이 시도해 온 질문입니다. 최근 연재한 몇 개의 기사에서 이 문제를 탐구해 왔습니다.

전통적인 연령 등급 체계는 유용하며 비교를 하나의 방법으로 분류하는 데 도움이 됩니다. 그러나 그것은 결함이 없는 것은 아닙니다.

성적을 하나의 숫자로 단순화한다는 점 때문에 항상 정확하고 신뢰할 수 있는 객관적인 측정이라고 생각하는 함정에 빠지기 쉽습니다.

마라톤 성적의 비교적인 강도를 대략적으로 나타내기 위해 몇 가지 대규모 결과 데이터 세트를 수집해 분석한 결과, 성적을 연령별 백분위수로 비교하는 대안을 제시하고 있습니다.

<div class="content-ad"></div>

이 시리즈를 따라오셨다면 다음 두 링크가 가장 흥미로울 것입니다:

- 2023 데이터를 사용하여 업데이트된 (그리고 향상된) 연령 등급 계산기 버전을 확인할 수 있습니다.
- 퍼센타일을 계산하는 데 사용한 2023 데이터셋의 공개 버전이 여기 있습니다. Kaggle에서 데이터를 사용하거나 CSV 형식으로 전체 데이터셋을 다운로드할 수 있습니다.

# 데이터에 관한 주요 사항

이 문제에 대해 처음 작업을 시작할 때, 2010년부터 2019년까지의 마라톤 샘플로 구성된 데이터셋으로 시작했습니다. 그 순간에는 명확한 결과를 고려하지 않고 데이터를 탐색했습니다.

<div class="content-ad"></div>

퍼센타일이 탐색할 수 있는 좋은 옵션이라고 결정한 후, 2023년 미국 내 모든 마라톤 대회를 포함한 새 데이터셋을 수집했어요.

만약 데이터 분석 도구를 잘 다룬다면, 전체 데이터셋을 Kaggle에 업로드했어요: 2023 마라톤 결과. 또한 데이터를 불러오고 데이터를 간단히 탐색하는 샘플 노트북도 공유했어요.

전체 데이터셋은 641개의 레이스와 42만 9천개가 넘는 개별 완주 시간을 포함하고 있어요.

그러나 퍼센타일 테이블을 계산하는 데 사용한 데이터는 약간 더 작아요. 일부 결과에는 연령 데이터가 없어서 제외되었어요. 또한 LA 마라톤, CIM, 콜로라도와 같은 몇몇 레이스 데이터가 부족했고, 나중에 데이터셋에 추가되었어요.

<div class="content-ad"></div>

아래 공유하는 분석은 대략 40만 건의 경주 결과를 기반으로 합니다. 추가 데이터를 수집한 후 90번째 백분위를 확인하여 유의미한 차이가 있는지 확인했고, 그 차이는 단 10초 정도였습니다.

# 전통적인 연령 평가 방식은 어떻게 작동합니까?

그렇다면 전통적인 연령 평가 방식은 무엇이며, 왜 우리가 가진 방법을 그대로 사용하지 않아야 하는지 알아야 할까요?

전통적인 연령 평가 방법론은 지난 몇 10년 동안 발전해 왔습니다. 하지만 핵심적으로 이것이 어떻게 작동하는지 살펴보겠습니다.

<div class="content-ad"></div>

신뢰도 있는 경험적 관찰과 통계 분석을 통해 세계 마스터스 애슬레틱스는 사람이 나이를 먹을수록 얼마나 느려지는지를 추정하는 표를 만들었습니다. 선수의 시간을 나이 계수로 곱하면 나이에 비해 얼마나 빠른지를 알 수 있는 나이 등급 시간이 나옵니다 - 더 어려운 선수일 때의 동등한 시간입니다.

따라서, 60세 남성의 원래 예시에서 나이 계수는 0.8331입니다. 만약 그가 3시간(10,800초) 동안 경주를 한다면, 나이 등급 시간은 2:29:58이 될 것입니다 (0.8331 \* 10,800).

25세 남성의 경우, 3시간 결과는 좋지만 놀라운 것은 아닙니다. 그러나 60세 남성의 경우, 이는 25세 남성에게 2:30 마라톤에 해당한다고 여겨집니다 - 정말 놀라운 것입니다.

여기서 멈춰서 시간을 비교할 수도 있습니다. 또는 마지막 단계로 넘어가서 나이 등급 시간을 그 이벤트의 표준 시간으로 나눌 수도 있습니다 - 일반적으로 표가 작성된 당시 오픈 세계 기록입니다.

<div class="content-ad"></div>

남자 마라톤의 이전 세계 신기록 2:01:39를 나누면 결과물인 2:29:58의 점수는 81.12%가 됩니다. 수여를 위해 나이 그레이딩 결과를 제공하는 경우 레이스 결과에서 일반적으로 볼 수 있는 것이죠. 이것은 성적 등급 퍼센트(PPL)라고도 불리워요.

# 그러면, 이 방법에는 무엇이 문제인가요?

저는 전통적인 나이 그레이딩 시스템에 몇 가지 비판과 문제점이 있지만, 가장 중요한 것은 두 가지로 요약할 수 있다고 생각해요: a) 교정과 b) 유용성.

## 교정에 대한 명확한 문제점들이 있습니다.

<div class="content-ad"></div>

이 두 문제 중에서 더 문제가 되는 것은 때로는 나이 등급 계산이 신뢰할 수 없다는 점이며, 일부 연령군이 다른 연령군보다 좋은 점수를 획들기 쉽다는 것입니다.

이 시리즈의 이전 기사에서는 2023년에 나이 등급별 상위 1,000명을 조사하여 나이와 성별별 분석을 살펴봤습니다. 여기 몇 가지 데이터 점:

- 35세 미만 남성은 전체 샘플에서 1,000명 중 221명을 대표했지만, 나이 등급별 상위 1,000명 중 368명을 획득했습니다.
- 45~59세 남성은 샘플에서 1,000명 중 65명을 대표했지만, 나이 등급별 상위 1,000명 중 39명만을 획득했습니다.
- 60~64세 여성은 샘플에서 1,000명 중 14명을 대표했지만, 나이 등급별 상위 1,000명 중 27명을 획득했습니다.
- 65~69세 여성은 샘플에서 1,000명 중 단 6명이었지만, 나이 등급별 상위 1,000명 중 20명을 획득했습니다.

나이 등급이 실제로 경기장을 평평하게 만들고 다른 연령군과 성별을 비교할 수 있는 신뢰할 수 있는 방법을 제공한다면, 상위 1,000명의 분포는 일반 러너들의 분포와 유사해야 합니다. 그러나 일부 뚜렷한 불일치가 있습니다.

<div class="content-ad"></div>

Boston Marathon 예선 시간 분석에서 나타난 이 문제의 또 다른 예는 남성의 경우입니다.

35세 미만 남성의 예선 시간은 가장 높은 연령 등급 결과 중 하나가 필요하며, 질 충전 비율도 가장 낮다는 것은 예상할 수 있습니다. 이 부분은 이해됩니다.

그러나 여성의 경우에는 명백한 문제가 있습니다. 50대 여성의 예선 시간은 20대, 30대 또는 40대 여성의 시간보다 높은 연령 등급 결과가 필요합니다. 이러한 시간이 동등하게 어려울 경우, 50대 여성 중 예선을 통과하는 비율이 더 낮을 것으로 예상됩니다.

그러나 실제로는, 그들이 더 높은 비율로 통과합니다. 45-49세 여성만 예외입니다. 60대 여성은 연령 등급으로 볼 때 비슷하게 엄격한 기준이 있으며, 그들은 더 높은 합격률을 보여줍니다.

<div class="content-ad"></div>

만일 연령 등급 시스템이 적절하게 보정되었다면, 자격 요건 시간의 상대적 연령 등급이 서로 다른 연령 그룹의 자격 달성률을 대략적으로 반영할 것으로 예상됩니다. 그러나 이 두 가지 사이에 일치하지 않는 것은 어떤 부분이 문제가 있다는 신호입니다.

이에 대한 가능한 이유들은 여러가지가 있지만, 제 추측으로는 a) 더 어린 연령 그룹의 엘리트 경쟁, b) 일부 더 늙은 연령 그룹의 이상값 결과, 그리고 c) 특히 여성들의 일부 더 늙은 연령 그룹 규모가 작기 때문에 일어난 결과일 것이라고 생각합니다.

## 연령 등급에 의해 제공되는 유용한 정보는 무엇인가요?

두 번째 문제는 — 여러분의 의견은 달라질 수 있습니다 — 연령 등급이 제공하는 정보가 얼마나 유용한지입니다.

<div class="content-ad"></div>

나이 그레이드의 특성은 100%에 가까워질수록 시간의 차이가 적어져도 나이 그레이드에 더 큰 차이가 난다는 것이죠.

예를 들어, 50세 남성이 2시간 35분의 마라톤을 뛴다고 가정해봅시다. 멋진 성과네요. 86.45%의 나이 그레이드를 받습니다. 다섯 분을 줄이면, 2시간 30분의 결과는 89.33%가 됩니다.

그러나, 중간부로 갈수록 시간의 큰 차이가 있어도 나이 그레이드에서는 작은 차이를 보입니다. 만약 50세 남성이 4시간의 레이스를 뛴다면, 평균 이상의 성과입니다. 55.83%의 나이 그레이드를 받습니다.

다섯 분을 줄이면, 3시간 55분은 약간 더 좋아집니다. 57.02%에 해당합니다. 그가 나이 그레이드를 3% 더 올리려면 거의 15분이 더 달려야 할 것입니다.

<div class="content-ad"></div>

이 경우 테이블 태그를 Markdown 형식으로 변경하십시오.

<div class="content-ad"></div>

그래서 대중들과 비교하는 대신 나 자신을 그들과 비교하게 되는 이유가 뭘까요?

# 대안은 무엇일까요? 백분위수.

제가 제안하는 대안은 특정 연령 및 성별 그룹의 다른 모든 러너와의 비교 결과를 기반으로 하는 것입니다.

러너들의 분포를 가지고 — 예를 들어 50-54세 남성 — 당신은 모든 결과를 정렬하여 90%의 다른 러너보다 빠른 시간이 얼마나 걸릴지, 또는 75%, 또는 50%, 등을 볼 수 있습니다.

<div class="content-ad"></div>

모든 연령 그룹에서의 시간 분포는 유사합니다. 탁월한 성적을 낸 소수의 러너들, 평균 주변에 처한 러너들이 점차 증가하며, 훨씬 더 느린 시간에 도달하는 소수의 러너들이 있습니다.

![이미지](/assets/img/2024-06-19-IsThereaBetterSystemforAgeGradingMarathonResults_1.png)

러너들이 나이를 먹을수록 분포가 약간 오른쪽으로 이동하지만, 일반적인 모양은 동일합니다. 충분히 많은 수의 러너들을 대상으로 고려하면, 그들이 정말 훌륭한 성적, 좋은 성적, 평균적인 성적, 혹은 평균 이하 성적으로 크게 분할될 것으로 예상됩니다.

따라서 50세의 남성이 50세의 다른 남성 중 90%보다 빠르게(3시간 18분 8초) 달리면, 90%의 동료들을 이기는 40세 여성(3시간 32분 22초)과 거의 동등한 성적을 거둡니다.

<div class="content-ad"></div>

최적 시간에 의존하는 대신 나이 관련 감소가 그 시간의 감소로 나타나는 것을 기다릴 필요가 없습니다. 대신 백분율을 사용하면 전체 시간 분포를 기반으로 하여 모든 참가자와 비교할 수 있습니다.

# 백분율은 나이 측정에 실패한 곳에서 동작합니까?

그렇다면 위에서 언급한 두 가지 불만족에 대해 백분율은 어떻게 대처할까요?

백분율이 전통적인 나이 측정보다 더 정확하게 보정되는가요? 대부분의 러너들에게 보다 유용한 정보를 제공하나요?

<div class="content-ad"></div>

## 백분위수가 더 잘 보정되나요?

한 마디로?

네.

위의 시각화는 세 가지를 보여줍니다:

<div class="content-ad"></div>

- 1,000명당 각 연령/성별 그룹의 완주자 수 (파란색)
- 나이 등급에 따른 각 연령/성별 그룹의 상위 1,000명 완주자 수 (보라색)
- 백분위로 나눈 각 연령/성별 그룹의 상위 1,000명 완주자 수 (분홍색)

잘 보정된 측정은 파란색 막대와 유사해야하며, 잘 보정되지 않은 경우에는 종종 차이가 날 것입니다.

파란색 막대와 보라색 막대 사이에 명백한 불일치가 있습니다.

여성들 중에서, 나이가 어린 연령 그룹(35-49세)은 매우 소외되어 있고 노인 연령 그룹(60-79세)은 매우 과대표시되어 있습니다. 남성들 중에서는, 35세 미만 그룹이 지나치게 과대표시되어 있고, 35-49세 그룹은 약간 소외되어 있습니다.

<div class="content-ad"></div>

파란 막대와 분홍 막대가 항상 동일하지는 않지만, 그들 사이의 차이는 훨씬 적습니다.

각 측정 항목의 총 분산을 더하면, 백분위수는 117의 총 분산을 가지고 있고, 연령 등급은 그것의 세 배가 넘는 383의 총 분산을 가지고 있습니다.

만약 연령 등급의 목표가 최상위 완주자가 어떤 성별과 연령 그룹에서든 동일하게 나올 가능성이 있는 보다 공정한 경기 환경을 만드는 것이라면, 백분위수를 사용하는 것이 이미 존재하는 연령 등급 시스템을 사용하는 것보다 더 적절하게 보정되어 있습니다.

## 백분위수는 더 유용한 정보를 제공할까요?

<div class="content-ad"></div>

의견은 각양각색일 수 있지만, 저는 이렇게 생각해요.

제 개인적인 진척 상황을 예시로 들어볼게요.

37세 때, 저는 3시간 35분으로 마라톤을 뛰었어요. 38세 때, 3시간 20분으로 뛰었고요. 39세 때, 3시간 10분을 달성했어요. 그리고 40세 때, 3시간 08분을 뛰었죠. 실제로 10월에 시카고에서 3시간을 넘어설 것이라고 가정해봅시다 (제 생각에는 상당히 가능하다고 생각해요).

나이 그레이딩으로 따지면, 제 진척은 다음과 같습니다:

<div class="content-ad"></div>

- 56.58% - 61.15% - 64.83% - 66.00% - 69.23%

그리고 백분위로 따지면 제 발전은:

- 71.53% - 80.34% - 85.20% - 88.13% - 92.53%

나이 그레이딩을 고려하면 이런 개선은 꽤 중요하지 않아 보일 수도 있어요. 56.58%는 꽤 평균적으로 들릴 수 있어요 — 하지만 37세 남성의 중간 완주시간(4:06)을 월등히 뛰어넘는 3:35에요. 그리고 69.23%는 그다지 더 인상적으로 들리진 않을 수 있어요.

<div class="content-ad"></div>

백분위수는 저와 동료들 간의 성과를 더 잘 이해할 수 있게 해주고, 시간이 지남에 따라 어떻게 변화하는지 보여줍니다. 제 초기 시간(3:35)은 평균보다 우수했지만 놀라울 정도는 아니었습니다. 한편, 10월의 목표 시간은 평균 마라톤러와 비교했을 때 상당히 좋지만(비켈레와의 격차가 많이 남은 것은 사실입니다).

정말 중요한 질문은 이겁니다: 최고를 대비하려는 건가요? 아니면 동료들과 비교하려는 건가요?

제가 최고와 정당하게 경쟁할 가능성이 거의 없다면, 나 자신을 동료들과 비교하는 것이 훨씬 더 합리적으로 보입니다. 그리고 그를 위해 백분위수가 더 유용한 도구인 것 같습니다.

# 백분위수가 완벽한가요?

<div class="content-ad"></div>

안녕하세요!

표를 마크다운 형식으로 변경해주세요.

고맙습니다!

<div class="content-ad"></div>

다른 문제는 연장된 연령 그룹에는 충분히 많은 러너가 없어 신뢰할 수 있는 분포를 만들어내기 어렵다는 것입니다. 70대 여성과 70대 후반 / 80대 남성을 대상으로 하면 문제가 발생하기 시작합니다.

이를 개선하기 위해 몇 가지 수학 모델링을 통해 분포를 완화시킬 수 있습니다. 하지만 이러한 러너들을 위한 더 신뢰할 수 있는 데이터셋을 구축하기 위해 더 많은 데이터가 필요합니다.

아마도 2024년 말까지 또 다른 한 해 동안의 데이터가 추가된다면, 작업을 업데이트하고 일부 개선을 할 수 있을 것입니다.

# 이 도구를 직접 활용하는 방법은 무엇인가요?

<div class="content-ad"></div>

이전에 독자들이 마라톤 성적을 백분위로 계산하고 전통적인 연령 점수와 비교할 수 있는 계산기를 만들었습니다.

그 도구를 업데이트하여 새로운 2023 데이터에서 생성된 백분위 표를 반영했습니다.

연령 점수 계산기는 여기에서 이용할 수 있습니다.

또한 계산기를 개선했습니다. 빠르게 작동하고 오류가 발생하면 더 정확하게 실패합니다.

<div class="content-ad"></div>

지금은 이것을 만들어서 내 웹사이트(Running with Rock)에 호스팅했어요. 당신이 러닝 웹사이트를 운영하고 계시고 본인만의 계산기 버전에 관심이 있다면 알려주세요. 실제로 관심이 있는 사람이 있다면 워드프레스 플러그인이나 유사한 것을 만들어볼 수 있을 거에요.

# 다음은 뭐가 있을까요?

지금까지 이 토끼굴을 끝까지 쫓아갔어요. 데이터를 몇 차례 반복하고 유용한 도구를 만들었어요.

나는 이것이 나이 등급과 개인 러닝 퍼포먼스 레벨(PLPs)을 대체할 것이라는 환상은 없어도, 이것이 가치 있는 관점을 제공한다고 생각해요.

<div class="content-ad"></div>

이제부터, 내가 고민 중인 몇 가지 다른 질문들이 있어요. 아마도 다음 몇 주 안에 그에 대해 글을 쓸 것 같아요:

- 이전에 보스턴 마라톤에서 날씨가 미치는 영향에 대한 기사를 썼어요. 이에 대한 후속 기사를 작성 중이고, 타임 예선자와 미예선자 간의 잠재적 차이를 살펴볼 계획이에요.
- 성별에 따라 러너들의 분포가 시간에 따라 어떻게 변화하는지 살펴보고 있어요. 특히, 연령 그룹 간의 차이와 여성이 데이터에서 역사적으로 배제된 흔적이 여전히 있는지 궁금해요.
- 나이 등급 및 백분위와 관련된 몇 가지 질문들도 있어요 — 그리고 이 시리즈와 별도로 각 주제를 더 자세히 탐구할 거에요.

만약 이러한 질문들에 관심이 있다면 — 또는 마라톤에 관한 데이터 기반 이야기에 대해 다른 이야기를 원한다면, 이메일 업데이트를 구독해 주세요.

저는 열렬한 러너이자 데이터 열정가에요. 제가 무엇을 하고 있는지 따라가는 방법은 다음과 같아요:

<div class="content-ad"></div>

- 나의 훈련에 대해 알고 싶다면 Running with Rock을 팔로우하세요.
- 마라톤 훈련 계획 선택에 관한 팁을 읽어보세요.
- Strava에서 제 프로필을 염탐하세요.
