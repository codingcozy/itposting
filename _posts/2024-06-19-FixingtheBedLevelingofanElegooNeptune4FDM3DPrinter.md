---
title: "이글루 넵튠 4 FDM 3D 프린터의 침대 레벨 조절 문제 해결하기"
description: ""
coverImage: "/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_0.png"
date: 2024-06-19 17:32
ogImage:
  url: /assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_0.png
tag: Tech
originalTitle: "Fixing the Bed Leveling of an Elegoo Neptune 4 FDM 3D Printer"
link: "https://medium.com/the-unpopular-opinions-of-a-senior-developer/fixing-the-bed-leveling-of-an-elegoo-neptune-4-fdm-3d-printer-cd48b38ab2ff"
isUpdated: true
---

<img src="/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_0.png" />

# 소개

Elegoo Neptune 4는 중국에서 만들어진 FDM 3D 프린터입니다. 대부분 오픈 소스 전자제품 및 소프트웨어를 기반으로 하지만, 인쇄 하드웨어의 설계 및 구현은 (대부분) Elegoo에 고유합니다. 이 프린터들은 적절한 FDM 중심 모델에 대해 훌륭한 인쇄물을 만들어낼 수 있지만, 시간이 지남에 따라 정확도가 떨어져 실패하는 인쇄물이 늘어납니다.

나는 이러한 프린터들과 가지는 문제 그리고 Elegoo와 넵튠 4 소유주 커뮤니티에서 제공하는 다양한 해결책을 연구하는 데 많은 시간을 투자했습니다. 나는 이러한 프린터들의 가장 큰 문제인 침대 수동 레벨링의 빈번한 필요성에 대한 해결책을 찾았다고 믿습니다.

<div class="content-ad"></div>

이 프린터들은 FDM 인쇄용 CoreXZ 디자인을 사용하며 Bedlsinger로도 알려집니다. 이 이름은 프린트 헤드가 X와 Z 축만 움직이고, Y 축 이동은 침대를 단일 평면에서 빠르게 움직여 처리한다는 사실에서 유래했습니다. 빌드할 단단한 표면을 제공하여 플라스틱 덩어리와 그 플라스틱을 인쇄가 완료될 때까지 가열하는 침대는 상당한 무게를 지지합니다. 이러한 침대의 빠른 가속 및 감속은 침대를 지지하는 하드웨어와 침대를 움직이는 하드웨어에 상당한 힘을 전달합니다. 이 침대는 침대를 격렬하게 흔들어서 (따라서 Bedslinger라는 용어가 나온 것) 프린터 전체와 프린터가 올려져 있는 표면을 교란시킬 수 있습니다.

가장 최근 (이 글은 2024년 6월에 작성됨)의 FDM 프린터, 특히 Bedslinger는 가속도계를 사용하여 입력 형태를 수행하여 프린터 소프트웨어가 움직임에 의해 생성되는 힘을 예측하고 GCODE (인쇄물을 부가적으로 생성하는 방법을 설명하는 언어)에서 명령을 수정할 수 있도록 합니다.

Elegoo Neptune 4의 침대는 알루미늄 프레임을 통해 Y 축 구동 장치에 장착되며, 이 프레임에는 M4 사이즈 스크류가 통과되는 네 개의 나사 구멍이 있습니다. 그리고 그 후면을 통과한 네 개의 금속 스프링을 사용하여 프레임과 침대 플레이트 사이에 조절 가능한 서스펜션 역할을 하는 스프링을 넣습니다. 이 네 개의 스크류는 침대를 프레임 아래에 고정시키고, 침대의 네 꼭지점마다 적용되는 긴장을 줄이거나 늘려서 각각의 높이를 조절할 수 있도록 하는 성형 핸드 너트를 사용합니다. 이는 높이를 설정하는 아날로그 메커니즘을 제공하며, 숙련된 사용자가 침대 수평 조정을 0.025밀리미터의 정확도로 조정할 수 있도록 하는 높이의 무한한 변화를 제공합니다 (이는 헤드의 z-위치 센서의 정확도입니다).

이 침대 수평 조정 스크류는 입력 형태의 가속도계가 추가되기 전부터 FDM 프린터의 기능이었습니다. 이 두 기능 모두 따로는 좋지만, 함께 사용하면 두 가지 기능의 약점을 악화시킵니다.

<div class="content-ad"></div>

