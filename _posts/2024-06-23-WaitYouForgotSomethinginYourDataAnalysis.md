---
title: "데이터 분석에서 절대 빼먹으면 안 되는 것들"
description: ""
coverImage: "/assets/img/2024-06-23-WaitYouForgotSomethinginYourDataAnalysis_0.png"
date: 2024-06-23 16:02
ogImage:
  url: /assets/img/2024-06-23-WaitYouForgotSomethinginYourDataAnalysis_0.png
tag: Tech
originalTitle: "Wait! You Forgot Something in Your Data Analysis!"
link: "https://medium.com/@epiren/wait-you-forgot-something-in-your-data-analysis-5ecb36928e99"
isUpdated: true
---

대도시에서 배달 사업을 운영하는 소유자라고 상상해보세요. 귀하의 전달 직원은 모두 자전거를 타고 배달을 하고 있습니다. 자전거 사고로 발생하는 응급실 방문을 기반으로 한 연구 결과를 읽었습니다. "사이클링 중 부상을 입은 사람들의 데이터에 따르면, 헬멧을 착용한 사람 중 57%가 부상을 입었으며 착용하지 않은 사람은 43%입니다." 귀하의 직원들에게 어떤 것을 권장하겠습니까?

사고 발생 시 헬멧이 뇌를 심각하게 보호한다는 근거를 따를 수도 있고, 헬멧 착용으로 인해 직원들이 무모하게 움직이는 것으로 생각하여 헬멧 착용을 금지할 수도 있습니다. (그런데 헬멧을 쓰는 사람들이 더 위험한 행동을 하지는 않습니다. "위험 보상" 이론은 최선이 아니라는 점입니다.) 연구를 살펴보면, 1,000명의 자전거 타는 사람 중 133명(13%)이 사고에 연루되었으며 그 중 70명(사고에 연루된 사람 중 53%)이 응급실에 입원했습니다. 응급실에 입원한 사람 중 40명(57%)은 헬멧을 착용하고 있었고 30명(47%)은 착용하지 않았습니다.

이제 커피 마시는 사람이라고 상상해보세요. 아침 신문을 읽는 중에 커피를 놓고 의사에게 전화하고 싶어지는 기사를 보게 됩니다. 기사는 커피와 췌장암의 연관성에 대한 연구 결과를 요약합니다. "연구, 커피 섭취와 췌장암 연결,"라는 대문자 제목이 눈에 띕니다. "통계적 연관성은 커피가 암을 유발한다는 것을 증명하지는 않지만, 연구 그룹의 리더인 하버드 대학의 브라이언 맥마헌 박사는 연구 결과가 명백해지자 며칠 전 커피를 그만 먹었다고 말했습니다. 전화 인터뷰에서 그는 다른 사람들에게 조언해야 한다고 자신하지 않겠다고 말했습니다," 기사에는 이렇게 써 있습니다.

자, 충분합니다. 만약 하버드 대학의 맥마헌 박사가 자신의 연구로 인해 커피를 먹지 않는다면, 그에게 무언가가 있는 것이 분명합니다. 그렇죠?

<div class="content-ad"></div>

## 음…

일부 연구에 불쑥 스며들거나 연구 설계에서 찾지 않았을 때 발생하는 흥미로운 편향이 있습니다. 이것은 "버크슨의 편향(Berkson's Bias)"이라고 불립니다. 이것은 데이터에서 존재할 수 있는 원인과 결과 사이의 관계를 보여줌으로써 결과에 영향을 미치는 유형의 편향이지만 실제 세계에는 없을 수도 있습니다. 아니요, 당신이 이런 걸 보는 게 아니에요. 네, 당신의 데이터는 유효해요. 단지 데이터 수집 방법을 계획하는 과정에서 어떤 일이 벌어져서 이러한 잘못된 연관성이 나타난 것일 뿐입니다.

Joseph Berkson은 1946년에 이 편향을 최초로 설명했으며, 과학자들은 여전히 논문이 거절되거나 철회되거나 치명적으로 비평당하기도 합니다. 예를 들어 커피와 췌장암과 관련된 논문과 같은 경우입니다. 일어나는 현상은 연구 대상 군이 일반 대중과 비슷하지 않으므로 결론을 내릴 수 있는 것은 연구 대상 군과 유사한 사람들에게로 제한되고 전체 대중에는 해당되지 않습니다. 또는, 연구 대상 군에 다른 사람들을 분석에 포함시키지 않아 수학적으로 문제가 발생하는 것일 수 있습니다.

## 헬멧 착용은 안전합니다, 아이들여

<div class="content-ad"></div>

픽셔널 자전거 헬멧 예시로, 자전거 타는 전체 인구 즉, 1,000명에 대해 알아볼게요. 더욱 명료하게 하기 위해 이를 점으로 나열해 볼게요:

