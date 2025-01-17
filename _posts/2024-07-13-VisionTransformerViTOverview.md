---
title: "비전 트랜스포머 ViT 개요 2024 최신 기술 분석"
description: ""
coverImage: "/code-tower.github.io/assets/no-image.jpg"
date: 2024-07-13 03:32
ogImage:
  url: /code-tower.github.io/assets/no-image.jpg
tag: Tech
originalTitle: "Vision Transformer (ViT) Overview"
link: "https://medium.com/@zakhtar2020/vision-transformer-vit-overview-1baa0d173ab5"
isUpdated: true
---

비전 변형(Vision Transformer, ViT)은 이미지 분류에 대한 새로운 접근 방식으로, 자연어 처리 작업에서 매우 성공적인 트랜스포머 아키텍처를 활용합니다. 구글 연구원들이 소개한 ViT는 이미지 데이터를 패치의 시퀀스로 취급하고 이러한 시퀀스에 트랜스포머 모델을 적용함으로써 이미지 처리 방법을 재정의합니다. 이 접근 방식은 이미지 분류 파이프라인을 간소화하고 최첨단 성능을 달성합니다. 이곳에서 ViT의 자세한 개요를 확인할 수 있습니다:

## 1. 소개

비전 변형(Vision Transformer, ViT)은 원래 텍스트 처리를 위해 설계된 트랜스포머 아키텍처를 이미지 데이터에 적용합니다. 이미지를 패치로 분할하고 이를 시퀀스로 처리함으로써, ViT는 트랜스포머의 장거리 종속성과 복잡한 패턴을 포착할 수 있는 능력을 활용합니다. 이 방법은 이미지를 처리하기 위해 합성곱을 사용하는 전통적인 합성곱 신경망(CNN)과는 다릅니다.

이미지를 패치의 시퀀스로: 합성곱 대신에 ViT는 이미지를 고정 크기의 패치로 나누고 이러한 패치를 펼쳐서 토큰처럼 다루어 시퀀스에서 단어와 같이 처리합니다.

<div class="content-ad"></div>

## 2. 구조

**이미지 패치 임베딩:** 입력 이미지는 겹치지 않는 패치로 나누어집니다. 각 패치는 펼쳐지고 선형 투사를 사용하여 고정 차원의 임베딩 공간으로 매핑됩니다. 이러한 임베딩은 공간 정보를 유지하기 위해 위치 인코딩과 결합됩니다.

**트랜스포머 인코더:** ViT의 핵심은 패치 임베딩 시퀀스를 처리하여 전체 이미지에 대한 표현을 생성하는 표준 트랜스포머 인코더입니다. 인코더는 다중 헤드 셀프 어텐션 및 피드포워드 신경망으로 구성된 여러 레이어로 이루어져 있습니다.

**인코더 구성요소:**

<div class="content-ad"></div>

**Key Components and Concepts**

Patch Embedding: 이미지는 고정 크기의 패치(예: 16x16 픽셀)로 분할됩니다. 각 패치는 펼쳐지고 선형 변환을 거쳐 벡터로 변환되어 패치 임베딩의 시퀀스를 생성합니다. 이 단계는 2차원 이미지 데이터를 트랜스포머 모델에 적합한 형식으로 변환하는 중요한 과정입니다.

- Multi-Head Self-Attention: 모델이 동시에 시퀀스의 다른 부분에 주의를 기울일 수 있도록 하는 것으로, 패치 사이의 복잡한 종속 관계를 포착합니다.
- 피드 포워드 네트워크(FFN): 각 임베딩에 대해 독립적으로 동일하게 변환을 적용하여 모델이 복잡한 패턴을 학습할 수 있는 능력을 향상합니다.
- 위치 인코딩: 이미지의 각 패치의 원래 위치에 대한 정보를 유지하기 위해 패치 임베딩에 추가됩니다.

분류 헤드: 트랜스포머 인코더를 통해 패치를 처리한 후, 특별한 분류 토큰(CLS)에 해당하는 표현을 사용하여 최종 이미지 분류를 수행합니다. 이 토큰은 모든 패치에서 정보를 집계하여 전체 이미지를 대표합니다.

<div class="content-ad"></div>

