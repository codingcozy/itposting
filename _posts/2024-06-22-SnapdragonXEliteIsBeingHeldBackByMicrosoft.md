---
title: "Snapdragon X Elite, Microsoft 때문에 제 성능을 발휘하지 못하는 이유"
description: ""
coverImage: "/assets/img/2024-06-22-SnapdragonXEliteIsBeingHeldBackByMicrosoft_0.png"
date: 2024-06-22 16:28
ogImage:
  url: /assets/img/2024-06-22-SnapdragonXEliteIsBeingHeldBackByMicrosoft_0.png
tag: Tech
originalTitle: "Snapdragon X Elite Is Being Held Back… By Microsoft"
link: "https://medium.com/@impure/snapdragon-x-elite-is-being-held-back-by-microsoft-05b9412c218e"
isUpdated: true
---

얼마 전에 Snapdragon X Elite에 대한 분석을 한 적이 있습니다. 이 분석은 초기 벤치마크를 기반으로 한 Qualcomm의 X Elite Matches M3 Loses To M4라는 제목의 글이었습니다. 그때는 몇 가지 출판물만이 칩을 손에 넣을 수 있었던 시절이었습니다. 그러나 지금은 Snapdragon X Elite가 공식적으로 출시되었는데, 성능은 어떨까요? 그다지 좋지 않습니다.

전에 쓴 글에서 말한 모든 것에 여전히 공감합니다. Arm에 네이티브로 컴파일된 프로그램을 실행하는 경우 Snapdragon X Elite는 좋은 칩입니다. 그러나 Arm에 네이티브로 컴파일되지 않은 프로그램을 실행할 때는 약간 문제가 발생할 수 있습니다.

그리고 Windows에는 Arm에 컴파일되지 않은 프로그램이 많습니다. 게임을 말하고 있습니다. 사실, 전 포스트에서 이에 대해 추측했던 적이 있습니다.

<div class="content-ad"></div>

아미에서 실행되도록 이전 게임을 업데이트하는 동기는 그리 많지 않아요. GTA 5 같은 경우. X Elite에서 GTA 5를 업그레이드할까요? 전혀 아니에요, 대신 GTA 6를 사세요.

라이브 서비스 게임과 구독 앱에 대해 말하고 싶은 게 있을 수 있지만, 그런 것들은 지원받아요. 제가 이에 대해 언급한 게시물 Why The Subscription Economy Is The Best Thing To Ever Happen To Software에 나와 있어요. 왜냐하면 그런 것을 지원하는 동기가 있기 때문이에요.

생각해보니 GTA 5는 기술적으로 게임 내에서 구매를 할 수 있는 방법이 있고 GTA 6는 아직 출시되지 않았기 때문에 그 게임을 아미에서 실행할 수 있도록 업데이트할 수도 있겠네요. 하지만 저는 의심스러워요. 그냥 GTA 6로 넘어가서 모든 것을 다시 사세요.

전체적으로 게임 상황이 좀 실망스러운 것 같아요. 아마도 저는 내 Steam Deck에 너무 행복해졌나 봐요. 그건 리눅스를 실행하고 있고 상당히 많은 게임이 실행되는데요. 하지만 Steam Deck은 x86-64 프로세서를 사용하고 있어서 좀 더 쉬울지도 몰라요. Steam Deck은 윈도우 시스템 콜을 리눅스 시스템 콜로 변환하면 되고요. 마이크로소프트의 프리즘에서는 실제 어셈블리 명령어를 변환해야 해요. 그 일은 더 많은 작업을 필요로 하고 심지어 애플의 로제타도 일부 앱을 변환할 수 없어요. 하지만 Apple Silicon에서 작동한 앱의 수는 처음부터 매우 높았어요.

<div class="content-ad"></div>

WWDC 2023에서 애플은 Windows x86–64 게임을 Arm으로 자동으로 이식할 수 있는 도구를 소개했어요. 이 도구는 개발자용 도구이기 때문에 문제가 있을 수 있지만 꽤 잘 작동해요.

마이크로소프트도 같은 작업을 할 수 있었으면 좋겠어요. 리뷰를 보면 Snapdragon X Elite에서 게임을 실행하는데 낮은 프레임 속도와 그래픽 아티팩트에 대해 리뷰어들이 일관되게 불평합니다. 게임이 실행되는 것조차 문제인 것 같아요.