# 문제점

넵튠 4 시리즈 프린터를 작동시키는 소프트웨어인 Klipper는 침대의 모양을 유지하는 맵을 유지하고, Z 위치 센서의 마지막 알려진 보정을 유지하며, 프린터가 움직임에 의해 전달되는 힘을 분석하기 위해 보정 프로필을 사용합니다. 마지막 데이터 조각은 입력 형태를 위해 사용됩니다. Klipper가 프린트용 GCODE를 구문 분석할 때, 요청된 움직임에 가속도와 감속도를 적용하여 프린트 헤드가 관성 때문에 잘못된 위치에 남을 가능성을 최소화합니다. Klipper 입력 형태는 ALL3DP에서 잘 다루는 복잡한 주제입니다. 요약하면, Klipper의 각 설치에는 입력 형태를 위해 일부 매개변수가 설정되어야 합니다. 넵튠 4는 공장에서 미리 설정되어 있지만, 링크된 기사의 지침을 사용하여 특정 프린터에서 입력 모양을 개선할 수 있습니다.

Klipper가 프린터의 물리적 설계를 기반으로 한 상수 집합을 사용하는 사실은 문제 발생의 시작입니다. 이러한 상수는 각 개별 프린터에서 관찰된 주파수에 기반하지 않습니다. 프린터를 받아올 때 튜닝 타워 테스트를 실행하고 그 값을 적용하면 다른 값이 나오므로 꼭 해야 합니다. 그러나 프린터에 시간이 지남에 따라 발생하는 변화나 인쇄하는 환경과 관련된 변화 같이, 프린터에 발생하는 변화들은 이러한 설정의 정확성에 상당한 영향을 미칠 수 있으므로 자주 해야 합니다.

또 다른 문제점이 있습니다: 그 탄성. 침대를 수평으로 맞추기 위해 스프링을 사용함으로써 프린터의 설계는 두 개의 별도 질량을 만듭니다. 프린터의 프레임은 침대가 이동하는 프레임에 견고하게 연결되어 있습니다. 이를 탄성이 없는 질량이라고 하며, 그 움직임은 쉽게 측정하고 예측할 수 있습니다. 앞서 설명한 대로, 가열 침대는 스프링에 떠서 프레임 위에 떠 있어서, 가열 침대에서 발생한 진동을 흡수하고, 삽을 통해 가열 침대로 진동을 전달할 수 있습니다. 이러한 감쇠 및 증폭 효과는 각 스프링의 정확한 장력에 대한 캘리브레이션을 실행할 때만 예측이 가능합니다. 스프링 중 하나라도 장력이 변하면, 조정 스크류를 의도적으로 돌리거나 인쇄 중에 스크류가 풀리는 것과 같은 이유로, 보정은 더 부정확해지며 입력 형태 기능은 프린터 부품의 움직임을 개입하는 데 과다하거나 부족하게 대응할 것입니다.

<div class="content-ad"></div>

안타깝게도, Elegoo Neptune 4의 디자인은 침대를 수동으로 레벨링 한 후 스프링의 긴장을 물리적으로 잠그는 방법을 포함하지 않습니다. 이 디자인은 스프링의 긴장만으로도 몸통을 막을 수 있다고 단순하게 가정합니다. 이는 믿을 수 없을 만큼 나쁜 디자인 선택입니다. 잠금 기구 없이 프린터의 조절 다이얼이 종이 위에 프린트하는 중에 완전히 나사에서 벗어나 있는 상황이 자주 발생했습니다. 이런 일이 발생하면 침대판의 기하학적 형태와 프린터에 적용되는 주파수가 전부 변하게 되며, 프린팅 중인 내용물이 높이로 밀려 프린트 헤드의 방향으로 이동되거나, 노즐 아래의 간격이 너무 줄어 결과적으로 불안정한 상태로 인쇄물이 생성되는 일이 매우 자주 일어나게 됩니다. 이는 종종 프린트 헤드에 새로운 핫엔드를 설치해야 하는 상황으로 이어지는데(필라멘트가 핫엔드의 전선을 감싸기 때문에 모두 효과적으로 제거하기가 매우 어렵기 때문입니다).

Elegoo에게 인정할 만한 점은, 제거할 수 없는 플라스틱이 결과로 올 때 핫엔드를 새로 보내 주겠다는 것입니다. 그러나, 프린터를 더 신중하게 설계한다면 이 비용을 아낄 뿐만 아니라 더 신뢰할 수 있는 프린터로 평판을 높일 수도 있을 것입니다.

