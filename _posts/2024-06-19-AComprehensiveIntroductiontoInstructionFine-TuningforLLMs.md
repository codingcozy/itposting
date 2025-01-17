---
title: "LLM을 위한 지시어 파인 튜닝에 대한 포괄적인 소개"
description: ""
coverImage: "/assets/img/2024-06-19-AComprehensiveIntroductiontoInstructionFine-TuningforLLMs_0.png"
date: 2024-06-19 03:09
ogImage:
  url: /assets/img/2024-06-19-AComprehensiveIntroductiontoInstructionFine-TuningforLLMs_0.png
tag: Tech
originalTitle: "A Comprehensive Introduction to Instruction Fine-Tuning for LLMs"
link: "https://medium.com/towards-artificial-intelligence/a-comprehensive-introduction-to-instruction-fine-tuning-for-llms-c9d66e4bae08"
isUpdated: true
---

지시 튜닝은 큰 언어 모델(LLM)의 능력을 특정 지시를 따르도록 개선하기 위해 사용되는 과정입니다. InstructGPT의 작업은 먼저 지시 미세 조정에 대한 작업을 소개했습니다.

InstructGPT는 인간 지시를 더 잘 따르도록 GPT-3를 미세 조정하여 학습되었습니다. 인간이 모델의 응답을 평가한 데이터셋에서 GPT-3를 조정하는 것은 ChatGPT를 만드는 방향으로 큰 발전이었습니다.

이 문서에서는 기존 LLM의 성능을 향상시키기 위해 지시 미세 조정하는 과정과 결과를 배우게 됩니다. 또한 미세 조정한 LLM의 성능을 평가하고 기본 모델과의 개선 정도를 양적으로 측정할 수 있는 중요한 지표에 대해 알게 될 것입니다.

![image](/assets/img/2024-06-19-AComprehensiveIntroductiontoInstructionFine-TuningforLLMs_0.png)

<div class="content-ad"></div>

## 목차:

- 지시사항 프롬프트를 사용한 LLMs 세밀조정
- 세밀조정 과정
- 지시 데이터 세트 준비
- 지시 세밀조정 프로세스
- 평가 및 성능 측정 지표

# 1. 지시 프롬프트를 활용한 LLMs 세밀조정

큰 LLMs 및 GPT3와 같은 기본 모델들은 프롬프트에 포함된 지시사항을 식별하고 올바르게 zero-shot 추론을 수행할 수 있지만, 더 작은 LLMs와 같은 다른 모델들은 작업을 수행하지 못할 수도 있습니다.

<div class="content-ad"></div>

예를 들어, "불어로 이 문장을 번역해주세요: '안녕, 어떻게 지내세요?'"라는 지시를 받으면 능력있는 LLM은 비슷한 번역 예시를 볼 필요 없이 올바른 번역 "Bonjour, comment ça va?"를 생성할 수 있습니다.

그러나 더 작은 LLM들이나 덜 포괄적인 훈련 데이터를 갖고 있는 LLM들은 또는 더 복잡한 작업에 대해서 적절한 작업을 제대로 수행하기 위해 안내 없이 어려움을 겪을 수 있습니다. 이를 해결하기 위해 one-shot 및 few-shot 추론 기술이 사용되는데, 여기서 한 번 또는 몇 가지 예제가 모델이 작업을 이해하는 데 도움이 됩니다.

예시: One-Shot 추론

- 프롬프트: "이 문장을 독일어로 번역해주세요: '좋은 아침.' 예시: '어떻게 지내세요?' - ` 'Wie geht es dir?'""
- 모델 출력: "Guten Morgen."

<div class="content-ad"></div>

여기서 모델은 제공된 예시를 사용하여 "Good morning"을 올바르게 번역하는 방법을 추론합니다.

예시: Few-Shot 추론

- 프롬프트: "다음 문장을 프랑스어로 번역하십시오: '안녕히 가세요.' 예시: '안녕' -` 'Bonjour'. '고맙습니다' -` 'Merci'."
- 모델 출력: "Au revoir."