위치 부호 인코딩: 트랜스포머는 순차적으로 시퀀스를 처리하지 않기 때문에 순서에 대한 감각이 부족합니다. 공간 정보를 보존하기 위해 ViT는 각 패치 임베딩에 위치 부호 인코딩을 추가합니다. 이러한 인코딩은 원본 이미지에서 각 패치의 위치를 나타내는 고정된 벡터입니다.

자기 주의 메커니즘: 자기 주의는 모델이 예측을 수행할 때 서로 다른 패치의 중요성을 가중치로 고려할 수 있게 합니다. 각 패치 쌍에 대해 주의 점수를 계산하여 이미지의 관련 부분에 집중하도록 모델을 유도합니다.

분류 토큰 (CLS): 특별한 토큰이 패치 임베딩 시퀀스 앞에 추가됩니다. 이 토큰은 모든 패치에서 정보를 종합하고 분류 작업을 위한 최종 표현으로 사용됩니다. 최종 분류 헤드는 이 토큰을 처리하여 출력 클래스 확률을 생성합니다.

## 4. 주요 기능 및 이점

<div class="content-ad"></div>

- 확장성: ViT는 대규모 데이터셋과 모델 크기에 효율적으로 확장되며, 트랜스포머 아키텍처의 능력을 통해 대량의 데이터와 복잡한 패턴을 처리할 수 있습니다.
- 단순성: 이미지를 패치 시퀀스로 취급함으로써, ViT는 복잡한 합성곱 레이어가 필요 없는 전통적인 CNN에 비해 아키텍처를 간단화합니다.
- 최신 성능: ViT는 다양한 이미지 분류 벤치마크에서 최신 CNN에 비해 경쟁력이나 우수한 성능을 달성합니다.
- 전이 학습: ViT는 자연어 처리로부터 사전 훈련된 트랜스포머 모델을 활용할 수 있어, 이미지 작업에서 효과적인 전이 학습과 세밀한 조정이 가능합니다.

## 5. 응용 분야

이미지 검색:

- 콘텐츠 기반 이미지 검색: ViT를 사용하여 콘텐츠에 기초한 대규모 데이터베이스에서 이미지를 검색하고 검색할 수 있으며, 효율적인 이미지 검색과 정리를 실현할 수 있습니다.
- 예술과 역사 아카이브: ViT는 예술 및 역사 아카이브에서 이미지를 조직화하고 검색하는 데 도움이 되어 가치 있는 시각 정보에 대한 연구와 접근을 용이하게 합니다.

<div class="content-ad"></div>

생성 모델:

- 이미지 합성: ViT는 생성 모델에서 사용되어 새로운 이미지를 합성하며, 미술 창작, 엔터테인먼트, 가상 현실 등의 응용 프로그램에 기여할 수 있습니다.
- 이미지 초해상도: ViT는 저해상도 이미지의 해상도를 향상시켜 시각화와 분석을 위해 명료하고 자세한 이미지를 제공할 수 있습니다.

물체 감지 및 분할:

- 자율 주행: ViT는 자율 주행 차량에서 실시간으로 물체를 감지하고 분할하여 차량의 환경을 이해하고 탐험하는 능력을 향상시킵니다.
- 로봇 시각: ViT는 로봇이 물체를 감지하고 분할하여 조작 작업에 도움을 줌으로써 물리적 세계와 상호 작용을 향상시킬 수 있습니다.

<div class="content-ad"></div>

### 6. 결론

비전 트랜스포머(Vision Transformer, ViT)은 비주얼 데이터에 변환자 모델을 적용하여 이미지 분류에서 패러다임 변화를 일으키고 있습니다. 이미지를 패치의 시퀀스로 처리하는 방식은 아키텍처를 단순화하는 동시에 최신 성능을 달성합니다. 의료 영상 및 문서 분석에서 이미지 검색 및 이상 징후 감지에 이르기까지 다양한 분야에 적용되며, ViT는 다양성과 효과성을 입증하고 있습니다. 확장 가능성, 단순성, 그리고 뛰어난 성능은 이미지 분류 및 그 이상의 기능을 발전시키는 데 유용한 도구로서 ViT를 만들어냅니다.

참고 자료:

[논문 링크](https://arxiv.org/abs/2010.11929)
