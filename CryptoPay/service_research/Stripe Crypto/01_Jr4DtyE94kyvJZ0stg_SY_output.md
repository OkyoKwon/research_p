# 시장 현황 분석 -- Stripe 크립토 결제 서비스

## 분석 개요

- **분석 대상**: Stripe 크립토 결제 서비스 전체 (Stablecoin Payments, x402/MPP, Crypto Onramp/Offramp, Pay with Crypto)
- **분석 일시**: 2026-04-15
- **주요 참조 소스**: Stripe 공식 블로그/뉴스룸, Stripe Documentation, PYMNTS.com, The Block, Fortune Crypto, CoinDesk, a16z, McKinsey, Forrester, WorkOS Blog, Yahoo Finance, CNBC

---

## 1. Stripe 크립토 전략 전체상

### 1.1 전략 배경 및 Bridge 인수

Stripe는 2024년 10월 스테이블코인 인프라 기업 **Bridge**를 **11억 달러(약 1.5조 원)**에 인수하며, 주요 결제 기업 역사상 최대 규모의 크립토 인수를 단행했다. 이 거래는 2025년 2월 규제 승인을 거쳐 최종 완료되었다.

Bridge 인수의 전략적 의도는 다음과 같다:

- **크로스보더 결제 비용 절감**: Stripe의 국경 간 거래량은 연간 50% 성장 중이며, 스테이블코인을 통해 기존 금융 네트워크 대비 비용과 실패율을 크게 줄일 수 있음
- **신흥시장 진출 가속화**: 결제 인프라가 미비한 국가에서 스테이블코인 기반으로 서비스 지역을 46개국에서 101개국으로 확대
- **스테이블코인 인프라 자체 구축**: Bridge의 발행/관리 API를 활용해 Open Issuance, Stablecoin Financial Accounts 등 새로운 제품군 출시

