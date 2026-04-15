# 경쟁사 심층 분석 -- Base Pay (Commerce Payments Protocol)

## 분석 개요

- **분석 대상**: Base Pay / Coinbase Commerce Payments Protocol의 경쟁 환경
- **분석 일시**: 2026-04-14
- **분석 관점**: 결제(Payment) - 정산(Settlement) - 환불(Refund) 프로세스 중심
- **주요 참조 소스**:
  - [Solana Payments Documentation](https://solana.com/docs/payments)
  - [Solana Pay x Shopify Refund Process](https://commercedocs.solanapay.com/merchants/refunds)
  - [Gnosis Pay Card Review 2026](https://coingape.com/crypto-cards/gnosis-pay-card-review/)
  - [Gnosis Pay Fees and Limits](https://help.gnosispay.com/hc/en-us/articles/39533569163284-Understanding-Your-Card-s-Fees-and-Limits)
  - [Stripe x402 Documentation](https://docs.stripe.com/payments/machine/x402)
  - [Stripe Stablecoin Payments](https://docs.stripe.com/payments/stablecoin-payments)
  - [x402 Protocol GitHub](https://github.com/coinbase/x402)
  - [BitPay Pricing](https://www.bitpay.com/pricing)
  - [BitPay Settlement Documentation](https://developer.bitpay.com/docs/settlement)
  - [NOWPayments Pricing](https://nowpayments.io/pricing)
  - [CoinGate Pricing](https://coingate.com/pricing)
  - [CoinGate Merchant Refunds](https://coingate.com/merchant-refunds)
  - [PayPal PYUSD Expansion](https://investor.pypl.com/news-and-events/news-details/2026/PAYPAL-BRINGS-PAYPAL-USD-TO-USERS-ACROSS-70-MARKETS/default.aspx)
  - [Lightning Network](https://lightning.network/)
  - [BTCPay Server Review 2026](https://blockfinances.fr/en/btcpay-server-review)
  - [Strike Review 2026](https://www.bitcoin.diy/exchanges/strike-review)
  - [Polygon Open Money Stack](https://www.coindesk.com/business/2026/01/08/polygon-labs-unveils-open-money-stack-to-power-borderless-stablecoin-payments/)
  - [Coinbase Commerce to Coinbase Business Transition](https://help.coinbase.com/en/transitioning-from-coinbase-commerce-to-coinbase-business)

---

## 1. 경쟁 구도 요약

### 1.1 시장 지형

Base Pay(Commerce Payments Protocol)는 **L2 블록체인 네이티브 결제 프로토콜**이라는 고유한 포지셔닝을 가지고 있다. 경쟁 구도는 크게 세 가지 층위로 나뉜다.

| 구분 | 설명 | 경쟁사 수 |
|------|------|-----------|
| **직접 경쟁사** | L2/블록체인 네이티브 결제 프로토콜 | 5개 |
| **간접 경쟁사** | 암호화폐 결제 게이트웨이 및 전통 결제사의 크립토 서비스 | 5개 |
| **잠재 대체재** | BTCPay Server, 자체 스마트 컨트랙트 결제, DEX 직접 결제 | 다수 |

### 1.2 경쟁 구도 핵심 포인트

- **시장 지배자**: 간접 경쟁 영역에서 Stripe(전통 결제 인프라 + 크립토 확장)와 PayPal(PYUSD + 650M 사용자)이 거래 규모 기준 지배적
- **직접 경쟁 선두**: Solana Pay가 블록체인 네이티브 결제 영역에서 가장 강력한 대항마 (Mastercard, Western Union, Worldpay 파트너십)
- **신흥 도전자**: Polygon의 Open Money Stack ($250M 투자), Stripe x402 (AI 에이전트 결제 신시장)
- **차별화된 니치**: Gnosis Pay (Visa 네트워크 연결 온체인 카드), Lightning Network (BTC 전용 마이크로페이먼트)

---

## 2. 경쟁사 분류

### 2.1 직접 경쟁사 (동일 가치 제안: L2/블록체인 네이티브 결제)

| 경쟁사명 | 블록체인 | 핵심 포지셔닝 | 설립/출시 |
|----------|----------|---------------|-----------|
| **Solana Pay** | Solana | 초고속 결제, 기관급 파트너십 (Visa, Mastercard) | 2022 |
| **Polygon Pay (Open Money Stack)** | Polygon PoS / zkEVM | 스테이블코인 특화 결제 인프라 | 2026 (리브랜딩) |
| **Gnosis Pay** | Gnosis Chain | Visa 네트워크 연결 온체인 지출 카드 | 2023 |
| **Lightning Network** | Bitcoin L2 | BTC 마이크로페이먼트, 오프체인 채널 기반 | 2018 |
| **Stripe x402** | Base, Solana | AI 에이전트 결제 프로토콜 (HTTP 402 기반) | 2026.02 |

### 2.2 간접 경쟁사 (유사 가치 제공: 암호화폐 결제 수용)

| 경쟁사명 | 유형 | 핵심 포지셔닝 | 설립 |
|----------|------|---------------|------|
| **BitPay** | 결제 게이트웨이 (수탁형) | 법정화폐 직접 정산, 38개국 은행 연결 | 2011 |
| **CoinGate** | 결제 게이트웨이 (수탁형) | EU 규제 준수, 70+ 암호화폐 지원 | 2014 |
| **NOWPayments** | 결제 게이트웨이 (준비수탁형) | 350+ 토큰 지원, 최저 수수료 | 2019 |
| **PayPal Crypto (PYUSD)** | 전통 결제사 크립토 확장 | 650M 사용자 기반, 70개 시장 PYUSD | 2023 |
| **Stripe Stablecoin** | 전통 결제사 크립토 확장 | 1.5% 수수료, Shopify 수백만 가맹점 | 2025 |

---

## 3. 직접 경쟁사 심층 분석

### 3.1 Solana Pay

#### 프로파일

| 항목 | 내용 |
|------|------|
| **운영 주체** | Solana Foundation / Solana Labs |
| **출시** | 2022년 |
| **블록체인** | Solana (L1, ~400ms 블록 타임) |
| **투자 현황** | Solana 생태계 전체 기준 수십억 달러 |
| **핵심 파트너** | Visa, Mastercard, Western Union, Worldpay, Shopify |
| **타깃 고객** | e-commerce 머천트, POS 소매점, 기관 결제 |

#### 결제-정산-환불 프로세스

**결제 흐름:**
1. 머천트가 결제 요청 생성 (QR 코드 또는 API)
2. 구매자가 Solana 지갑으로 결제 (SOL, USDC, 기타 SPL 토큰)
3. 트랜잭션이 ~400ms 내 확정
4. 머천트 지갑에 직접 정산

**정산:**
- 즉시 정산 (온체인 확정 즉시)
- 정산 통화: USDC, SOL, 기타 SPL 토큰
- 법정화폐 전환: 직접 미지원, 서드파티(Coinbase, Strike 등) 경유 필요
- 2026년 Worldpay와 협력하여 머천트 법정화폐 정산 추진 중

**환불:**
- Shopify 통합 시 관리자 패널에서 환불 개시
- 부분 환불 지원
- 환불 지갑은 수신 지갑과 달라도 가능
- 가스비는 현재 Solana Pay가 부담 (향후 변경 가능)
- 수 초 내 환불 완료

**수수료:**
- 플랫폼 수수료: 없음 (프로토콜 자체는 무료)
- 네트워크 가스비: ~$0.00025/건
- 중간 처리자 사용 시 별도 수수료 가능

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **Strengths** | 극저 가스비($0.00025), 무료 프로토콜, 기관급 파트너십(Visa/Mastercard/Worldpay), 높은 TPS(~4,000), Shopify 네이티브 통합 |
| **Weaknesses** | 에스크로/Auth-Capture 모델 미지원, 법정화폐 직접 정산 미지원, Solana 네트워크 과거 다운타임 이력, EVM 비호환 |
| **Opportunities** | 기관 개발자 플랫폼 출시(2026), Mastercard/Western Union 파트너십 확대, x402 프로토콜 Solana 지원 추가 |
| **Threats** | Base 네트워크의 빠른 성장, Stripe의 다중 체인 지원으로 플랫폼 종속도 감소, 네트워크 안정성 우려 잔존 |

---

### 3.2 Stripe x402 프로토콜

#### 프로파일

| 항목 | 내용 |
|------|------|
| **운영 주체** | x402 Foundation (Coinbase 주도 오픈소스), Stripe이 주요 구현체 |
| **출시** | 2026년 2월 (Preview) |
| **지원 네트워크** | Base, Solana (추가 확장 예정) |
| **핵심 파트너** | Coinbase, Stripe, Cloudflare |
| **타깃 고객** | AI 에이전트, API 제공자, 마이크로서비스, IoT |

#### 결제-정산-환불 프로세스

**결제 흐름:**
1. 클라이언트가 유료 리소스에 HTTP 요청
2. 서버가 HTTP 402 Payment Required 응답 + 결제 요건 반환
3. 클라이언트가 USDC로 결제 서명 생성
4. 서버가 결제 검증 (로컬 또는 Facilitator 경유)
5. 결제 확인 후 리소스 제공

**정산:**
- 즉시 정산 (온체인 USDC 전송)
- 정산 통화: USDC
- 수수료 없음 (Stripe facilitator 기준, 네트워크 가스비만 발생)
- 마이크로페이먼트 가능 ($0.001 수준)

**환불:**
- 프로토콜 수준의 환불 메커니즘 미정의 (요청-응답 모델 특성상 환불 개념 제한적)
- "exact" 스킴: 고정 금액 결제, 별도 환불 프로세스 필요
- "upto" 스킴: 사용량 기반 과금, 미사용분은 과금되지 않아 환불 불필요

**수수료:**
- Stripe x402 facilitator: 수수료 없음 (네트워크 가스비만 발생)
- 기존 Stripe 결제(2.9% + $0.30) 대비 파격적 가격
- Base 네트워크 가스비: ~$0.01

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **Strengths** | HTTP 표준 기반(기존 웹 인프라 호환), 수수료 없음, 마이크로페이먼트 최적화, Stripe + Coinbase 생태계 시너지, 오픈소스 |
| **Weaknesses** | Preview 단계(미성숙), 인간 대면 결제에 부적합, USDC 단일 통화, 환불 메커니즘 미비, API 버전 제한(2026-03-04) |
| **Opportunities** | AI 에이전트 경제 폭발적 성장, API 경제 과금 패러다임 전환, 다중 네트워크 확장 |
| **Threats** | 기존 API 과금 모델(구독/API 키)과의 경쟁, 규제 불확실성, 다른 결제 프로토콜의 유사 기능 구현 |

#### x402와 Base Pay의 관계

x402는 Base Pay의 **경쟁자이자 보완재**라는 이중적 관계를 가진다.

- **보완재 측면**: x402는 Coinbase가 주도한 오픈소스 프로토콜이며, Base 네트워크를 주요 정산 레이어로 사용한다. x402의 성장은 Base 네트워크 거래량 증가로 이어지며, Commerce Payments Protocol과 동일한 USDC on Base 정산 인프라를 공유한다.
- **경쟁 측면**: x402는 머신-투-머신 결제에 특화되어 Commerce Payments Protocol(인간 대면 e-commerce)과 타깃 시장이 다르다. 다만, API 과금이나 디지털 콘텐츠 결제 영역에서는 Base Pay의 잠재 시장과 일부 겹칠 수 있다.
- **전략적 평가**: Coinbase는 x402를 Commerce Payments Protocol의 경쟁자가 아닌, Base 네트워크 결제 생태계의 **또 다른 결제 레이어**로 포지셔닝하고 있다. x402(머신 결제) + Commerce Payments Protocol(인간 결제)이 Base 위에서 공존하는 구조다.

---

### 3.3 Lightning Network (BTC 결제)

#### 프로파일

| 항목 | 내용 |
|------|------|
| **운영 주체** | 분산형 (Lightning Labs, ACINQ, Blockstream 등) |
| **출시** | 2018년 (메인넷) |
| **기반** | Bitcoin L2 (오프체인 결제 채널) |
| **규모** | 18,000+ 노드, 5,400+ BTC 용량, 월 1,200만+ 건 |
| **핵심 결제 처리자** | Strike, BTCPay Server, Lightspark |
| **타깃 고객** | BTC 커뮤니티, 신흥국 송금, POS 소매점 |

#### 결제-정산-환불 프로세스

**결제 흐름:**
1. 머천트가 Lightning 인보이스 생성 (BOLT11 형식)
2. 구매자 지갑이 경로 탐색 후 HTLC를 통해 결제
3. 중간 노드를 경유한 원자적 다중홉 결제
4. 수 초 내 결제 확정

**정산:**
- 즉시 정산 (채널 내 잔고 업데이트)
- 정산 통화: BTC (Strike 경유 시 법정화폐 즉시 전환 가능)
- Strike: 85개국에서 BTC -> 현지 법정화폐 즉시 전환
- BTCPay Server: 자체 호스팅, 수수료 0%

**환불:**
- 프로토콜 수준 환불 메커니즘 없음
- 결제 실패 시 자동 반환 (HTLC 타임아웃)
- 성공한 결제의 환불: 별도 역방향 결제로 처리 (수동)
- BTCPay Server: 수동 환불만 가능
- Strike: 앱 내 환불 기능 제공

**수수료:**
- 네트워크 라우팅 수수료: < $0.01 (보통 $0.001 미만)
- BTCPay Server: 플랫폼 수수료 0% (자체 호스팅 비용만)
- Strike: 0.3~1%
- 채널 개설/종료 시 온체인 수수료 발생

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **Strengths** | BTC 생태계 독점적 접근, 극저 수수료, 완전 분산형, Square 통한 400만 가맹점 접근(2026), 가장 긴 운영 이력 |
| **Weaknesses** | BTC 단일 자산, 채널 유동성 관리 필요, 노드 운영 복잡, 환불 메커니즘 부재, 스테이블코인 네이티브 미지원 |
| **Opportunities** | Square/Block 통한 대규모 가맹점 확장, Taproot Assets로 스테이블코인 지원 추진, 신흥국 송금 수요 |
| **Threats** | 스테이블코인 결제의 부상(USDC/PYUSD), L2 결제 프로토콜의 기능 우위, BTC 가격 변동성에 따른 결제 의욕 변동 |

---

## 4. 간접 경쟁사 분석

### 4.1 BitPay

| 항목 | 내용 |
|------|------|
| **설립** | 2011년 (가장 오래된 크립토 결제 서비스) |
| **수수료** | 1% + $0.25/건 |
| **지원 토큰** | 16+ (BTC, ETH, USDC, DOGE 등) |
| **정산** | 법정화폐 직접 은행 정산 (8개 통화, 38개국), T+2 |
| **환불** | 원래 암호화폐로 환불, 채굴 수수료 머천트 부담, 30일 제한 |
| **커스터디** | 수탁형 |
| **통합** | Shopify, WooCommerce, WHMCS 등 |
| **핵심 강점** | 법정화폐 직접 정산, 긴 운영 이력, 규제 준수 |
| **핵심 약점** | 높은 건당 고정 수수료($0.25), L2 지원 제한적, 에스크로 미지원 |

### 4.2 NOWPayments

| 항목 | 내용 |
|------|------|
| **설립** | 2019년 |
| **수수료** | 0.5% (+0.5% 환전 수수료) |
| **지원 토큰** | 350+ (업계 최다) |
| **정산** | 암호화폐 직접 정산, 법정화폐 정산(75+ 통화, 서드파티 경유) |
| **환불** | 제한적 (자동 환불 미지원) |
| **커스터디** | 준비수탁형 (임시 주소 경유) |
| **통합** | Shopify, WooCommerce, PrestaShop, API |
| **핵심 강점** | 최저 수수료, 최다 토큰 지원, 볼륨 할인 |
| **핵심 약점** | 에스크로 미지원, 환불 기능 제한, 실제 비수탁 아님 |

### 4.3 CoinGate

| 항목 | 내용 |
|------|------|
| **설립** | 2014년 (리투아니아) |
| **수수료** | 1% (결제), 0.25 EUR + 0.1% (환불) |
| **지원 토큰** | 70+ |
| **정산** | 암호화폐 또는 EUR 은행 정산 |
| **환불** | 전액/부분 환불 지원, 다른 암호화폐로 환불 가능 |
| **커스터디** | 수탁형 |
| **통합** | Shopify, WooCommerce, Magento, WHMCS, API |
| **핵심 강점** | EU 규제 준수(리투아니아 라이선스), 명확한 환불 정책, x402 pay-per-request 구현(CoinGecko) |
| **핵심 약점** | 유럽 중심, L2 지원 제한적, 에스크로 미지원 |

### 4.4 PayPal Crypto (PYUSD)

| 항목 | 내용 |
|------|------|
| **출시** | 2023년 (PYUSD), 2025년 (머천트 결제 확장) |
| **수수료** | 0.99% (2026.07.31까지 프로모션), 이후 미정 |
| **지원 토큰** | 100+ (구매자측), 정산은 PYUSD/USD |
| **정산** | 법정화폐(USD) 직접 정산, PYUSD로 보유 시 4% 이자 |
| **환불** | PayPal 표준 환불 프로세스 적용 (구매자 보호 포함) |
| **커스터디** | 수탁형 |
| **통합** | PayPal 기존 가맹점 전체, Checkout 버튼 |
| **핵심 강점** | 650M 사용자 기반, 70개 시장 PYUSD, 구매자 보호, 법정화폐 즉시 정산 |
| **핵심 약점** | 높은 중앙화, 블록체인 네이티브 아님, PYUSD 채택 아직 초기, 수수료 인상 가능성 |

### 4.5 Stripe Stablecoin Payments

| 항목 | 내용 |
|------|------|
| **출시** | 2025년 (스테이블코인 결제) |
| **수수료** | 1.5% (가스비 Stripe 부담) |
| **지원 스테이블코인** | USDC, USDP, USDG (9+ 네트워크) |
| **정산** | USD 직접 은행 정산 (미국 비즈니스 한정) |
| **환불** | Stripe 표준 환불 프로세스 적용 |
| **커스터디** | 수탁형 |
| **통합** | Stripe API, Shopify (수백만 가맹점), Payment Links |
| **핵심 강점** | 가장 광범위한 네트워크 지원(9+), 기존 Stripe 인프라 활용, 가스비 흡수, Shopify 수백만 가맹점 즉시 접근 |
| **핵심 약점** | 미국 비즈니스만 수용 가능, 1.5% 수수료(온체인 직접 비용 대비 고가), 스테이블코인 한정 |

---

## 5. 핵심 비교: 결제-정산-환불 프로세스

### 5.1 수수료 구조 비교

| 경쟁사 | 플랫폼 수수료 | 네트워크 가스비 | 환전 수수료 | 환불 수수료 | 월/설치 수수료 |
|--------|-------------|----------------|------------|------------|---------------|
| **Base Pay** | 1% | ~$0.01 (Base) | DEX 슬리피지 | 가스비 별도 | 없음 |
| **Solana Pay** | 0% | ~$0.00025 | N/A (직접 토큰) | 가스비 (현재 SP 부담) | 없음 |
| **Stripe x402** | 0% | ~$0.01 (Base) | N/A | 미정의 | 없음 |
| **Gnosis Pay** | 1.5% (안정화) | Gnosis Chain 가스 | FX 수수료 별도 | N/A (Visa 환불) | 없음 |
| **Lightning** | 0% (BTCPay) / 0.3-1% (Strike) | < $0.001 라우팅 | N/A | 수동 역결제 | 없음 (BTCPay 자체호스팅) |
| **BitPay** | 1% + $0.25 | 포함 | 포함 | 채굴 수수료 차감 | 없음 |
| **NOWPayments** | 0.5% | 포함 | +0.5% | 제한적 | 없음 |
| **CoinGate** | 1% | 포함 | 1% (수동 변환) | 0.25 EUR + 0.1% | 없음 |
| **PayPal Crypto** | 0.99%* | N/A | 포함 | PayPal 표준 | 없음 |
| **Stripe Stablecoin** | 1.5% | Stripe 부담 | N/A | Stripe 표준 | 없음 |

*PayPal 0.99%는 2026.07.31까지 프로모션 요율

### 5.2 정산 방식 비교

| 경쟁사 | 정산 속도 | 정산 통화 | 법정화폐 직접 정산 | 정산 주기 |
|--------|----------|----------|------------------|----------|
| **Base Pay** | ~200ms (온체인) | USDC, ETH, 기타 토큰 | 간접 (Coinbase 경유) | 실시간 |
| **Solana Pay** | ~400ms (온체인) | USDC, SOL, SPL 토큰 | 간접 (서드파티 경유, Worldpay 추진 중) | 실시간 |
| **Stripe x402** | ~2초 (Base) | USDC | 간접 | 실시간 |
| **Gnosis Pay** | 즉시 (Visa 네트워크) | EURe, GBPe, USDCe | 간접 (Visa 가맹점 수용) | 카드 결제 표준 |
| **Lightning** | 즉시 (~1초) | BTC (Strike 경유 시 법정화폐) | 가능 (Strike: 85개국 법정화폐) | 실시간 |
| **BitPay** | T+2 (은행 정산) | USD, EUR 등 8개 법정화폐 | 직접 (38개국) | T+2 영업일 |
| **NOWPayments** | 즉시 (크립토) | 350+ 크립토, 75+ 법정화폐 | 가능 (서드파티 경유) | 실시간 (크립토) |
| **CoinGate** | 즉시 (크립토) / T+1 (EUR) | 크립토 또는 EUR | 가능 (EUR 은행 정산) | 실시간~T+1 |
| **PayPal Crypto** | 즉시 | USD, PYUSD | 직접 (PayPal 잔고) | 실시간 |
| **Stripe Stablecoin** | T+2 (은행 정산) | USD | 직접 (미국 비즈니스) | T+2 영업일 |

### 5.3 환불/분쟁 해결 비교

| 경쟁사 | 자동 환불 | 부분 환불 | 에스크로 | 차지백 보호 | 분쟁 중재 |
|--------|----------|----------|---------|------------|----------|
| **Base Pay** | 지원 (온체인) | 지원 | **지원 (Auth-Capture)** | 차지백 없음 (머천트 유리) | 오퍼레이터 중재 가능 |
| **Solana Pay** | 지원 (Shopify 연동) | 지원 | 미지원 | 차지백 없음 | 플랫폼 의존 |
| **Stripe x402** | 미정의 | 미정의 | 미지원 | 해당 없음 | 해당 없음 |
| **Gnosis Pay** | Visa 표준 | Visa 표준 | 미지원 | Visa 차지백 적용 | Visa 분쟁 절차 |
| **Lightning** | 실패 시 자동 반환 | 불가 | 미지원 | 차지백 없음 | 없음 |
| **BitPay** | 지원 | 지원 | 미지원 | 차지백 없음 | BitPay 중재 |
| **NOWPayments** | 제한적 | 제한적 | 미지원 | 차지백 없음 | 제한적 |
| **CoinGate** | 지원 | 지원 | 미지원 | 차지백 없음 | CoinGate 중재 |
| **PayPal Crypto** | **지원** | **지원** | **지원** | **구매자 보호 적용** | **PayPal 분쟁 센터** |
| **Stripe Stablecoin** | **지원** | **지원** | **지원** | **Stripe Radar** | **Stripe 분쟁 관리** |

### 5.4 가맹점 통합 난이도 비교

| 경쟁사 | 통합 복잡도 | Shopify | WooCommerce | 커스텀 API | SDK |
|--------|-----------|---------|-------------|-----------|-----|
| **Base Pay** | 중간 | 네이티브 플러그인 | 미확인 | Solidity + REST API | JS |
| **Solana Pay** | 중간 | 네이티브 플러그인 | 서드파티 | REST API | JS/TS |
| **Stripe x402** | 낮음 (1줄 코드) | 미지원 (API 전용) | 미지원 | HTTP 헤더 기반 | JS/Python/Rust |
| **Gnosis Pay** | N/A | N/A (카드 결제) | N/A | N/A | N/A |
| **Lightning** | 높음 (BTCPay) / 낮음 (Strike) | 플러그인 지원 | 플러그인 지원 | REST API | 다수 |
| **BitPay** | 낮음 | 플러그인 지원 | 플러그인 지원 | REST API | 다수 |
| **NOWPayments** | 낮음 | 플러그인 지원 | 플러그인 지원 | REST API | JS/Python |
| **CoinGate** | 낮음 | 플러그인 지원 | 플러그인 지원 | REST API | PHP/Python |
| **PayPal Crypto** | 매우 낮음 | 기본 내장 | 플러그인 지원 | REST API | 다수 |
| **Stripe Stablecoin** | 매우 낮음 | 기본 내장 | 플러그인 지원 | Stripe API | 다수 |

---

## 6. 경쟁사 포지셔닝 맵

### 6.1 축 정의

- **X축: 결제 프로그래머빌리티 (Programmability)** -- 단순 전송(좌) vs 프로그래머블 결제 흐름(우)
- **Y축: 법정화폐 통합도 (Fiat Integration)** -- 크립토 네이티브(하) vs 법정화폐 완전 통합(상)

### 6.2 포지셔닝 맵 (텍스트 표현)

```
  법정화폐 완전 통합 (상)
  ^
  |
  |  [PayPal Crypto]          [Stripe Stablecoin]
  |       (.99%, 650M 사용자)      (1.5%, Shopify 수백만)
  |
  |  [BitPay]                  [Gnosis Pay]
  |    (1%+$0.25, 38개국)          (1.5%, Visa 80M 가맹점)
  |
  |  [CoinGate]
  |    (1%, EU 은행)
  |
  |  [NOWPayments]             [Strike/Lightning]
  |    (0.5%, 350+ 토큰)           (0.3-1%, 85개국)
  |
  |  [Solana Pay]              [Base Pay]
  |    (0%, ~400ms)               (1%, Auth-Capture, ~200ms)
  |                                    |
  |                            [Stripe x402]
  |                              (0%, HTTP 402, 마이크로페이먼트)
  |
  +------------------------------------------------------------->
  단순 전송 (좌)              프로그래머블 결제 흐름 (우)
```

### 6.3 포지셔닝 맵 해석

1. **우하단 (프로그래머블 + 크립토 네이티브)**: Base Pay와 Stripe x402가 위치한다. 이 영역은 온체인 결제의 기술적 우위가 가장 두드러지는 곳으로, 에스크로, 조건부 결제, 마이크로페이먼트 등 전통 결제사가 제공하기 어려운 기능이 집중된다.

2. **좌하단 (단순 전송 + 크립토 네이티브)**: Solana Pay, NOWPayments가 위치한다. 저비용 단순 전송에 특화되어 있으나, 프로그래머블 결제 흐름은 제한적이다.

3. **좌상단 (단순 전송 + 법정화폐 통합)**: PayPal Crypto, BitPay가 위치한다. 법정화폐 직접 정산이라는 강력한 이점이 있으나, 온체인 기능은 제한적이다.

4. **우상단 (프로그래머블 + 법정화폐 통합)**: Stripe Stablecoin이 위치한다. 프로그래머블 결제와 법정화폐 통합을 모두 갖추고 있어, Base Pay에 대한 가장 강력한 경쟁 위협이다.

---

## 7. 차별화 기회 및 경쟁 공백 분석

### 7.1 Base Pay의 고유한 경쟁 우위

| 차별화 요소 | Base Pay | 가장 가까운 경쟁사 | 격차 평가 |
|------------|----------|------------------|----------|
| **에스크로/Auth-Capture 온체인** | 유일하게 스마트 컨트랙트 기반 구현 | Stripe Stablecoin (오프체인), PayPal (중앙화) | 높음 -- 온체인 수준의 구현은 Base Pay만 보유 |
| **오픈소스 프로토콜** | 전체 프로토콜 공개 | BTCPay Server (게이트웨이만), x402 (결제 프로토콜) | 중간 -- BTCPay와 x402도 오픈소스 |
| **Uniswap V3 통합 (다중 토큰)** | 모든 유동성 토큰 자동 스왑 | NOWPayments (350+ 수동), Solana Pay (SPL 토큰) | 높음 -- DEX 기반 자동 스왑은 Base Pay 고유 |
| **Coinbase 생태계** | 6,000만+ 인증 사용자 직접 접근 | PayPal (650M, 간접) | 중간 -- PayPal이 규모는 더 크나 크립토 네이티브 아님 |

### 7.2 경쟁 공백 (White Space)

**공백 1: 법정화폐 직접 정산 + 온체인 프로그래머빌리티**

현재 법정화폐 직접 정산과 온체인 프로그래머블 결제를 동시에 제공하는 솔루션이 없다. Base Pay가 Coinbase Business 플랫폼을 통해 법정화폐 정산 기능을 강화하면 이 공백을 메울 수 있다. Stripe Stablecoin이 가장 가까운 위치에 있으나, Stripe의 프로그래머빌리티는 오프체인이다.

**공백 2: 크로스체인 결제 프로토콜**

대부분의 결제 솔루션이 단일 체인 또는 제한된 체인을 지원한다. 현재 Commerce Payments Protocol은 Base, Ethereum, Polygon에 배포되어 있으나, Solana 등 비 EVM 체인으로의 확장 여지가 있다. Stripe Stablecoin이 9+ 네트워크를 지원하지만 이는 중앙화된 게이트웨이 방식이다.

**공백 3: 구매자 보호 메커니즘**

온체인 결제의 가장 큰 약점은 구매자 보호 부재다. PayPal과 Stripe만이 구매자 보호를 제공하며, 모든 블록체인 네이티브 솔루션(Base Pay 포함)은 이 영역이 취약하다. Base Pay의 에스크로 모델은 온체인 구매자 보호의 기초를 제공하지만, 아직 완전한 분쟁 해결 메커니즘은 아니다.

**공백 4: AI 에이전트 + e-commerce 통합 결제**

x402가 AI 에이전트 결제를, Commerce Payments Protocol이 e-commerce 결제를 각각 담당하지만, 이 둘을 통합한 단일 결제 인프라는 아직 없다. AI 에이전트가 사용자를 대신하여 e-commerce 구매를 수행하는 시나리오에서, 에스크로 기반 결제와 x402의 결합이 필요하다.

### 7.3 위협 평가

| 위협 요인 | 심각도 | 시기 | 대응 방향 |
|----------|--------|------|----------|
| **Stripe Stablecoin의 Shopify 대규모 롤아웃** | 높음 | 2026 현재 진행 중 | Base Pay도 Shopify 네이티브 통합 확보 완료, 수수료 차별화(1% vs 1.5%) 강조 |
| **Solana Pay의 기관 파트너십 확대** | 중간 | 2026-2027 | Solana 대비 에스크로/프로그래머블 결제의 기능적 우위 부각 |
| **PayPal PYUSD 70개 시장 확장** | 중간 | 2026 진행 중 | 탈중앙화 + 오픈소스 가치 제안, 수수료 경쟁력, 크립토 네이티브 사용자 타깃 |
| **Polygon Open Money Stack $250M 투자** | 중간-높음 | 2026-2027 | 기존 Polygon 배포 활용, EVM 호환 생태계 내 경쟁 우위 강화 |
| **Lightning Square 400만 가맹점** | 낮음-중간 | 2026 | BTC 전용이라는 한계, 스테이블코인 결제와 다른 시장 세그먼트 |

---

## 8. 종합 평가 및 전략적 시사점

### 8.1 Base Pay의 경쟁 포지션 평가

Base Pay(Commerce Payments Protocol)는 경쟁 구도에서 **"프로그래머블 온체인 결제 프로토콜"**이라는 독자적 포지션을 확보하고 있다.

**강점 영역:**
- 에스크로/Auth-Capture 모델은 온체인 결제 솔루션 중 유일무이
- Coinbase 생태계 + Shopify 통합 + Stripe x402 시너지로 강력한 네트워크 효과
- 1% 수수료는 Stripe Stablecoin(1.5%), BitPay(1%+$0.25) 대비 경쟁력 있음
- 오픈소스 전략으로 생태계 확장 가능

**취약 영역:**
- 법정화폐 직접 정산 미지원 (BitPay, PayPal, Stripe 대비 열위)
- 구매자 보호/분쟁 해결 메커니즘 미비 (PayPal, Stripe 대비 열위)
- Solana Pay 대비 높은 플랫폼 수수료 (1% vs 0%)
- 미국/싱가포르 외 Coinbase Commerce 서비스 종료(2026.03)로 글로벌 접근성 제한

### 8.2 전략적 권고

1. **법정화폐 정산 강화 (최우선)**: Coinbase Business 통합을 통한 USD/EUR 직접 정산 기능 조기 출시가 BitPay, Stripe와의 경쟁에서 핵심적
2. **구매자 보호 프레임워크 구축**: 에스크로 모델 위에 온체인 분쟁 해결 레이어를 추가하여 PayPal/Stripe 수준의 구매자 보호 제공
3. **수수료 경쟁력 유지**: Solana Pay(0%)와의 수수료 격차를 에스크로/프로그래머블 기능의 부가가치로 정당화
4. **x402 시너지 극대화**: Commerce Payments Protocol과 x402의 통합 시나리오(AI 에이전트 대리 구매)를 선제적으로 개발
5. **글로벌 접근성 복원**: 미국/싱가포르 외 시장에서의 서비스 재개 또는 오픈소스 프로토콜을 통한 제3자 오퍼레이터 활성화

---

*본 보고서는 2026년 4월 14일 기준 공개된 정보를 바탕으로 작성되었습니다. 각 경쟁사의 수수료, 정책, 기능은 수시로 변경될 수 있으므로 의사결정 시 최신 정보를 추가 확인하시기 바랍니다.*

---

## Sources

- [Solana Payments Documentation](https://solana.com/docs/payments)
- [Solana Pay x Shopify Refund Process](https://commercedocs.solanapay.com/merchants/refunds)
- [Solana Pay - Decentralized Payments](https://solanapay.com/)
- [Solana Payments Goes Live With Instant Settlement](https://coinfomania.com/solana-payments-goes-live-with-instant-settlement-features/)
- [Solana Foundation Institutional Developer Platform](https://www.coindesk.com/tech/2026/03/24/solana-foundation-taps-mastercard-western-union-worldpay-for-institutional-developer-platform)
- [Gnosis Pay Card Review 2026](https://coingape.com/crypto-cards/gnosis-pay-card-review/)
- [Gnosis Pay Fees and Limits](https://help.gnosispay.com/hc/en-us/articles/39533569163284-Understanding-Your-Card-s-Fees-and-Limits)
- [Gnosis Pay - Official Site](https://gnosispay.com/)
- [Stripe x402 Documentation](https://docs.stripe.com/payments/machine/x402)
- [Stripe Taps Base for AI Agent x402 Payment Protocol](https://crypto.news/stripe-taps-base-ai-agent-x402-payment-protocol-2026/)
- [Stripe Adds x402 Integration - The Block](https://www.theblock.co/post/389352/stripe-adds-x402-integration-usdc-agent-payments)
- [x402 Protocol GitHub](https://github.com/coinbase/x402)
- [x402 Official Site](https://www.x402.org/)
- [x402 Explained - Allium](https://www.allium.so/blog/x402-explained-the-internet-native-payments-standard-for-apis-data-and-agent-commerce/)
- [Stripe Stablecoin Payments Documentation](https://docs.stripe.com/payments/stablecoin-payments)
- [Stripe Charges 1.5% for Stablecoin Transfers - Yahoo Finance](https://finance.yahoo.com/news/stripe-charges-1-5-stablecoin-145737023.html)
- [Stripe Stablecoin Subscriptions](https://stripe.com/blog/introducing-stablecoin-payments-for-subscriptions)
- [BitPay Pricing](https://www.bitpay.com/pricing)
- [BitPay Fees Support](https://support.bitpay.com/hc/en-us/articles/203324073-What-fees-will-I-pay-to-use-BitPay-for-payment-processing)
- [BitPay Settlement Documentation](https://developer.bitpay.com/docs/settlement)
- [BitPay Refund Process](https://support.bitpay.com/hc/en-us/articles/360000051746-How-to-claim-a-refund-from-a-BitPay-merchant-refund-email)
- [NOWPayments Pricing](https://nowpayments.io/pricing)
- [NOWPayments Review 2026](https://coingape.com/nowpayments-review/)
- [CoinGate Pricing](https://coingate.com/pricing)
- [CoinGate Merchant Refunds](https://coingate.com/merchant-refunds)
- [PayPal PYUSD](https://www.paypal.com/us/digital-wallet/manage-money/crypto/pyusd)
- [PayPal Expands PYUSD to 70 Markets](https://thecryptobasic.com/2026/03/17/paypal-expands-pyusd-stablecoin-to-70-markets-for-faster-global-payments-and-lower-fees/)
- [PayPal Crypto Payments Expansion - CoinDesk](https://www.coindesk.com/business/2025/07/28/paypay-expands-crypto-payments-for-u-s-merchants-to-cut-cross-border-fees)
- [Lightning Network](https://lightning.network/)
- [Lightning Network - Bitget Guide 2026](https://www.bitget.com/academy/lightning-network)
- [BTCPay Server Review 2026](https://blockfinances.fr/en/btcpay-server-review)
- [Strike Review 2026](https://www.bitcoin.diy/exchanges/strike-review)
- [BTCPay Server + Strike Integration](https://strike.me/en/blog/btcpay-server-integrates-strike-api-to-power-bitcoin-payments/)
- [Polygon Open Money Stack - CoinDesk](https://www.coindesk.com/business/2026/01/08/polygon-labs-unveils-open-money-stack-to-power-borderless-stablecoin-payments/)
- [Polygon $250M Stablecoin Push - PYMNTS](https://www.pymnts.com/cryptocurrency/2026/polygon-makes-250-million-dollar-investment-stablecoin-payments/)
- [Coinbase Commerce to Coinbase Business Transition](https://help.coinbase.com/en/transitioning-from-coinbase-commerce-to-coinbase-business)
- [Coinbase Commerce Shutdown Guide - MoonPay](https://www.moonpay.com/newsroom/coinbase-commerce-shutdown-guide-for-merchants)
- [Coinbase Payments Introduction](https://www.coinbase.com/blog/powering-the-future-of-ecommerce-introducing-coinbase-payments)
- [Crypto Payment Gateway Comparison 2026](https://aurpay.net/aurspace/crypto-payment-gateway-comparison-2026/)