# 이 디자인에서의 문제 해결하기

이 문제에 대한 일반적인 해결책은 스프링을 스페이서로 교체하는 것입니다. r/ElegooNeptune4의 Reddit에서 이에 대해 읽은 후, 먼저 스페이서를 출력하였으나 이러한 스프링과 같이 쉽게 변형되어 움직이는 것으로 나타났습니다. 그 후 알루미늄 스페이서를 구매했지만, 이러한 것으로 침대를 레벨링하려면 침대와 스페이서 사이에 워셔를 쌓아야 했는데, 각 코너를 작업할수록 점점 더 어려워졌습니다. 사용 가능한 워셔는 2mm 두께와 0.5mm 두께뿐이었습니다. 이것은 스프링이나 출력된 스페이서보다 정확도가 훨씬 떨어지는 0.5mm 주변으로 침대를 레벨링 할 수 있는 최상의 방법인 것으로 알려졌습니다. 더 얇은 워셔를 찾아 구매해야 한다는 것을 고려할 때 나는 깨달음을 얻었습니다.

<div class="content-ad"></div>

너는 개발자야. 위 텍스트를 친근한 어조로 한국어로 번역해주세요.

스페이서를 제거하고 M4 볼트를 히트 베드에 안정하게 고정할 너트로 교체하고, 베드 프레임에 히트 베드를 안정하게 고정할 추가 너트를 달았어. 이로 인해 두 가지 문제의 해결책을 찾았어:

- 네 모서리의 위치를 Z 축에 대해 고정시킬 수 있었어.
- 히트 베드를 베드 프레임에 안전하게 연결하여 스프링 질량을 제거하고 스프링으로 인한 힘을 없앴어.

이것은 침대를 레벨로 조정하면 유지될 것이고, 입력 모양을 교정하면 정확할 것임을 의미해 (환경 및 히트 베드 위의 플라스틱 구조의 영향을 무시한다 가정할 때).

이 프로세스를 통해 이 프린터의 제조에 대해 배우고 프린터 기능에 불리한 결정 몇 가지를 발견했어. 먼저, 핫 베드에 있는 경사 각도의 구멍이 조립 중 사용되는 원뿔형 M4 볼트에 너무 커서 문제가 되었어. 이로 인해 M4 볼트가 경사면에 안정적이고 직선적으로 놓이지 않아 볼트가 베드 프레임에 수직이 아니게 되는 상황이 발생하게 돼. 이는 다시 볼트가 베드 프레임의 구멍과 올바르게 정렬되지 않도록 하게 해. 스프링을 사용할 때는 이 문제가 좀 덜하지만, 이 기술을 적용할 때 볼트를 히트 베드에 안전하게 고정하는 데 더 신경을 써야 한다. 그럼에도 불구하고, 스프링을 사용할 때도 볼트의 머리가 경사되게 놓일 수 있어서 볼트가 히트 베드에 수직이 아닐 수 있어. 또 다른 문제는 베드 프레임 자체가 상당히 약하고 쉽게 구부러진다는 것이야. 이것은 주어진 무게를 가볍게 가져가야 한다는 필요 때문에 의도된 디자인 선택이라는 것을 깨달았는데, 더 나은 지지 구조는 더 큰 강성을 제공하여 인쇄물의 치수 정확도를 크게 향상시킬 수 있을 거야.

이 변화를 적용하는 것은 간단하지만, 이후 침대를 레벨로 조정할 때 주의와 주의가 필요하다는 점을 명심해야 해.

<div class="content-ad"></div>

# 단계별

## 이 모드를 완성하기 위해 필요한 것은 M4 나사를 위한 너트 8개뿐입니다.

단계 1: 침대 조절 너트를 침대 프레임 아래에서 모두 풉니다. 조절 너트는 나중에 다시 사용할 것이므로 옆에 놓아 두세요.

단계 2: 히트 베드를 프레임에서 제거합니다. M4 볼트는 나중에 다시 사용할 것이므로 옆에 놓아 두세요. 침대를 원래의 어셈블리로 되돌리고 싶을 경우를 대비해 스프링을 컨테이너에 넣어 두세요.

<div class="content-ad"></div>

