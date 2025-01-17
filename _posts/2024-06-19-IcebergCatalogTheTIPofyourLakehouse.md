---
title: "아이스버그 카탈로그 당신의 레이크하우스의 TIP"
description: ""
coverImage: "/assets/img/2024-06-19-IcebergCatalogTheTIPofyourLakehouse_0.png"
date: 2024-06-19 01:36
ogImage:
  url: /assets/img/2024-06-19-IcebergCatalogTheTIPofyourLakehouse_0.png
tag: Tech
originalTitle: "Iceberg Catalog: The TIP of your Lakehouse"
link: "https://medium.com/@christian_24956/iceberg-catalog-the-tip-of-your-lakehouse-8bea6284f785"
isUpdated: true
---

아이스버그 카탈로그 랜드스케이프는 Snowflake와 Databricks로부터 중요한 발표가 속출하며 급속하게 변화하고 있어요. 이 다채로운 생태계에 TIP를 소개합니다. HANSETAG가 선보이는 이 Rust-native Iceberg REST 카탈로그는 데이터 품질, 거버넌스, 그리고 유연성을 우선시합니다. 변경 이벤트, 계약 유효성 검사, 멀티 테넌시와 함께 경량화되고 맞춤형 솔루션으로 혁신을 추구해요.

![이미지](/assets/img/2024-06-19-IcebergCatalogTheTIPofyourLakehouse_0.png)

이제 몇 날 뒤 데이터 랜드스케이프에서는 지표적인 변화가 일어나고 있어요. 특히, Snowflake는 공개 소스 아이스버그 REST 카탈로그인 Polaris를 발표했고, Databricks는 Apache Iceberg를 만든 파이오니어 회사 Tabular.io를 인수했어요. 더불어 Databricks는 아이스버그 REST(읽기) 지원을 하는 Unity Catalog도 오픈소스로 공개했죠. 이제 요즘에는 데이터 회사로 진정으로 인정받으려면 아이스버그 카탈로그의 구현을 오픈소스화해야 하는 것 같아요.

이미 화요일이 다가왔고, 의심스러운 침묵이 느껴집니다. 이번 주에 새로운 카탈로그가 나오지 않았어요. 하지만 걱정하지 마세요! 저희가 TIP를 소개해 드릴게요. 이는 Rust-native, 멀티 테넌트, 싱글 바이너리로 Iceberg REST 카탈로그를 구현한 것이에요. 하지만 주의해 주세요, 우리는 약간 다르게(알려진 대로 😉) 그리고 기존 카탈로그와 다른 방식으로 일을 진행하고 있어요. 이에 대해 더 자세히 설명하겠어요. 함께 시작해 볼까요?

<div class="content-ad"></div>

# 우리는 누구인가

HANSETAG에서는 회사들이 데이터 자산을 구축, 공유 및 활용할 수 있는 첨단 데이터 제품 플랫폼을 구축합니다. 저희 플랫폼은 데이터 계약서에 기록된 강제 SLO를 통해 지속적으로 높은 데이터 품질을 보장합니다. 플랫폼을 구동하기 위해 신뢰할 수 있는 멀티 테넌트 Iceberg 카탈로그가 필요합니다. 기존 구현이 우리의 요구를 충족하지 못했기 때문에 Apache 라이센스 하에 자체 카탈로그를 구축했습니다. 기여해 주시기 바랍니다! 😊

# 데이터 레이크하우스

데이터 레이크하우스는 데이터 및 분석 프로젝트의 기본 아키텍처가 되었으며 데이터 메쉬 구현을 위한 기반을 제공합니다. 데이터 레이크의 유연성과 데이터 웨어하우스의 구조와 편의성을 결합합니다. 모든 레이크하우스가 동일하지 않다는 점을 인식하는 것이 중요합니다. 레이크하우스에는 Apache Iceberg, Delta Lake 및 Apache Hudi와 같은 세 가지 테이블 포맷이 등장했습니다. Iceberg의 신속한 개발과 뛰어난 벤더 독립적인 커뮤니티로 인해 HANSETAG에서는 초기 레이크하우스 형식으로 Iceberg를 선택했습니다.

<div class="content-ad"></div>

# 아이스버그 및 REST 카탈로그