몇 가지 예시를 제공함으로써, 모델은 번역 작업에 대한 더 나은 이해를 얻고 정확한 결과를 내놓습니다. 파인 튜닝은 LLM의 가중치를 업데이트하기 위해 레이블이 지정된 예시를 사용하여 기본 모델을 더 학습시키는 솔루션을 제공합니다.

<div class="content-ad"></div>

# 2. 지시 사항 세부 조정 과정

이전에 대비해서, 선행 교육에서는 LLM을 자기 지도 학습을 통해 거대한 양의 비구조화된 텍스트 데이터를 사용하여 훈련했지만, 지시 사항 세부 조정은 레이블이 지정된 예제 데이터 세트를 사용하여 LLM의 가중치를 업데이트하는 지도 학습 과정입니다.

레이블이 지정된 예제는 프롬프트-완료 쌍이며, 세부 조정 프로세스는 모델의 훈련을 확장하여 특정 작업에 대한 좋은 완료를 생성할 수 있는 능력을 향상시킵니다.

다양한 작업에 대한 지시 사항 세부 조정 예시:

<div class="content-ad"></div>

- 텍스트 분류:

  - 작업: 영화 리뷰의 감정 분류
  - 프롬프트: "이 리뷰의 감정을 분류하세요: '나는 이 영화를 정말 좋아했어요! 처음부터 끝까지 멋있었어요.'"
  - 완료: "감정: 긍정적"

2. 텍스트 요약:

   - 작업: 기사 요약
   - 프롬프트: "다음 기사를 요약하세요: '주식 시장은 역대급 성장을 보여주었으며, 주요 지수가 사상 최고치를 기록했습니다. 투자자들은 경제의 회복에 대해 낙관적입니다.'"
   - 완료: "요약: 경제 회복에 대한 낙관주의 속에서 주식 시장이 사상 최고치를 경신했습니다."

<div class="content-ad"></div>

3. 번역:

- 작업: 영어 문장을 프랑스어로 번역하십시오.
- 프롬프트: “다음 문장을 프랑스어로 번역하십시오: ‘The weather is nice today.’”
- 완료: “Le temps est agréable aujourd’hui.”

4. 질의응답:

- 작업: 주어진 텍스트를 기반으로 질문에 답하십시오.
- 프롬프트: “다음 글을 읽고 질문에 답하십시오: ‘중국의 만리장성은 세계에서 가장 유명한 구조물 중 하나입니다. 침입으로부터 보호하기 위해 건설되었습니다.’ 질문: 만리장성은 왜 지어졌습니까?”
- 완료: “만리장성은 침입으로부터 보호하기 위해 건설되었습니다.”

<div class="content-ad"></div>

5. Named Entity Recognition (NER):

- Task: 명명된 Entity(개체)를 식별하고 분류합니다. 예를 들어, 사람, 조직, 위치 등
- 지시문: "다음 문장에서 Entity(개체)를 식별하고 분류하세요: 'Barack Obama was born in Hawaii and served as the President of the United States.'"
- 완성: "Barack Obama: 사람, Hawaii: 위치, President of the United States: 직책"

지시서 파인튜닝은 특정 지시에 대한 모델의 반응을 보여주는 예시를 사용하여 다양한 작업에서 모델의 성능을 향상시키는 데 특히 좋습니다. 지시서 파인튜닝의 가장 중요한 장점 중 세 가지는 다음과 같습니다:

- 작업별 전문 지식: 레이블이 지정된 예시를 통해 특정 작업에 대해 직접 학습함으로써 모델이 해당 작업에서 높은 능숙도를 갖게 됩니다.
- 향상된 정확도: 파인튜닝은 모델이 훈련된 작업에 대한 정확도를 크게 향상시키며 명확한 지침과 예시를 통해 학습합니다.
- 문맥 처리 효율: 파인튜닝 후에는 프롬프트 내에서 여러 예시를 요구하지 않아도 되므로, 문맥 창에서 다른 관련 정보를 위한 공간을 절약할 수 있습니다.