3단계: M4 볼트를 침대에 다시 넣고 침대를 평평하고 수평한 표면 위로 뒤집어 놓으세요. 볼트들은 각 경사면에 딱 맞지 않을 것이므로 너무 걱정하지 마세요.

4단계: 각 M4 볼트에 M4 너트를 꽃아넣고 너트를 다 꽉 돌려 침대에 딱 맞게 끼웁니다. 구멍이 상당히 크기 때문에 열로인팅과 M4 너트 사이에 M4 워셔를 사용하는 것이 좋습니다. 볼트를 구멍 가운데에 정확히 위치시켜 열 로인팅에 가능한 한 수직으로 가깝게 위치하도록 노력해야 합니다. 볼트의 각도에 만족하면 렌치로 M4 너트를 꽉 조여주어야 합니다 (손으로 너무 헐거운 정도는 충분하지 않습니다) M4 볼트를 잠금 상태로 고정하세요. 이 과정은 매우 중요하며 인쇄 중 무작위로 발생하는 힘을 방지합니다.

![이미지](/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_1.png)

5단계: 손 너트를 나사에 꽃아넣고 나사의 길이의 절반 정도로 내려놓습니다. 이는 각 코너의 침대 높이를 세밀하게 조절하는 데 사용됩니다.

<div class="content-ad"></div>

<img src="/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_2.png" />

6단계. 침대를 뒤집어서 M4 볼트를 침대 프레임의 구석 구멍에 넣고 손 나사 위에 놓으십시오. 모서리마다 M4 볼트 아래에 최소 5mm가 있는지 확인하십시오. 각 M4 볼트 아래에 M4 너트를 꼭지로 병합하여 난방 침대를 침대 프레임에 고정하십시오. 이 시점에서 침대는 수평이 멀리 떨어져 있지만, 괜찮습니다.

7단계: 프린터에 Fluidd Web UI를 엽니다. 이를 위해 웹 브라우저를 열고 http://`프린터 IP 주소`로 이동하면 Fluid Web UI가 열립니다. Edge를 사용하여 앱으로 Fluidd Web UI를 프린터에 추가하여 시작 메뉴와 작업 표시줄에 쉽게 고정시킬 수 있습니다.

<img src="/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_3.png" />

<div class="content-ad"></div>

왼쪽에서는 콘솔 아이콘을 선택하여 클리퍼 콘솔을 열 수 있습니다.

![Console Icon](/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_4.png)

프린트 헤드를 홈 포지션으로 이동시키는 명령(G28)을 입력하세요. 이렇게 하면 엑스트루더가 침대의 중앙 부근 및 침대 위 약 10mm의 곳에 위치하게 됩니다.

![Home Command](/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_5.png)

<div class="content-ad"></div>

다음으로 프린트 헤드를 나사 #1의 위치로 이동시키세요. 이들을 수동으로 찾아 31mm x 31mm 뜨거운 베드의 각 모서리로부터 떨어져 있다는 것을 알고 있습니다. 아래 명령어를 입력하여 프린트 헤드를 해당 위치로 이동시킨 후, PROBE 명령을 사용하여 이 지점에서 베드의 높이를 측정하세요.

![image](/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_6.png)

측정한 높이를 기록하세요. 이러한 위치를 사용하여 사각 나사의 높이를 찾기 위해 동일한 절차를 따르세요. 아래 명령어를 복사하여 Klipper 콘솔에 붙여넣기하여 한꺼번에 모든 명령을 실행할 수 있습니다.

```js
G28

M118 Screw 1, Front Left
G1 X31 Y31 Z10
PROBE

M118 Screw 2, Rear Left
G1 X194 Y31 Z10
PROBE

M118 Screw 3, Rear Right
G1 X194 Y194 Z10
PROBE

M118 Screw 4, Front Right
G1 X194 Y31 Z10
PROBE
```

<div class="content-ad"></div>

<img src="/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_7.png" />

가장 높은 지점에 있는 나사를 확인한 후, 이 구석을 최대한 0에 가깝게 조절한 다음에 M4 너트로 그 나사를 잠그고, 그 나사 밑에 있는 M4 볼트에 M4 너트를 사용해 고정합니다. 제 침대의 경우, 오른쪽 앞쪽 (나사 4)이 가장 높은 지점에 있습니다. 이는 히트 베드의 자연적인 변동으로 인한 결과입니다. (위의 스크린샷은 이미 이러한 단계를 따른 결과이며, 당신의 값은 더 많이 달라질 것입니다.)