이는 걱정스럽네요. 만약 게임이 작동하지 않으면 비즈니스 소프트웨어는 어떨까요? 실제로 필요한 것들 말이에요, 학교 과정에서도 필요한 것들 말이죠. 더 쉬운 문제일 것이라고 생각할 수 있지만 아닐 수도 있어요. Windows는 광범위한 하위 호환성을 가지고 있어서 때때로 이전 버전에서 버그까지 이식하곤 해요. 이는 마이크로소프트가 앱을 업데이트할 믿음이 없어 보일 때문일지도 모르죠. Windows 프로그램은 아주 적은 업데이트를 받아요.

보통 업데이트가 없으면 괜찮아요. 특히 윈도우가 매년, 십년마다 크게 변하지 않기 때문이죠. 하지만 Arm에서는 이것이 주요 문제가 될 것입니다. 왜냐하면 애플 실리콘이 출시되자 앱 업데이트가 아주 빨리 이루어졌는데, 윈도우에서는 그렇게 되지 않을 것 같아요.

<div class="content-ad"></div>

신규 리뷰 중에는 일부 프로그램을 실행할 수 없다는 보고가 나온 것 같아요. 업데이트가 될까요? 누가 알겠죠?

리뷰에 대해 이야기해봅시다. 일부 리뷰어들이 성능이 그리 좋지 않다고 불평을 했어요. 보고서를 충분히 선택적으로 골라내면 원하는 내용을 담긴 것처럼 만들 수 있죠. 공정하게 말하자면 Qualcomm도 상당히 선택적으로 결과를 보여줬습니다. 하지만 기술 리뷰어들도 마찬가지죠. 전체적으로 보면 이전에 보여진 것들과 크게 다르지 않은 벤치마크 결과들이에요.

아직까지는 X Elite 노트북을 몇 개만 봤습니다. 총 4개의 X Elite 칩이 있어요. 냉각 및 내부 구성품 선택도 역할을 할 수 있어요. 속도는 그렇게 걱정하지 않아요. 지난 몇 년 동안의 어떤 메인스트림 칩이라도 충분히 빠를 거에요. 더 중요한 것은 배터리 수명이에요. X Elite은 이 측면에서 잘 동작하는 것 같아요. 비록 M1 MacBook Air을 이긴 것으로 주장한 것은 아니었지만요. 시연에서 X Elite 노트북이 에너자이저 배니처럼 꾸준히 작동하는 모습을 보여줬어요. 하지만 X Elite의 다양한 변형들은 특히 다양한 전력 효율 설정에 따라 다르게 동작할 수 있어요.

그래서 X Elite에 대해 어떻게 생각하나요? 애플이 마침내 경쟁사가 생겼다는 것에 기뻐해요. 특히 그 아름다운 OLED 디스플레이들과 함께 말이에요. Vivobook S15을 사용하는 모든 리뷰어들이 화면이 얼마나 멋진지 늘 언급하고 있어요. 애플, 이제 Pro에 OLED를 넣어봐요. 무엇을 기다리고 있나요?

<div class="content-ad"></div>

새 노트북을 사려고 생각 중이었어. 사실을 말하자면, 현재 애플의 맥북 제품에 대해 그다지 만족스럽지 않아. 새로운 맥북 에어 디자인이 싫어. 저 벌써 이물감이 드네. 저 노치 때문이야, 그리고 스피커도 더 안 좋아졌어. 혹시 저만 그런 걸까? 그리 나쁘진 않지만, 확실히 나의 M1과 비교하면 다운그레이드된 기분이야.

맥북 프로도 노치가 있고, 게다가 엉망인 미니 LED 디스플레이를 달았어. 이것에 대해 너무 많이 불평을 해왔는데, 이젠 거의 웃기게까지 다가왔어. 요약하자면, 디스플레이 반응 시간이 69ms야. 그래서 이들 디스플레이를 120Hz라고 하는 건 오도독도하지. 모션 스무딩이 있는 15Hz로 마케팅되어야 하는 거야.

어떻게 할 지 모르겠어. 다만 한 가지는 확실해: X Elite 노트북은 사지 않을 거야. 고민을 했지만, iOS 개발자로서 앱을 만들려면 다른 맥이 하나 더 필요하거든. 게다가 X Elite에서 많은 프로그램이 작동하지 않는 것도 나를 걱정시켜.

얼마 전에는 X Elite에 너무 흥분했었어. 지금도 여전해. 칩이 튼튼하거든. 그러나 문제는 칩이 아니야. 문제는 x86-64에서 Arm64로의 번역 계층이야. 문제는 마이크로소프트야.