아파치 아이스버그 카탈로그는 데이터 레이크하우스의 핵심으로 대규모 데이터 세트의 효율적인 관리 및 조직을 제공합니다. 이는 네임스페이스, 테이블 및 뷰의 중앙 저장소 역할을 하며, 개별 객체에 대한 세밀한 접근을 관리합니다.

아이스버그는 REST 이외의 다른 카탈로그를 지원합니다. 그러나 최근 시장 활동에 의해 강조된 것처럼, 아이스버그 REST 카탈로그가 가장 밝은 미래를 가지고 있습니다. 또한 현재의 아이스버그 카탈로그 중 유일한 것으로, 클라이언트 측에서 저장 자격 증명을 지정하지 않고 데이터에 대한 클라이언트 접근을 허용합니다. 아이스버그 커뮤니티는 REST 명세의 새 버전의 일부로 모든 다른 카탈로그를 REST 카탈로그를 통해 보완할 것을 고려하고 있습니다.

# TIP가 다른 점

<div class="content-ad"></div>

카탈로그를 구축하는 것은 로켓 과학은 아니지만 경솔하게 결정한 것은 아닙니다. 우리 플랫폼에서 데이터 품질과 데이터 거버넌스를 우선시하며 사용자들이 자체 호스팅이든 클라우드에 있든 데이터에 대해 완전한 통제를 할 수 있기를 바랍니다. 결과적으로 기존 표준을 혁신하는 방법으로 카탈로그를 구축했습니다:

- 멀티 테넌트: 하나의 TIP 배포로 여러 프로젝트를 서비스할 수 있습니다. 각 프로젝트는 여러 창고를 포함할 수 있습니다. 창고와 프로젝트는 실행 중에 REST-API를 통해 동적으로 추가되며 각각 다른 저장 위치에 있습니다.
- 변경 이벤트: 외부 시스템이 우리 테이블에 어떤 변경이 가해졌는지 알 수 있어야 합니다. 우리는 각 테이블 변경 시 이벤트(Cloudevents)를 발생시킵니다. 예를 들어 테이블 스키마가 변경될 때 이벤트를 발행합니다.
- 변경 승인 / 계약 검증: 데이터 계약은 HANSETAG에서 하는 주요 작업입니다. 변경 이벤트를 통해 스키마 변경을 알 수 있지만, 데이터 계약에 영향을 미칠 수 있으며 이로 인해 하류 파이프라인이 모두 손상될 수 있습니다. TIP를 사용하면 ContractVerification 트레이트를 사용하여 해당 변경 사항을 금지할 수 있습니다. 데이터 계약의 오픈 소스 구현에 주목하세요!
- Rust로 작성: 단일 작고 통합된 이진 파일. JVM이나 Python 환경이 필요하지 않습니다.
- 사용자 정의 가능: TIP는 확장 가능하도록 설계되었지만 필수 구성요소가 함께 제공됩니다. 향후 통합을 추가하고 여러분이 몇 가지 메서드를 구현하여 자체 통합을 작성할 수 있도록 키 인터페이스를 공개합니다. 이러한 인터페이스는 다음과 같습니다:
  - 백엔드 데이터베이스 (카탈로그): Postgres 외부에 내장
  - 시크릿 저장소: Postgres 내장, Vault 작업 진행 중
  - 이벤트 시스템: NATS 내장
  - 인증: OIDC 내장, Zitadel 작업 진행 중
  - 권한: 곧 OpenFGA 내장 예정
  - 계약 검증: 곧 출시될 데이터 계약 라이브러리 지원
- 저장소 액세스 관리: 클라이언트와 S3 자격 증명을 공유하지 않고 자체 호스팅 및 AWS S3를 지원하는 내장된 S3-Signing을 제공합니다. 또한 판매 자격 정보에 대해 작업 중입니다!
- 외부 잘 정의된 접근 (FGA): TIP는 권한을 내부적으로 저장하지 않으며 결코 저장하지 않습니다. 인증을 구현하기 위해 일부 메서드를 구현하여 다른 시스템과 통합할 수 있습니다.

# 시작하기

```js
git clone https://github.com/hansetag/iceberg-catalog.git
cd iceberg-catalog/examples
docker compose up
```

<div class="content-ad"></div>

GitHub에서 더 많은 자세한 내용을 확인하러 가보세요! 그리고 별표 한 개 꾸욱 눌러주세요!

Github: https://github.com/hansetag/iceberg-catalog
HANSETAG: https://hansetag.com/