<div class="content-ad"></div>

# 3. 지시 데이터 세트 준비

지시 미세 조정 작업의 한 가지 어려움은 많은 공개 데이터 세트가 내용은 풍부하지만 지시 프롬프트로 사용하기에 적합하게 구조화되어 있지 않다는 것입니다. 예를 들어, 언어 모델 사전 훈련에 사용되는 데이터 세트는 특정 지시나 프롬프트 없이 원시 텍스트 단락으로 구성될 수 있습니다.

이러한 어려움을 해결하기 위해 연구원들과 개발자들은 지시 프롬프트 데이터 세트로 변환하기 위해 기존 데이터 세트를 변환하는 미리 정의된 템플릿을 포함하는 라이브러리와 도구를 선별해 왔습니다. 예를 들어, 지시 프롬프트 라이브러리 및 예시를 포함한 Template Libraries, 예를 들면:

- Hugging Face의 NLP Datasets: Hugging Face는 자연어 처리 (NLP) 데이터 세트의 방대한 컬렉션을 제공하며, 이 중 많은 데이터 세트에 미리 정의된 프롬프트 템플릿이 함께 제공됩니다. 이 템플릿을 사용하면 사용자가 원시 데이터 세트를 지시 기반 프롬프트 형식으로 변환할 수 있습니다.
- OpenAI의 GPT Prompt Engineering: OpenAI는 지시 엔지니어링을 위한 자원과 도구를 제공하며, 특정 작업에 맞춘 프롬프트 라이브러리를 포함합니다. 이러한 라이브러리는 분류, 텍스트 생성 및 요약과 같은 작업을 위한 사용 준비가 완료된 템플릿을 제공합니다.

<div class="content-ad"></div>

이 라이브러리와 도구를 사용하면 지시용 데이터 세트를 만들 수 있습니다:

- Amazon 제품 리뷰 데이터 세트: 개발자는 Amazon 제품 리뷰 데이터 세트를 활용하여 언어 모델을 감정 분석이나 제품 분류를 위해 세밀하게 조정할 수 있습니다. "이 리뷰의 감정을 분류하십시오" 또는 "제품 평가를 예측하십시오"와 같은 프롬프트 템플릿을 적용하여, 개발자는 원시 리뷰를 세부 조정을 위한 지시 프롬프트로 변환할 수 있습니다.
- Stanford Sentiment Treebank (SST): SST는 감정(긍정적 또는 부정적)으로 분류된 영화 리뷰를 포함하는 데이터셋입니다. 적절한 프롬프트 템플릿을 사용하면 연구자들은 SST를 감정 분석 세밀 조정 작업용 지시 프롬프트 데이터 세트로 변환할 수 있습니다.
- CNN/Daily Mail 데이터 세트: 이 데이터 세트는 뉴스 기사와 글머리 기사 요약이 짝지어진 것입니다. "이 기사에 대한 요약 생성"과 같은 프롬프트 템플릿을 활용하여 개발자는 텍스트 요약 세밀 조정용 지시 데이터 세트를 준비할 수 있습니다.
- WMT 번역 작업 데이터 세트: WMT(기계 번역 워크샵)은 기계 번역 모델을 훈련하기 위한 데이터 세트를 제공합니다. "이 문장을 프랑스어로 번역하십시오"와 같은 프롬프트 템플릿을 사용하여 연구자는 번역 세밀 조정 작업용 지시 프롬프트를 생성할 수 있습니다.

# 4. 지시 세밀 조정 프로세스

지시 데이터 세트를 준비했다면, 이를 훈련, 검증 및 테스트 세트로 나눕니다. 세밀 조정 중에는 훈련 데이터 세트에서 프롬프트를 선택하고 LLM에 전달하여 완성본을 생성합니다.