> 출처: [CNBC](https://www.cnbc.com/2025/02/04/stripe-closes-1point1-billion-bridge-deal-prepares-for-stablecoin-push-.html), [a16z Newsletter](https://a16z.com/newsletter/what-stripes-acquisition-of-bridge-means-for-fintech-and-stablecoins-april-2025-fintech-newsletter/), [Fortune Crypto](https://fortune.com/crypto/2025/10/01/stripe-crypto-stablecoins-open-issuance-bridge-blockchain-tempo/)

### 1.2 Tempo 블록체인 (2026년)

2026년 2월 25일, Stripe는 **Tempo**라는 결제 전용 레이어1 블록체인을 발표했다.

| 항목 | 상세 |
|------|------|
| 목적 | 결제에 최적화된 블록체인, 스테이블코인 네이티브 지원 |
| 처리 성능 | 100만 TPS 이상, 서브세컨드(sub-second) 최종 확정 |
| 검증자 | Stripe, Visa, Zodia Custody (연간 수조 달러 결제 처리 기업들) |
| 핵심 프로토콜 | Machine Payments Protocol (MPP) -- AI 에이전트 자율 결제 표준 |
| 상태 | 2025년 12월 퍼블릭 테스트넷 / 2026년 3월 메인넷 론칭 |

> 출처: [PYMNTS](https://www.pymnts.com/blockchain/2026/stripe-wants-reinvent-global-settlement-tempo/), [CoinDesk](https://www.coindesk.com/tech/2026/03/18/stripe-led-payments-blockchain-tempo-goes-live-with-protocol-for-ai-agents/), [CoinCentral](https://coincentral.com/stripe-and-tempo-build-high-speed-blockchain-for-ai-payment/)

### 1.3 제품 포트폴리오 요약

| 제품 | 론칭 시기 | 대상 | 핵심 기능 |
|------|-----------|------|-----------|
| Stablecoin Payments | 2025.12 (일반), 2025.10 (구독 프리뷰) | B2B/B2C 가맹점 | 스테이블코인으로 결제 수취, USD 정산 |
| Stablecoin Financial Accounts | 2025.05 | 101개국 비즈니스 | 스테이블코인 잔고 보유/송수신 |
| Open Issuance (Bridge) | 2025.09 | 기업/기관 | 자체 스테이블코인 발행/관리 |
| Crypto Onramp | 2022.12~ (지속 확장) | Web3 DApp | 법정화폐 -> 크립토 전환 |
| Pay with Crypto (Crypto.com) | 2026.01 | 소비자 | 크립토 잔고로 직접 결제 |
| x402 Protocol | 2025~ (프리뷰) | 개발자/AI 에이전트 | HTTP 402 기반 머신 결제 |
| MPP (Machine Payments Protocol) | 2026.03 | AI 에이전트/서비스 | Tempo 기반 자율 결제 표준 |

---

## 2. 시장 규모 및 성장률

### 2.1 스테이블코인 시장 전체

| 구분 | 규모 | 기준 연도 | 출처 |
|------|------|-----------|------|
| 스테이블코인 시가총액 | 약 2,517억 달러 | 2025년 중반 | CoinLaw |
| 스테이블코인 시가총액 | 약 3,086억 달러 | 2026년 1월 | Stablecoin Insider |
| 스테이블코인 시가총액 전망 | 1조 달러 초과 전망 | 2026년 말 (추정) | 업계 추산 |
| 스테이블코인 연간 결제 볼륨 | 약 3,900억 달러 (실질 결제) | 2025년 | McKinsey |
| 스테이블코인 결제 연환산 런레이트 | 1,220억 달러 | 2025년 | 업계 추산 |
| B2B 스테이블코인 거래량 | 4,000억 달러 | 2025년 (전년 대비 2배) | PYMNTS |

### 2.2 크립토 결제 게이트웨이 시장

| 구분 | 규모 | 기준 연도 | 출처 |
|------|------|-----------|------|
| 글로벌 크립토 결제 게이트웨이 시장 | 20억 달러 | 2025년 | GII Research |
| 글로벌 크립토 결제 게이트웨이 시장 | 23.9억 달러 | 2026년 | GII Research |
| CAGR | 19.0% | 2025-2026 | GII Research |

### 2.3 스테이블코인 결제 인프라 플랫폼 시장

| 구분 | 규모 | 기준 연도 | 출처 |
|------|------|-----------|------|
| 글로벌 시장 규모 | 76억 달러 | 2025년 | Research Intelo |
| 전망 규모 | 약 894억 달러 | 2034년 | Research Intelo |
| CAGR | 32.1% | 2026-2034 | Research Intelo |

---

## 3. 제품별 상세 분석: 결제 - 정산 - 환불

### 3.1 Stablecoin Payments (스테이블코인 결제 수취)

#### 결제(Payment) 프로세스

| 항목 | 상세 |
|------|------|
| **결제 흐름** | 고객이 결제 시 -> crypto.stripe.com으로 리디렉션 -> 크립토 월렛 연결 -> 스테이블코인 전송 -> 가맹점 Stripe 잔고에 USD로 반영 |
| **지원 스테이블코인** | USDC (Ethereum, Solana, Polygon, Base), USDP (Ethereum, Solana), USDG (Ethereum) |
| **지원 블록체인** | Ethereum, Solana, Polygon, Base |
| **지원 월렛** | 400개 이상의 월렛 지원 |
| **수수료** | **1.5%** (가맹점 부담) |
| **구독 결제** | 스마트 컨트랙트 기반 반복 결제 승인 -- 매 트랜잭션마다 재서명 불필요 |
| **가맹점 요건** | 현재 미국(US) 기반 비즈니스만 수취 가능 |
| **고객 범위** | 글로벌 (월렛 보유 고객이면 국적 무관) |

#### 정산(Settlement) 프로세스

| 항목 | 상세 |
|------|------|
| **정산 통화** | USD (미국 달러) |
| **정산 방식** | 스테이블코인 수취 -> Stripe가 자동으로 USD 전환 -> 가맹점 Stripe 잔고에 반영 |
| **정산 주기** | Stripe 표준 정산 주기 적용 (일반적으로 T+2 영업일, 카드 결제와 동일하게 통합 관리) |
| **자동 환전** | 스테이블코인 -> USD 자동 전환 (가맹점은 크립토 노출 없음) |
| **정산 수수료** | 1.5% 트랜잭션 수수료에 포함 |

#### 환불(Refund) 시나리오

| 항목 | 상세 |
|------|------|
| **환불 가능 여부** | 가능 |
| **환불 방식** | 스테이블코인으로 고객의 원래 월렛 주소로 반환 (온체인 트랜잭션) |
| **환불 통화** | 원래 결제에 사용된 스테이블코인 |
| **분쟁(Dispute) 지원** | **지원하지 않음** -- 스테이블코인 결제는 Stripe의 Disputes 시스템 미적용 |
| **취소/역전** | **불가** -- 블록체인에 제출된 트랜잭션은 취소/역전 불가 |
| **차지백** | **없음** -- 크립토 결제 특성상 차지백 메커니즘 부재 (가맹점에게 유리) |
| **주의사항** | 잘못된 주소로의 송금은 복구 불가; 환불 시 결제 시점 크립토 가치 수동 추적 필요 |

> 출처: [Stripe Docs - Stablecoin Payments](https://docs.stripe.com/payments/stablecoin-payments), [Yahoo Finance](https://finance.yahoo.com/news/stripe-charges-1-5-stablecoin-145737023.html), [Stripe Legal](https://stripe.com/legal/stablecoin-payments)

---

### 3.2 x402 Protocol 및 MPP (머신/에이전트 결제)

#### x402 Protocol

| 항목 | 상세 |
|------|------|
| **프로토콜 개요** | HTTP 402 "Payment Required" 상태 코드를 활용한 온체인 결제 프로토콜 |
| **개발 주체** | Coinbase가 2025년 5월 최초 개발; 이후 x402 Foundation (Coinbase, Cloudflare, Google, Visa) 공동 관리 |
| **Stripe 통합** | Stripe가 x402를 통합하여 개발자가 USDC on Base로 AI 에이전트에 직접 과금 가능 |
| **결제 흐름** | 클라이언트가 유료 리소스 요청 -> 서버가 HTTP 402 + 결제 상세 반환 -> 클라이언트 결제 -> 인증 포함 재요청 |
| **지원 통화** | USDC on Base |
| **정산** | Stripe 잔고에 반영 (deposit address 생성, 블록체인 모니터링, Stripe 잔고 정산) |
| **현재 규모** | 최근 30일: 7,500만+ 트랜잭션, 2,400만+ 달러 볼륨, 9.4만 구매자, 2.2만 판매자 |

> 출처: [Stripe Docs - x402](https://docs.stripe.com/payments/machine/x402), [The Block](https://www.theblock.co/post/389352/stripe-adds-x402-integration-usdc-agent-payments)

#### MPP (Machine Payments Protocol)

| 항목 | 상세 |
|------|------|
| **프로토콜 개요** | Tempo 블록체인 기반의 오픈 스탠다드 머신 결제 프로토콜 |
| **론칭일** | 2026년 3월 18일 (Tempo 메인넷과 동시) |
| **공동 개발** | Tempo + Stripe |
| **지원 결제 수단** | 스테이블코인(Tempo), 신용/체크카드(Stripe/Visa), 비트코인(Lightning), 커스텀 결제 수단 |
| **핵심 기능** | PaymentIntents API 기반 수 줄 코드로 에이전트 결제 수취; Shared Payment Tokens(SPTs) 지원 |
| **성능** | 배치 정산, 서브-100ms 지연시간, 요청당 거의 제로 수수료 |
| **유스케이스** | AI 에이전트 자율 결제 (컴퓨팅, 데이터, 클라우드 리소스), 마이크로페이먼트, 반복 결제 |

#### x402 vs MPP 비교

| 구분 | x402 | MPP |
|------|------|-----|
| 인프라 | Coinbase/Base L2 | Stripe/Tempo L1 |
| 결제 수단 | USDC on Base (크립토 전용) | 스테이블코인 + 카드 + BTC Lightning (멀티) |
| 타겟 | 에이전트 네이티브, 인간 개입 없는 자율 결제 | 에이전트 + 기존 결제 수단 통합 |
| 정산 | 온체인 즉시 | 배치 정산, 기존 Stripe 잔고 통합 |
| 생태계 | Coinbase, Cloudflare, Google, Visa | Stripe, Visa, Zodia |

> 출처: [WorkOS Blog](https://workos.com/blog/x402-vs-stripe-mpp-how-to-choose-payment-infrastructure-for-ai-agents-and-mcp-tools-in-2026), [Stripe Blog](https://stripe.com/blog/machine-payments-protocol), [PYMNTS](https://www.pymnts.com/news/payment-methods/2026/stripe-backed-protocol-lets-ai-agents-transact-autonomously/)

---

### 3.3 Crypto Onramp (법정화폐 -> 크립토 전환)

#### 결제(Purchase) 프로세스

| 항목 | 상세 |
|------|------|
| **서비스 유형** | 법정화폐 -> 크립토 전환 (Onramp만 제공, Offramp 미제공) |
| **통합 방식** | 임베디드 위젯 또는 Stripe-hosted 옵션 |
| **지원 크립토** | USDC (Ethereum, Solana, Polygon, Avalanche, Base), ETH, MATIC, AVAX, XLM |
| **결제 수단** | 신용/체크카드, Apple Pay, ACH 은행 이체 (미국 전용) |
| **수수료** | 약 5% 내외 (예: $100 USDC 구매 시 $4.99; 금액/결제 수단에 따라 변동) |
| **KYC** | 내장 본인인증 및 사기 방지 도구 포함 |
| **지원 국가** | 미국 (하와이 제외) 및 EU |

#### 정산 프로세스

| 항목 | 상세 |
|------|------|
| **정산 방식** | 사용자가 법정화폐로 결제 -> Stripe가 크립토로 전환 -> 사용자 월렛으로 즉시 전송 |
| **정산 속도** | KYC 완료 후 즉시 크립토 전달 |
| **플랫폼 수익** | Stripe가 트랜잭션 수수료 수취; DApp 운영자는 커미션 설정 가능 |

#### 환불 시나리오

| 항목 | 상세 |
|------|------|
| **환불** | Onramp 특성상 표준 환불 프로세스 미제공 (크립토가 이미 사용자 월렛에 전달되므로) |
| **지역 제한** | 뉴욕주에서 XLM, USDC(Stellar/Avalanche/Polygon) 이용 불가; EU에서 ETH(Base), MATIC, AVAX 등 제한 |

> 출처: [Stripe Docs - Crypto Onramp](https://docs.stripe.com/crypto/onramp), [Stripe Newsroom](https://stripe.com/newsroom/news/fiat-to-crypto-onramp), [GetIvy](https://www.getivy.io/fiat-onramps/stripe-crypto-onramp)

---

### 3.4 Pay with Crypto (Crypto.com 연동 -- 소비자 크립토 결제)

#### 결제(Payment) 프로세스

| 항목 | 상세 |
|------|------|
| **파트너십** | Stripe x Crypto.com (2026년 1월 발표, 최초의 크립토 플랫폼 직접 연동) |
| **결제 흐름** | 소비자가 Crypto.com 앱 내 크립토 잔고로 Stripe 가맹점에서 직접 결제 -> Stripe/Crypto.com이 법정화폐로 전환 -> 가맹점에 정산 |
| **지원 결제 수단** | Crypto.com 보유 암호화폐 전체 + 스테이블코인 |
| **사전 환전** | 불필요 -- 소비자가 크립토를 먼저 법정화폐로 바꿀 필요 없음 |
| **지원 국가** | 미국 우선 론칭, 이후 글로벌 확대 예정 |

#### 정산(Settlement) 프로세스

| 항목 | 상세 |
|------|------|
| **정산 통화** | 가맹점이 선호하는 현지 통화 (법정화폐) |
| **정산 방식** | Stripe 잔고에 다른 결제 수단과 동일하게 통합 입금 |
| **자동 환전** | Stripe + Crypto.com이 크립토 -> 법정화폐 자동 전환 |
| **가맹점 부담** | 가맹점은 크립토 관련 별도 작업 불필요 (기존 Stripe 연동만으로 수취) |

#### 환불(Refund) 시나리오

| 항목 | 상세 |
|------|------|
| **차지백** | **없음** -- 크립토 결제이므로 전통적 차지백 메커니즘 미적용 (가맹점 유리) |
| **환불 처리** | 가맹점이 직접 환불 처리 필요; 결제 시점의 크립토 가치를 수동으로 추적/관리해야 함 |
| **스테이블코인 환불** | 스테이블코인으로 결제된 경우, 고객의 원래 월렛으로 스테이블코인 반환 |

> 출처: [Yahoo Finance](https://finance.yahoo.com/personal-finance/investing/article/stripe-users-can-now-pay-with-crypto-through-new-cryptocom-partnership-175929078.html), [PYMNTS](https://www.pymnts.com/cryptocurrency/2026/stripe-integrates-cryptocom-facilitate-crypto-payments/), [Stripe Customers](https://stripe.com/customers/crypto-com-spotlight)

---

### 3.5 Stablecoin Financial Accounts

| 항목 | 상세 |
|------|------|
| **서비스 개요** | 스테이블코인 기반 금융 계좌 -- 잔고 보유, 송수신, 법정화폐 입출금 |
| **지원 스테이블코인** | USDC (Circle), USDB (Bridge) |
| **지원 법정화폐 레일** | ACH, SEPA (USD, EUR 시작, GBP 확대 예정) |
| **지원 국가** | 101개국 (기존 Stripe 46개국에서 대폭 확대; 아르헨티나, 칠레, 터키, 콜롬비아, 페루 등 포함) |
| **핵심 기능** | 다중 통화 잔고 보유, 통화 간 전환, 가상/실물 카드 발급 |
| **론칭** | 2025년 5월 |

> 출처: [Stripe Blog](https://stripe.com/blog/introducing-stablecoin-financial-accounts), [Bloomberg](https://www.bloomberg.com/news/articles/2025-05-07/stripe-introduces-stablecoin-accounts-in-more-than-100-countries), [Ledger Insights](https://www.ledgerinsights.com/stripe-rolls-out-stablecoin-accounts-in-101-countries-as-bridge-launches-usdb/)

---

### 3.6 Open Issuance (자체 스테이블코인 발행)

| 항목 | 상세 |
|------|------|
| **서비스 개요** | 기업이 수 줄의 코드로 자체 스테이블코인을 발행/관리할 수 있는 플랫폼 |
| **기반 인프라** | Bridge API |
| **준비금 관리** | BlackRock, Fidelity Investments, Superstate가 준비금 운용; Lead Bank이 현금 보관 |
| **핵심 기능** | 무제한 발행/소각, 준비금 커스터마이징, 상호운용성 (Open Issuance로 발행된 코인 간 완전 호환) |
| **론칭** | 2025년 9월 |
| **사례** | Sui 네트워크가 USDsui를 Bridge Open Issuance로 발행 |

> 출처: [Stripe Blog](https://stripe.com/blog/introducing-open-issuance-from-bridge), [CoinDesk](https://www.coindesk.com/business/2025/11/12/sui-launches-native-stablecoin-usdsui-using-bridge-s-open-issuance-platform)

---

## 4. 수수료 체계 종합

| 제품 | 수수료 | 비고 |
|------|--------|------|
| Stablecoin Payments | 1.5% | 온체인 비용(약 $0.0002) 대비 논란 존재; USD 정산 포함 |
| Crypto Onramp | 약 5% 내외 | $100 기준 $4.99; 결제 수단/금액에 따라 변동 |
| Pay with Crypto | 미공개 | Crypto.com 연동; 표준 Stripe 가맹점 수수료 체계 적용 추정 |
| x402 | 미공개 (프리뷰) | USDC on Base 기반; 온체인 수수료 + Stripe 정산 수수료 |
| MPP | 요청당 거의 제로 | Tempo 기반 배치 정산; 대량 마이크로페이먼트에 최적화 |
| Stablecoin Financial Accounts | 전환 수수료 적용 | 법정화폐 <-> 스테이블코인 전환 시 수수료 |
| Open Issuance | 불필요한 수수료 없이 발행/소각 | 준비금 수익은 발행 기업에 귀속 |

> 출처: [Yahoo Finance](https://finance.yahoo.com/news/stripe-charges-1-5-stablecoin-145737023.html), [Stripe Pricing](https://stripe.com/pricing)

---

## 5. 경쟁 환경

### 5.1 주요 경쟁자

| 기업 | 주요 제품/전략 | 시장 포지셔닝 |
|------|---------------|--------------|
| **PayPal** | PYUSD 스테이블코인, 크립토 매매/결제 | 자체 스테이블코인 보유; 5,600억 달러 결제 플랫폼의 블록체인 통합 |
| **Coinbase Commerce** | Commerce Payments Protocol, Base L2 | authorize-and-capture 모델 (카드 결제 유사 흐름); 온체인 네이티브 |
| **BitPay** | B2B/B2C 크립토 결제 게이트웨이 | 크립토 결제 전문 10년 이상 경험; 다양한 코인 지원 |
| **MoonPay** | 온/오프램프, Helio 인수(2025.01) | 온램프 시장 선도; 결제 인프라 강화 |
| **Visa** | Tempo 검증자 참여, USDC 결제 | 기존 카드 네트워크와 스테이블코인 브릿지 |

### 5.2 Stripe의 차별화 포인트

1. **기존 가맹점 네트워크**: 수백만 Stripe 가맹점에 크립토 결제를 플러그인 방식으로 추가 가능
2. **엔드투엔드 인프라**: 결제 수취 -> 자동 환전 -> 정산까지 원스톱 처리
3. **Bridge/Tempo 수직 통합**: 스테이블코인 발행(Bridge) + 결제 블록체인(Tempo) + 결제 처리(Stripe) 수직 통합
4. **AI 에이전트 커머스**: MPP/x402를 통한 머신 결제 선점
5. **개발자 경험**: 기존 Stripe API와 동일한 패러다임으로 크립토 결제 통합 (수 줄의 코드)

---

## 6. 규제 대응 및 지원 국가

### 6.1 규제 프레임워크

| 지역 | 규제 현황 | Stripe 대응 |
|------|----------|-------------|
| **미국** | GENIUS Act (2025년 7월 서명) -- 스테이블코인 규제 프레임워크 수립 | Stablecoin Payments는 현재 US 가맹점만 수취 가능; SEC 동향 모니터링 |
| **EU** | MiCA (Markets in Crypto-Assets) 시행 | 전자화폐 토큰 발행 규제로 Open Issuance EU 배포 제한적; Onramp EU 지원 |
| **글로벌** | 국가별 상이한 크립토 규제 | 101개국 Stablecoin Financial Accounts; 국가별 규제 준수 접근 |

### 6.2 지원 국가 요약

| 제품 | 가맹점(수취) 지원 국가 | 소비자(결제) 지원 국가 |
|------|----------------------|----------------------|
| Stablecoin Payments | 미국만 (현재) | 글로벌 (월렛 보유자) |
| Crypto Onramp | 미국 (하와이 제외), EU | 동일 |
| Pay with Crypto | 미국 우선 론칭 | Crypto.com 사용자 |
| Stablecoin Financial Accounts | 101개국 | - |
| x402/MPP | 프리뷰 (지역 제한 정보 미공개) | - |

### 6.3 컴플라이언스 특징

- **KYC/AML**: Crypto Onramp에 내장된 본인인증 및 사기 방지 도구
- **준비금 투명성**: Open Issuance의 준비금은 BlackRock, Fidelity 등 기관급 운용사가 관리
- **정산 서비스 제공자**: 스테이블코인 결제 이용 시 별도의 Settlement Services Provider와 계약 체결

---

## 7. 산업 트렌드 및 성장 동인

### 7.1 핵심 트렌드

1. **"스테이블코인의 여름" (2025)**: Stripe가 자사 연간 서한에서 2025년을 "stablecoin summer"로 명명. AI 기업 Shadeform 사례에서 결제 볼륨의 약 20%가 스테이블코인으로 전환
2. **AI 에이전트 커머스 부상**: 자율 AI 에이전트가 데이터, 컴퓨팅 등 리소스를 자동 구매하는 시대 도래. x402, MPP 등 머신 결제 프로토콜 경쟁 본격화
3. **크로스보더 결제 혁신**: B2B 스테이블코인 거래량이 2025년 4,000억 달러로 전년 대비 2배 성장. 기존 SWIFT/코레스 뱅킹 대비 비용/속도 우위
4. **규제 명확화**: 미국 GENIUS Act, EU MiCA 등으로 스테이블코인 법적 지위 확립. 기관 참여 가속화
5. **전통 금융의 크립토 통합**: Visa, Stripe, PayPal 등 거대 결제 기업들의 본격적 크립토 인프라 구축

### 7.2 성장 동인

- 크로스보더 결제 비용 절감 수요 (특히 신흥시장)
- AI/자동화 경제의 마이크로페이먼트 수요 급증
- 스테이블코인 규제 프레임워크 정비로 기관 채택 확대
- 개발도상국의 달러 접근성 니즈 (Stablecoin Financial Accounts)
- 구독 경제의 스테이블코인 결제 전환

### 7.3 저해 요인 및 리스크

- **규제 불확실성**: 국가별 상이한 규제, 특히 EU MiCA 하 Open Issuance 제한
- **수수료 논란**: 온체인 비용 대비 Stripe의 1.5% 수수료에 대한 업계 비판
- **분쟁 해결 부재**: 스테이블코인 결제는 차지백/분쟁 시스템 미지원 -- 소비자 보호 관점에서 약점
- **월렛 보급률**: 일반 소비자의 크립토 월렛 보유/사용 경험 부족
- **기술 리스크**: 스마트 컨트랙트 취약점, 브릿지 해킹, 디페그 리스크 등

---

## 8. 타임라인 요약

| 시기 | 주요 이벤트 |
|------|------------|
| 2024.10 | Stripe, Bridge 11억 달러 인수 발표 |
| 2025.02 | Bridge 인수 규제 승인 완료 |
| 2025.05 | Stablecoin Financial Accounts 론칭 (101개국) |
| 2025.05 | x402 Protocol 프리뷰 (Coinbase 개발, Stripe 통합) |
| 2025.07 | 미국 GENIUS Act 서명 (스테이블코인 규제 프레임워크) |
| 2025.09 | Open Issuance (Bridge) 론칭 |
| 2025.10 | 스테이블코인 구독 결제 프리뷰 (US) |
| 2025.12 | Stablecoin Payments 일반 출시; Tempo 테스트넷 |
| 2026.01 | Pay with Crypto (Crypto.com 연동) 론칭 |
| 2026.02 | Tempo 블록체인 발표 |
| 2026.03 | Tempo 메인넷 + MPP 론칭 |
| 2026.04 | Visa, Zodia가 Tempo 검증자로 합류 |

---

## 9. 핵심 인사이트

1. **Stripe는 "스테이블코인의 AWS"를 지향**: Bridge(발행) + Tempo(블록체인) + Stripe(결제/정산) 수직 통합으로 스테이블코인 인프라 전체를 장악하려는 전략
2. **가맹점 진입 장벽 최소화**: 기존 Stripe API 패러다임 유지 -- 가맹점은 크립토 지식 없이도 수 줄의 코드로 스테이블코인 결제 수취 가능
3. **정산의 핵심은 "가맹점은 법정화폐만 받는다"**: 모든 크립토 결제가 자동으로 USD/현지 통화로 전환되어 가맹점의 크립토 리스크를 제로화
4. **환불/분쟁의 구조적 한계**: 블록체인 결제 특성상 차지백 불가, 분쟁 시스템 미지원은 소비자 보호 측면에서 해결해야 할 과제
5. **AI 에이전트 결제가 차세대 성장 축**: x402/MPP를 통한 머신간 자율 결제는 Stripe 크립토 전략의 다음 챕터

---

*본 보고서는 2026년 4월 15일 기준 공개된 정보를 바탕으로 작성되었습니다. 수치 및 정보는 각 출처의 발행 시점 기준이며, 시장 상황에 따라 변동될 수 있습니다.*