각 나사를 조절하기 위해서, 측정을 진행할 때마다 두 개의 명령을 내리게 됩니다.

```js
G1 X31 Y31 Z10 ; X31은 가로 31mm를 의미하고, Y31은 세로 31mm를 의미하며, Z10은 침대 위 10mm를 의미합니다.
PROBE
```

<div class="content-ad"></div>

지난 단계의 위치를 사용하십시오. 각 나사를 가능한 한 0에 가깝게 만드는 것이 목표입니다. 처음으로 잠글 나사부터 시계 방향으로 작업할 것입니다. 나사의 위치를 확정하면 베드프레임 아래의 M4 너트를 조여서 꽉 고정할 것입니다. 높이를 설정하기 위해 써냄깃고리를 사용하여 베드를 프레임에서 멀리 밀어낸 후, 베드프레임 아래의 M4 너트를 사용하여 히팅 베드를 베드프레임에 가깝게 당길 것입니다. 써냄꽃개와 M4 너트를 고정한 후, 두 명령을 한 번 더 실행하십시오. 베드프레임이 굽는 현상에 관한 이전 코멘트를 기억하세요? 이것이 정말 중요한 때입니다. 각 나사를 고정할 때마다 다른 세 개의 장착 포인트에 힘을 가하게 되며, 베드프레임의 모양이 바뀌게 됩니다. 모든 나사 위치를 시계 방향으로 이동하여 어떠한 조정도 필요하지 않고 베드 주위를 완전히 돌 수 있을 때까지 계속하셔야 합니다. 제 프린터의 경우, 주로 베드 주위를 세 번 돌게됩니다.

베드를 레벨링 한 후, Z-Offset을 설정해야 합니다. Elegoo는 이 과정을 보여주는 괜찮은 비디오를 제공합니다.

ELEGOO NEPTUNE 4/ PRO: 제일 레이어의 Z-축 오프셋을 정밀 조정하는 방법 (youtube.com)

다음으로, ALL3DP 기사에 따라 프린터의 입력 형태 주파수를 보정하는 단계를 따르십시오. 프린터의 이동 바디 구조를 근본적으로 변경했으므로, Elegoo에서 제공하는 기본 값과 극명하게 다른 보정 값을 가질 수 있음에 놀랍지 마십시오.

<div class="content-ad"></div>

# 결론

이 모드는 내 Elegoo Neptune 4 프린터 사용 방식을 완전히 바꿨어요. 이전에는 매일 수동으로 베드 레벨링을 해야 했어요. 어떤 날은 각 출력물 사이에도 해야 했죠. 지금은 베드 레벨을 생각할 필요도 없어요. 내 출력물은 치수 정확성에서 훨씬 일정해요. 그리고 무엇보다, 매번 출력하기 전에 베드 메쉬를 보정할 필요가 없어요!

![이미지](/assets/img/2024-06-19-FixingtheBedLevelingofanElegooNeptune4FDM3DPrinter_8.png)

이 기사를 작성하면서 (아무것도 빠뜨리지 않기 위해) 다시 이 모드를 적용한 결과, 이게 내 베드 메쉬의 모습이에요. 0.1975 mm의 차이는 0.2mm 레이어 높이로 출력해도 베드 어디에서든 안전하게 출력될 거에요. 만약 차이가 의도한 레이어 높이보다 크다면, 차이가 레이어 높이보다 낮아질 때까지 레벨링 프로세스를 진행해야 해요. 대부분의 슬라이싱 소프트웨어는 초기 층을 다른 레이어 높이로 사용할 수 있게 해요. 일반적으로 모든 출력물의 초기 층에는 0.3mm를 사용하지만, 본체 출력물에 더 작은 레이어 높이를 사용할 예정이더라도요. 이 초기 층 높이가 실제 차이 목표에요. 차이보다 초기 층 높이가 높으면, 필라멘트가 베드에 눌리지 않아 부착이 부족할 확률이 낮아져 성공적인 출력물을 얻을 수 있어요. 이 모드를 적용한 후에도 베드 부착이 여전히 좋지 않다면, 노즐을 교체하거나 새로운 자석식 빌드 플레이트를 사용해야 할 수도 있어요. 무엇보다도, 이 모드를 적용한 이후로 덩어리가 생기지 않았어요.