<div class="content-ad"></div>

LLM 완성 결과를 교육 데이터에 지정된 응답과 비교하여 표준 교차 엔트로피 함수를 사용하여 손실을 계산하고 역전파를 통해 모델 가중치를 업데이트하십시오.

모델의 성능을 향상시키기 위해 여러 배치의 프롬프트-완성 쌍을 여러 번의 epoch 동안 반복합니다.

# 5. 평가 및 성능 지표

표준 지도 학습과 마찬가지로, 보유 검증 데이터 세트를 사용하여 LLM 성능을 측정하는 별도의 평가 단계를 정의하여 검증 정확도를 얻습니다.

<div class="content-ad"></div>

미세 조정을 완료한 후, 테스트 정확도를 얻기 위해 홀드아웃 테스트 데이터셋을 사용하여 최종 성능 평가를 수행하십시오. 이때, 이메일 보완보상평가(BLEU) 및 ROUGE(Recall-Oriented Understudy for Gisting Evaluation)은 긴 통역모델 (LLM) 지침 미세 조정을 평가하는 데 사용되는 인기있는 두 평가 지표 중 하나입니다.

- BLEU (이중 언어 평가 보조) 스코어:

- 정의: 한 언어에서 다른 언어로 기계 번역된 텍스트의 품질을 평가하기 위한 지표로, 이를 인간이 만든 번역과 비교합니다.
- 예시: 번역 작업에서 모델이 "The weather is nice today"을 정확하게 "Le temps est agréable aujourd’hui"로 번역했을 때, 인간 번역과 비교하여 BLEU 스코어가 높게 나타납니다.

2. ROUGE (Recall-Oriented Understudy for Gisting Evaluation) 스코어:

<div class="content-ad"></div>

- 정의: 자동 요약 및 기계 번역을 평가하는 메트릭스 세트입니다. 이는 모델 출력물과 참조 텍스트 간의 n-gram의 중첩을 측정합니다.
- 예시: 요약 작업의 경우, 높은 ROUGE 점수는 모델이 생성한 요약과 인간이 작성한 요약 간에 높은 중첩이 있음을 나타냅니다.

세밀 조정 과정은 기반 모델의 새 버전을 만들어내며 이를 보통 가르침 모델이라고 합니다. 이는 당신이 관심 있는 작업에 더 적합한 모델입니다.

지시 프롬프트로 세밀 조정하는 것이 오늘날 LLM을 세밀 조정하는 가장 흔한 방법입니다. 본 문서에서는 이 중요한 주제에 대해 간략히 소개되었으니 이제 손을 더럽히고 LLM을 조금 만지작거리며 조정해보는 것이 시간입니다.

## 만약 이 문서를 좋아하셨고 저를 지원하고 싶으시다면, 확인해주십시오:

<div class="content-ad"></div>

- 👏 이 이야기에 박수를 보내주세요 (50번 클랩!) 이 기사가 주목받을 수 있도록 도와주세요
- To Data & Beyond 뉴스레터를 구독해주세요
- 제 Medium 계정을 팔로우해주세요
- 📰 제 Medium 프로필에서 더 많은 콘텐츠를 확인해주세요
- 🔔 팔로우하기: LinkedIn | Youtube | GitHub | Twitter

## 제 뉴스레터 'To Data & Beyond'를 구독하여 제 글을 완전히 그리고 일찍 볼 수 있습니다:

## 데이터 과학과 AI 분야에서 커리어를 시작하고 방향을 모를 때 도움이 필요하신가요? 저는 데이터 과학 멘토링 세션과 장기적 커리어 멘토링을 제공합니다:

- 멘토링 세션: [링크](https://lnkd.in/dXeg3KPW)
- 장기적 멘토링: [링크](https://lnkd.in/dtdUYBrM)

<div class="content-ad"></div>

![Image](/assets/img/2024-06-19-AComprehensiveIntroductiontoInstructionFine-TuningforLLMs_1.png)