- 자전거 타는 사람은 1,000명이에요.
- 그 중 75%가 헬멧을 쓰고 있어요. 그렇게 되면 750명이 헬멧을 쓰고 있는 거죠.
- 25%는 헬멧을 쓰고 있지 않아요. 그러면 250명의 사람이 헬멧을 안 쓰고 있어요.
- 750명 중 헬멧을 쓰고 있는 사람 중 100명 (13%)이 사고를 당했어요.
- 헬멧을 쓰지 않은 250명 중 33명 (13%)이 사고를 당했어요.
- 두 그룹 모두 사고 위험이 동일해요.
- 100명의 헬멧을 쓰고 사고를 당한 피해자 중 40명 (40%)이 응급실로 가야 했고, 나머지 60명은 가지 않았어요.
- 33명의 헬멧을 쓰지 않은 사고 피해자 중 30명 (91%)이 응급실로 가야했지만, 3명은 가지 않았어요.
- 응급실 방문 위험은 헬멧을 쓰지 않은 그룹에서 높아요.
- 응급실에 들어간 70명의 피해자 중 40명 (57%)이 헬멧을 썼고, 나머지 30명 (43%)은 헬멧을 쓰지 않았어요.
- 응급실에서의 헬멧 착용 위험은 모든 사이클리스트에 대해 높아요.

마지막에 한 것을 보셨나요? 이것이 올바른 결론입니다. 사고 위험은 같지만, 응급실 방문 위험은 헬멧을 쓰지 않은 그룹이 더 높아요 (91% 대 40%). 그러나 분석은 ER의 마지막 70명만을 살펴보았으며 전체 사이클리스트 인구에 대해 고려되지 않았어요.

## Go Ahead and Drink Your Joe

<div class="content-ad"></div>

커피와 췌장암에 관한 연구에 따르면, 연구자들은 연구 대상을 일반 대중이 아닌 위장 질환 클리닉에서 선정했습니다. 그들은 클리닉에서의 췌장암 환자를 선택하고, 다른 질환으로 클리닉에 있는 사람들과 매칭시켰습니다. 결과적으로, 췌장암을 앓는 사람들이 커피를 더 많이 마신다고 보고되었습니다. 다른 질환을 앓는 사람들은 더 적게 커피를 마셨습니다. 혹은, 편집장에게 보낸 편지 중 하나에서는 다음과 같이 언급되었습니다:

이후 연구가 진행된 분석에 따르면, 연구자들이 실험군의 식이 제한을 고려하지 못했을 가능성이 있습니다. 그들은 이미 위장 질환으로 클리닉에 방문한 사람들이었고, 그 중 많은 사람들은 치료 요법으로 커피를 마시지 않고 있었습니다. 더구나, 연구는 클리닉에 있지 않은 병이 없는 많은 커피 마시는 사람들을 포함하지 않았습니다.

요약하자면, 이 연구는 연구 대상과 유사한 사람들에게만 일반화될 수 있으며, 일반 대중에게는 적용할 수 없습니다.

## 무슨 일이 있는 걸까?

<div class="content-ad"></div>

건강 관련 분야에서 참가자를 모집하지만 연구 결과를 대중에 일반화하려고 하는 경우에는 이러한 한계가 있을 수 있습니다. 연구 대상이 특정 질병 또는 상태의 최악의 경우만 분석하는 경우, 결과를 일반화하기 어렵습니다. 그리고 원인과 결과를 연관시키지만 해당 원인에 노출된 전체 인구를 고려하지 않는다면 선택편향이 발생할 수 있습니다.

아래는 이에 대한 그래픽 표현입니다:

![](/assets/img/2024-06-23-WaitYouForgotSomethinginYourDataAnalysis_0.png)

왼쪽에는 노출과 결과 사이의 약한 양의 상관 관계가 있습니다. 오른쪽에는 노출과 결과 사이의 강한 음의 상관 관계가 있습니다. 두 경우 모두 동일한 데이터 세트에서 나왔지만, 오른쪽의 경우에는 몇 가지 데이터 포인트가 누락된 선택 기준이 있었습니다. 사고 부상으로 응급실에 가지 않아도 되는 사람들이나 위장 증상으로 클리닉에 가야 하는 필요가 없는 사람들을 제외하는 경우, 연관성을 인위적으로 만들어낼 수 있습니다.

<div class="content-ad"></div>

## 그래서요?

데이터와 증거를 해석하는 방법에 주의하세요. 가장 뛰어난 두뇌도 연구에서 선택 편향이나 다른 편향에 빠질 수 있습니다. 혼동 요인에 대해서는 말도 안 돼죠. 신뢰하되 검증하는 걸 잊지 마세요... 아니면 적어도 누군가가 검증을 할 때까지 기다리세요.

커피를 즐기세요.

만약 방금 읽은 내용이 마음에 들었고 일반적인 Medium 기사도 좋은데, 우리의 작업을 지원하고 싶다면 멤버십을 획득하고 우리의 작업을 지원해 보세요! 자세한 내용은 여기를 클릭해보세요: [https://epiren.medium.com/membership](https://epiren.medium.com/membership) 감사합니다!

<div class="content-ad"></div>

René F. Najera, MPH, DrPH은 공중보건 의사이자 역학학자이며, 아마추어 사진작가이자 러닝/사이클링/수영 애호가입니다. 그는 남편이자 아버지이며, "전반적으로 훌륭한 남자"로 알려져 있습니다. 그는 공중보건 센터의 소장으로 일하거나, 지역 타코 가게에서 타코를 먹거나, 버지니아 북부의 한 대학에서 교수로 재직하며, 거기서 국제 및 지역보건학부의 부교수로 지정된 세계 최고의 공중보건 학교에서 가르칩니다. 이 블로그 글의 모든 의견은 나회자 박사의 개인 의견이며, 그의 직장, 친구, 가족 또는 지인들의 의견을 반영하는 것은 아닙니다.
