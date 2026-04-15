# 비즈니스 모델 및 기술 프로파일 -- Stripe 크립토 결제 서비스

## 분석 개요

- **분석 대상**: Stripe 크립토 결제 서비스 전체 (Stablecoin Payments, x402, MPP, Bridge/Tempo, Onramp, Pay with Crypto, Open Issuance)
- **분석 일시**: 2026-04-15
- **선행 분석 참조**: 01_시장 현황 분석 보고서
- **신뢰도 표기**: 확인됨 / 추정 / 불명확

---

## 1. 비즈니스 모델 요약

### 1.1 수익 유형 분류

Stripe 크립토 결제는 단일 수익 모델이 아니라, 복합적 수익 레이어를 구축하고 있다.

| 수익 유형 | 해당 제품 | 모델 |
|-----------|----------|------|
| **트랜잭션 수수료** | Stablecoin Payments, x402, Pay with Crypto | 결제 건당 퍼센트 기반 과금 |
| **전환 수수료(Onramp/Offramp)** | Crypto Onramp, Stablecoin Financial Accounts | 법정화폐-크립토 전환 시 수수료 |
| **인프라 이용료** | Open Issuance, Bridge API | 스테이블코인 발행/관리 플랫폼 수수료 |
| **준비금 수익 (추정)** | USDB, Open Issuance | 준비금(US Treasuries) 이자 수익 일부 |
| **네트워크 수수료 (추정)** | Tempo 블록체인 | 검증자 수수료, 네트워크 이용 수수료 |
| **부가 서비스** | Stripe Radar, Billing, Connect | 기존 Stripe 생태계 부가 서비스 연동 수익 |

### 1.2 핵심 가치 제안

1. **가맹점 zero-crypto 경험**: 가맹점은 크립토를 이해하거나 보유할 필요 없이, 기존 Stripe API로 스테이블코인 결제를 수취하고 법정화폐로 정산받음
2. **글로벌 도달성**: 월렛만 보유하면 국적 무관하게 결제 가능 -- 101개국 비즈니스가 스테이블코인 잔고를 보유/관리
3. **비용 우위**: 카드 결제(2.9%+30c) 대비 1.5%로 약 48% 비용 절감; 차지백 부재로 분쟁 비용 제거
4. **수직 통합 인프라**: 발행(Bridge/Open Issuance) + 블록체인(Tempo) + 월렛(Privy) + 결제(Stripe) 전체 스택 보유

### 1.3 주요 고객 세그먼트

| 세그먼트 | 제품 | 핵심 니즈 |
|---------|------|----------|
| SaaS/AI 기업 | Stablecoin Payments, 구독 | 글로벌 결제 수취, 낮은 수수료, 크로스보더 |
| AI 에이전트/개발자 | x402, MPP | 자율 결제, 마이크로페이먼트, API 과금 |
| Web3 DApp | Crypto Onramp | 법정화폐-크립토 전환, 사용자 온보딩 |
| 신흥시장 비즈니스 | Stablecoin Financial Accounts | 달러 접근성, 크로스보더 송수신 |
| 기업/기관 | Open Issuance | 자체 스테이블코인 발행, 브랜드 토큰 |
| 크립토 사용자 | Pay with Crypto | 보유 크립토로 직접 결제 |
| 플랫폼/마켓플레이스 | Connect + Stablecoin Payouts | 셀러에게 스테이블코인 정산 |

---

## 2. 수수료 모델 상세 분석

### 2.1 제품별 수수료 구조

| 제품 | 수수료 | 온체인 실비용 | 마진 | 비고 |
|------|--------|-------------|------|------|
| **Stablecoin Payments** | 1.5% | ~$0.0002 (Base) | 매우 높음 | USD 정산, 가스비 포함 [확인됨] |
| **Crypto Onramp** | ~5% (카드), ~1.5% (ACH) | 네트워크에 따라 상이 | 높음 | 결제 수단별 차등 [확인됨] |
| **Pay with Crypto** | 미공개 | - | - | 표준 Stripe 수수료 적용 추정 [추정] |
| **x402** | 미공개 (프리뷰) | Base USDC 전송비 | - | 제로 프로토콜 수수료 주장, Stripe 정산 수수료 별도 [추정] |
| **MPP** | 요청당 거의 제로 | Tempo 네트워크 비용 | - | 배치 정산으로 비용 최소화 [확인됨] |
| **Stablecoin Financial Accounts** | 전환 수수료 | - | - | 법정화폐-스테이블코인 전환 시 [확인됨] |
| **Open Issuance** | 미공개 | - | - | 발행/소각 자체 무료, 인프라 이용료 별도 [추정] |

### 2.2 수수료 논란과 경제성 분석

Stripe의 1.5% 스테이블코인 수수료는 업계에서 논란의 대상이다.

**온체인 실비용 대비 분석**:
- Base 네트워크 USDC 전송: ~$0.0002
- Stripe 수수료 ($100 결제 기준): $1.50
- **마크업 배율**: 약 7,500배

**Stripe의 반론 (추정)**:
- 온체인 비용만이 아닌 전체 결제 인프라 비용 포함
- KYC/AML 컴플라이언스 비용
- 실시간 USD 전환 및 정산 비용
- 사기 방지 및 모니터링 비용
- 400개+ 월렛 호환성 유지 비용
- 가맹점 대시보드, 리포팅, 회계 통합

**경쟁사 수수료 비교**:

| 서비스 | 수수료 | 비고 |
|--------|--------|------|
| Stripe Stablecoin Payments | 1.5% | USD 정산 포함 |
| Stripe 카드 결제 | 2.9% + 30c | 비교 기준 |
| Coinbase Commerce | 1% | 온체인 네이티브 |
| BitPay | 1% | 크립토 결제 전문 |
| PayPal (PYUSD) | 미공개 | 자체 스테이블코인 |
| 직접 온체인 수취 | ~$0.0002 | 인프라 자체 구축 필요 |

### 2.3 숨겨진 수익원 (추정)

1. **USDB 준비금 수익**: Bridge의 USDB는 BlackRock Short-Term Bond Fund 등에 준비금 투자. 준비금 이자 수익은 Bridge/Stripe에 귀속 [추정]
2. **FX 스프레드**: 스테이블코인-법정화폐 전환 시 환율 스프레드 [추정]
3. **Tempo 검증자 보상**: Tempo 네트워크 검증 참여에 따른 네트워크 수수료 수취 [추정]
4. **Open Issuance 플랫폼 수수료**: 기업이 발행한 스테이블코인의 유통/관리 인프라 이용료 [추정]
5. **생태계 고착화**: 크립토 결제 유입 -> Stripe Billing, Radar, Connect 등 부가 서비스 교차 판매 [확인됨]

---

## 3. 기술 아키텍처 심층 분석

### 3.1 전체 기술 스택 구조

```
+------------------------------------------------------------------+
|                    Stripe 크립토 결제 전체 아키텍처                  |
+------------------------------------------------------------------+
|                                                                    |
|  [프론트엔드 레이어]                                                |
|  +------------------+  +----------------+  +------------------+    |
|  | Stripe Checkout  |  | Stripe Elements|  | Payment Links    |    |
|  | (crypto.stripe   |  | (임베디드 위젯) |  | (노코드 결제)     |    |
|  |  .com 리디렉션)   |  |                |  |                  |    |
|  +------------------+  +----------------+  +------------------+    |
|                                                                    |
|  [월렛 연결 레이어]                                                 |
|  +------------------+  +----------------+  +------------------+    |
|  | Privy 임베디드   |  | WalletConnect  |  | 400+ 월렛 지원    |    |
|  | 월렛 인프라      |  | 프로토콜       |  | (MetaMask,       |    |
|  |                  |  |                |  |  Phantom 등)     |    |
|  +------------------+  +----------------+  +------------------+    |
|                                                                    |
|  [결제 처리 레이어]                                                 |
|  +------------------+  +----------------+  +------------------+    |
|  | PaymentIntents   |  | x402 Middleware|  | MPP Protocol     |    |
|  | API (crypto)     |  | (HTTP 402)     |  | (Tempo 기반)     |    |
|  +------------------+  +----------------+  +------------------+    |
|                                                                    |
|  [블록체인 인프라 레이어]                                            |
|  +------------------+  +----------------+  +------------------+    |
|  | Ethereum 노드    |  | Solana 노드    |  | Base (L2) 노드   |    |
|  | Polygon 노드     |  | Tempo (L1) 노드|  | 멀티체인 인덱서   |    |
|  +------------------+  +----------------+  +------------------+    |
|                                                                    |
|  [정산/전환 레이어]                                                 |
|  +------------------+  +----------------+  +------------------+    |
|  | Bridge 오케스트  |  | USD 자동 전환  |  | Stablecoin       |    |
|  | 레이션 엔진      |  | (OTC/AMM)     |  | Financial Accts  |    |
|  +------------------+  +----------------+  +------------------+    |
|                                                                    |
|  [컴플라이언스/보안 레이어]                                          |
|  +------------------+  +----------------+  +------------------+    |
|  | KYC/AML 파이프   |  | 온체인 모니터링 |  | Stripe Radar     |    |
|  | 라인 (Bridge)    |  | (제재 스크린)  |  | (사기 방지 ML)   |    |
|  +------------------+  +----------------+  +------------------+    |
|                                                                    |
|  [발행/관리 레이어]                                                 |
|  +------------------+  +----------------+  +------------------+    |
|  | Open Issuance    |  | USDB 발행/소각 |  | 준비금 관리      |    |
|  | (커스텀 코인)    |  | (Bridge)       |  | (BlackRock,      |    |
|  |                  |  |                |  |  Fidelity)       |    |
|  +------------------+  +----------------+  +------------------+    |
+------------------------------------------------------------------+
```

### 3.2 추정 기술 스택

| 영역 | 기술 | 신뢰도 |
|------|------|--------|
| **블록체인 클라이언트** | Reth (Paradigm의 고성능 Ethereum 클라이언트) -- Tempo 기반 | 확인됨 |
| **합의 알고리즘** | Simplex BFT (Commonware) -- Tempo | 확인됨 |
| **스마트 컨트랙트** | Solidity (EVM 호환) -- 구독 결제 컨트랙트 포함 | 확인됨 |
| **노드 인프라** | 멀티체인 풀 노드/아카이벌 노드 클러스터, 리전별 분산 | 추정 |
| **키 관리** | HSM, MPC (다자간 연산) 기반 커스터디 | 확인됨 |
| **월렛 인프라** | Privy (임베디드 셀프 커스터디 월렛) | 확인됨 |
| **백엔드** | Ruby (Stripe 코어), Go/Rust (성능 크리티컬 서비스) | 추정 |
| **API 프레임워크** | RESTful API (PaymentIntents 패턴) | 확인됨 |
| **데이터베이스** | PostgreSQL 기반 (Stripe 레거시) + 블록체인 인덱서 | 추정 |
| **메시지 큐** | Apache Kafka (이벤트 스트리밍, 웹훅 전달) | 추정 |
| **모니터링** | 온체인 트랜잭션 인덱서 + 제재 스크리닝 엔진 | 추정 |
| **컴플라이언스** | Bridge KYC/AML 파이프라인, OCC 은행 면허 기반 | 확인됨 |

---

## 4. 제품별 기술 구현 상세

### 4.1 Stablecoin Payments -- 결제-정산-환불 기술 흐름

#### 4.1.1 결제(Payment) 기술 흐름

**PaymentIntent 생성 (서버 사이드)**:
```
POST /v1/payment_intents
  payment_method_types[] = "crypto"
  amount = 1099
  currency = "usd"
```

**상세 흐름**:

```
[1] 가맹점 서버                   [2] Stripe API
    |                                  |
    |--- POST /payment_intents ------->|
    |    (amount, currency, crypto)     |
    |<-- client_secret 반환 ------------|
    |                                  |
[3] 프론트엔드                    [4] crypto.stripe.com
    |                                  |
    |--- confirmPayment() ------------>|
    |    (client_secret 전달)          |
    |                                  |
    |         [5] 월렛 연결            |
    |         (WalletConnect/직접연결)  |
    |         400+ 월렛 지원            |
    |                                  |
    |         [6] 토큰/체인 선택        |
    |         (USDC/USDP/USDG)        |
    |         (Ethereum/Solana/        |
    |          Polygon/Base)           |
    |                                  |
    |         [7] 트랜잭션 서명         |
    |         (사용자 월렛에서)         |
    |                                  |
    |         [8] 온체인 제출           |
    |         (Stripe가 브로드캐스트)   |
    |                                  |
[9] Stripe 블록체인 모니터링      [10] 확인
    |                                  |
    |--- 트랜잭션 감시 ------->        |
    |--- 블록 확인 대기 ------->       |
    |--- payment_intent.succeeded      |
    |    웹훅 발송 --------->          |
```

**기술적 핵심**:
- `payment_method_types[]`에 `"crypto"`를 지정하면 스테이블코인 결제 활성화
- 클라이언트가 `client_secret`으로 결제 프로세스를 시작하면 `crypto.stripe.com`으로 리디렉션
- Stripe가 해당 체인에 트랜잭션을 브로드캐스트하고 컨펌을 모니터링
- 블록 확인 후 `payment_intent.succeeded` 웹훅 이벤트 발송

#### 4.1.2 정산(Settlement) 기술 흐름

```
[온체인 수취]                    [USD 전환]                    [은행 출금]
    |                              |                              |
USDC/USDP/USDG  -------->  Bridge 오케스트레이션  -------->  Stripe 잔고
수취 확인                    엔진이 자동 전환                 (USD 반영)
    |                              |                              |
블록체인별                   OTC/유동성 풀을                  표준 정산 주기
컨펌 시간 상이               통해 USD 전환                   (T+2 영업일)
    |                              |                              |
Ethereum: ~12s              스테이블코인 1:1               가맹점 은행
Solana: ~0.4s               페깅 기반 전환                 계좌로 ACH/
Base: ~2s                   (슬리피지 최소화)              SEPA 출금
Polygon: ~2s
```

**정산 기술 세부사항**:
- **커스터디**: Bridge가 수취한 스테이블코인의 커스터디 담당. USDC (Circle 발행) 또는 USDB (Bridge 발행)로 보유 [확인됨]
- **USD 전환**: Bridge의 스테이블코인 오케스트레이션 엔진이 자동으로 USD 전환. 1:1 페깅 기반이므로 환율 리스크 최소 [확인됨]
- **정산 주기**: Stripe 표준 정산 주기(일반적으로 T+2 영업일)와 통합 관리 [확인됨]
- **정산 수수료**: 1.5% 트랜잭션 수수료에 포함 (별도 정산 수수료 없음) [확인됨]
- **Settlement Services Provider**: 별도의 정산 서비스 제공자와 계약 체결 필요 (Stripe Legal 문서 기준) [확인됨]

#### 4.1.3 환불(Refund) 기술 메커니즘

```
[가맹점]                      [Stripe]                    [고객 월렛]
    |                            |                            |
환불 요청                   Stripe가 새로운                온체인 트랜잭션
(API/대시보드)              온체인 트랜잭션 생성            수신 확인
    |                            |                            |
POST /v1/refunds            원래 결제의                    원래 결제 시
  charge=ch_xxx             스테이블코인 종류와             사용한 월렛
                            체인으로 환불                   주소로 수신
    |                            |                            |
    |                       주의: 테스트 환경에서            |
    |                       환불 토큰 컨트랙트가             |
    |                       결제 토큰과 다를 수 있음         |
```

**환불 기술 세부사항**:
- **메커니즘**: Stripe가 가맹점의 Stripe 잔고(USD)에서 차감 -> 해당 금액을 원래 스테이블코인으로 구매 -> 고객의 원래 월렛 주소로 온체인 전송 [확인됨]
- **환불 통화**: 원래 결제에 사용된 스테이블코인과 동일 [확인됨]
- **차지백 부재**: 블록체인 결제 특성상 차지백 메커니즘 없음 -- 가맹점에게 유리 [확인됨]
- **Stripe Disputes 미적용**: 스테이블코인 결제는 Stripe의 분쟁(Disputes) 시스템에 연동되지 않음 [확인됨]
- **비가역성**: 블록체인에 제출된 트랜잭션은 취소/역전 불가 [확인됨]
- **테스트 주의점**: 테스트 환불 시 수신 토큰의 컨트랙트 주소가 결제 토큰과 다를 수 있어 블록 익스플로러에서 `transaction_hash` 확인 필요 [확인됨]

#### 4.1.4 구독 결제 스마트 컨트랙트

Stripe는 스테이블코인 구독 결제를 위한 전용 스마트 컨트랙트를 개발했다.

**기술적 과제**: 블록체인에서는 매 트랜잭션마다 월렛 소유자의 서명이 필요하여, 반복 결제(구독)가 불가능한 근본적 한계가 존재.

**해결 방식**:
```
[최초 구독 등록]
1. 고객이 월렛 연결
2. Stripe 스마트 컨트랙트에 대한 "사전 승인(pre-approval)" 서명 1회
3. 스마트 컨트랙트가 승인된 범위 내에서 반복 인출 권한 획득

[반복 결제 실행]
1. Stripe Billing 엔진이 정기 결제 트리거
2. 스마트 컨트랙트가 고객 월렛에서 자동 인출
3. 재서명 불필요
4. payment_intent.succeeded 웹훅 발송
```

- **지원 체인**: Base, Polygon [확인됨]
- **지원 토큰**: USDC [확인됨]
- **월렛 호환**: 400개 이상 [확인됨]
- **카드 결제 유사 경험**: 월렛을 "결제 수단으로 저장"하는 UX -- 카드 저장과 동일 패러다임 [확인됨]

---

### 4.2 x402 프로토콜 -- 기술 아키텍처 상세

#### 4.2.1 프로토콜 구조

x402는 HTTP 402 "Payment Required" 상태 코드를 활용한 머신 네이티브 결제 프로토콜이다.

**3대 핵심 HTTP 헤더**:

| 헤더 | 방향 | 인코딩 | 용도 |
|------|------|--------|------|
| `PAYMENT-REQUIRED` | 서버 -> 클라이언트 (402 응답 시) | Base64 | 결제 요건: 토큰, 금액, 수신 주소, 체인 |
| `PAYMENT-SIGNATURE` | 클라이언트 -> 서버 (재요청 시) | Base64 | 서명된 결제 페이로드 (결제 증명) |
| `PAYMENT-RESPONSE` | 서버 -> 클라이언트 (성공 시) | Base64 | 정산/검증 결과 |

#### 4.2.2 결제 검증 흐름

```
[클라이언트/AI 에이전트]        [리소스 서버]           [Facilitator]        [Base 블록체인]
        |                          |                       |                      |
   (1)  |--- GET /resource ------->|                       |                      |
        |                          |                       |                      |
   (2)  |<-- HTTP 402 -------------|                       |                      |
        |    PAYMENT-REQUIRED:     |                       |                      |
        |    {token: USDC,         |                       |                      |
        |     amount: 0.01,        |                       |                      |
        |     address: 0xABC...,   |                       |                      |
        |     chain: base}         |                       |                      |
        |                          |                       |                      |
   (3)  |--- 결제 트랜잭션 생성 ---+---------------------->|                      |
        |    (월렛으로 서명)        |                       |                      |
        |                          |                       |                      |
   (4)  |                          |                       |--- 온체인 제출 ------>|
        |                          |                       |<-- 트랜잭션 확인 -----|
        |                          |                       |                      |
   (5)  |--- GET /resource ------->|                       |                      |
        |    PAYMENT-SIGNATURE:    |                       |                      |
        |    {signed_tx, proof}    |                       |                      |
        |                          |                       |                      |
   (6)  |                          |--- 검증 요청 -------->|                      |
        |                          |                       |--- 온체인 확인 ------>|
        |                          |<-- 검증 완료 ---------|                      |
        |                          |                       |                      |
   (7)  |<-- HTTP 200 -------------|                       |                      |
        |    PAYMENT-RESPONSE:     |                       |                      |
        |    {tx_hash, status}     |                       |                      |
        |    + 리소스 본문          |                       |                      |
```

#### 4.2.3 Facilitator 아키텍처

Facilitator는 x402 프로토콜의 핵심 미들웨어로, Web2와 Web3를 연결하는 중간 계층이다.

**Facilitator 역할**:
1. **결제 검증**: 서명된 트랜잭션의 유효성 확인
2. **금액/수신자 매칭**: 결제 금액과 수신 주소가 서버 요구사항과 일치하는지 검증
3. **온체인 정산 확인**: 트랜잭션이 실제로 블록체인에 정산되었는지 확인
4. **Stripe 잔고 연동**: 확인된 결제를 Stripe deposit address -> Stripe 잔고로 연결

**Stripe의 x402 Facilitator 구현**:
- Stripe가 deposit address를 생성하고 블록체인을 모니터링 [확인됨]
- PaymentIntent가 자동 캡처됨 (온체인 정산 확인 시) [확인됨]
- 인간 결제와 에이전트 결제가 동일한 Stripe 대시보드에 통합 표시 [확인됨]

**x402 Foundation 거버넌스**: Coinbase, Cloudflare, Google, Visa가 공동 관리 (2025.09~) [확인됨]

#### 4.2.4 x402 서버 통합 (미들웨어)

```
// 의사 코드: x402 미들웨어 적용
server.use("/paid-endpoint", x402Middleware({
    facilitator: "https://x402.stripe.com",   // Stripe Facilitator
    price: "$0.01",                             // USDC 가격
    token: "USDC",
    chain: "base",
    payTo: "0xYOUR_DEPOSIT_ADDRESS"
}));

server.get("/paid-endpoint", (req, res) => {
    // 결제 완료 후에만 도달
    res.json({ data: "premium content" });
});
```

---

### 4.3 Tempo 블록체인 -- 기술 아키텍처

#### 4.3.1 핵심 기술 사양

| 항목 | 상세 | 신뢰도 |
|------|------|--------|
| **유형** | 결제 전용 Layer-1 블록체인 | 확인됨 |
| **EVM 호환** | Solidity 스마트 컨트랙트 지원 | 확인됨 |
| **실행 엔진** | Reth (Paradigm의 Rust 기반 Ethereum 클라이언트) | 확인됨 |
| **합의** | Simplex BFT (Commonware -- Tempo가 $25M 투자) | 확인됨 |
| **TPS** | 100,000+ TPS (목표 1M TPS) | 확인됨 |
| **최종 확정성** | ~0.6초 (서브세컨드) 결정론적 파이널리티 | 확인됨 |
| **가스비 통화** | 모든 주요 스테이블코인으로 가스비 납부 가능 | 확인됨 |
| **온체인 AMM** | Enshrined AMM -- 가스비 전환용 자동화 마켓메이커 | 확인됨 |
| **프라이버시** | 옵트인 프라이버시 (민감한 트랜잭션 세부정보 은닉) | 확인됨 |
| **네이티브 토큰** | 없음 -- 스테이블코인 중립적 설계 | 확인됨 |
| **검증자** | Stripe, Visa, Zodia Custody (Standard Chartered 자회사) | 확인됨 |
| **인큐베이터** | Stripe + Paradigm 공동 인큐베이팅 | 확인됨 |

#### 4.3.2 합의 메커니즘 상세

```
[Simplex BFT 합의]

+------------------+     +------------------+     +------------------+
| Stripe 검증자    |     | Visa 검증자       |     | Zodia 검증자     |
| (결제 처리 데이터)|     | (카드 네트워크)   |     | (커스터디)       |
+--------+---------+     +--------+---------+     +--------+---------+
         |                         |                         |
         +------------+------------+------------+------------+
                      |                         |
              [Simplex BFT 라운드]         [블록 생성]
              - 비잔틴 장애 허용          - ~0.6초 파이널리티
              - 즉시 확정성              - 결정론적 (확률적이 아님)
              - 높은 처리량              - 리오그 없음
```

**현재 상태**: 초대된 검증자 집합(허가형) -> 향후 퍼미션리스 PoS로 전환 로드맵 [확인됨]

#### 4.3.3 Enshrined AMM

Tempo의 고유한 설계 -- 프로토콜 레벨에서 내장된 자동화 마켓메이커:
- 사용자가 보유한 스테이블코인 종류에 관계없이 가스비 납부 가능
- USDC 보유자가 USDT 기반 서비스 이용 시 자동 전환
- "스테이블코인 중립성" 구현의 핵심 메커니즘

---

### 4.4 Bridge 인프라 -- 기술 구조

#### 4.4.1 Bridge의 기능별 API 구조

```
Bridge API 레이어
+------------------------------------------------------------------+
|                                                                    |
|  [Orchestration API]                                               |
|  - 스테이블코인 생성/전송/수신                                      |
|  - 멀티체인 트랜잭션 브로드캐스트                                    |
|  - 트랜잭션 추적/인덱싱                                             |
|                                                                    |
|  [Issuance API (Open Issuance)]                                    |
|  - mint() / burn() -- 스테이블코인 발행/소각                        |
|  - 접근 제어 리스트 관리                                            |
|  - 다중 역할 승인 워크플로                                          |
|  - 전송 정책 설정                                                  |
|                                                                    |
|  [Conversion API]                                                  |
|  - 법정화폐 -> 스테이블코인 (Onramp)                               |
|  - 스테이블코인 -> 법정화폐 (Offramp)                               |
|  - ACH, SEPA 레일 지원                                             |
|                                                                    |
|  [Financial Accounts API]                                          |
|  - 스테이블코인 잔고 보유/관리                                      |
|  - 다중 통화 지원 (USD, EUR, GBP 확대 예정)                        |
|  - 외부 은행 계좌/월렛 연동                                         |
|                                                                    |
|  [Compliance API]                                                  |
|  - KYC/AML 파이프라인                                              |
|  - 제재 리스트 스크리닝                                             |
|  - 트랜잭션 모니터링                                                |
|  - OCC 은행 면허 기반 규제 준수                                     |
|                                                                    |
+------------------------------------------------------------------+
|  [인프라 레이어]                                                    |
|  - 멀티체인 노드 클러스터 (리전별 분산)                              |
|  - HSM/MPC 기반 키 관리                                            |
|  - 자동 페일오버                                                    |
|  - 트랜잭션 인덱싱 (자체 인덱서)                                    |
+------------------------------------------------------------------+
```

#### 4.4.2 USDB 스테이블코인

| 항목 | 상세 | 신뢰도 |
|------|------|--------|
| 발행자 | Bridge (Stripe 자회사) | 확인됨 |
| 페깅 | USD 1:1 | 확인됨 |
| 유형 | 인프라/클로즈드루프 스테이블코인 (공개 판매 불가) | 확인됨 |
| 준비금 | US 달러 + BlackRock Short-Term Bond Fund | 확인됨 |
| 규제 | OCC 국가 은행 면허 기반 | 확인됨 |
| 용도 | Stablecoin Financial Accounts의 기본 단위 | 확인됨 |

#### 4.4.3 Open Issuance 기술 구현

```
[기업의 스테이블코인 발행 흐름]

1. Bridge Open Issuance API 계약
2. 준비금 구성 결정
   - BlackRock (채권 펀드)
   - Fidelity (투자)
   - Superstate (DeFi 연계)
   - Lead Bank (현금 보관)
3. 스테이블코인 파라미터 설정
   - 이름, 심볼
   - 지원 체인
   - 접근 제어 정책
   - 발행/소각 한도
4. API 호출로 발행 시작

[준비금 관리]
- 준비금 비율: 현금 + US Treasuries (커스터마이징 가능)
- 준비금 수익: 발행 기업에 귀속
- 독립 감사: 정기적 제3자 감사

[상호운용성]
- Open Issuance로 발행된 모든 스테이블코인 간 1:1 스왑 가능
- "콜드 스타트" 문제 해결 -- 신규 발행 코인도 즉시 유동성 확보
```

---

### 4.5 Crypto Onramp 기술 구현

#### 4.5.1 통합 방식

| 방식 | 구현 | 용도 |
|------|------|------|
| **임베디드 위젯** | iframe/웹 컴포넌트로 DApp에 직접 삽입 | 원활한 사용자 경험 |
| **Stripe-hosted** | Stripe 호스팅 페이지로 리디렉션 | 빠른 통합 |

#### 4.5.2 KYC/사기 방지 기술

- 본인인증이 Onramp 위젯에 내장 [확인됨]
- Stripe의 기존 사기 방지 ML 모델 활용 [추정]
- 제재 리스트 스크리닝 자동화 [확인됨]
- 지갑 주소 리스크 스코어링 [추정]

---

### 4.6 MPP (Machine Payments Protocol) 기술 구현

#### 4.6.1 x402 vs MPP 기술 비교

| 기술 항목 | x402 | MPP |
|----------|------|-----|
| **기반 인프라** | Base L2 (Coinbase) | Tempo L1 (Stripe/Paradigm) |
| **합의** | Optimistic Rollup (Base) | Simplex BFT (Tempo) |
| **결제 수단** | USDC on Base 단일 | 스테이블코인 + 카드 + BTC Lightning |
| **정산 방식** | 건별 온체인 즉시 | 배치 정산 (비용 최소화) |
| **지연시간** | ~2초 (Base 블록 타임) | 서브-100ms |
| **API 패턴** | HTTP 402 헤더 기반 | PaymentIntents API 기반 |
| **프로토콜 수수료** | 제로 | 요청당 거의 제로 |
| **SPT 지원** | 없음 | Shared Payment Tokens (SPT) |
| **거버넌스** | x402 Foundation (오픈) | Tempo + Stripe |

#### 4.6.2 MPP PaymentIntents 통합

```
// 의사 코드: MPP 결제 수취
const paymentIntent = await stripe.paymentIntents.create({
    amount: 100,            // $0.01 (마이크로페이먼트)
    currency: 'usd',
    payment_method_types: ['mpp'],
    metadata: {
        agent_id: 'agent_abc123',
        resource: 'compute_hour'
    }
});
// MPP는 수 줄의 코드로 에이전트 결제 수취 [확인됨]
```

#### 4.6.3 Shared Payment Tokens (SPTs)

MPP의 고유 기능으로, AI 에이전트가 위임된 결제 권한을 다른 에이전트에게 전달하는 메커니즘:
- 에이전트 A가 에이전트 B에게 특정 금액/범위의 결제 권한을 위임
- 에이전트 B가 해당 권한으로 자율 결제 실행
- 기업이 에이전트에게 예산 할당하는 패턴에 최적화

---

## 5. 보안 및 컴플라이언스 기술 분석

### 5.1 보안 아키텍처

| 레이어 | 기술 | 상세 | 신뢰도 |
|--------|------|------|--------|
| **키 관리** | HSM + MPC | 단일 개인/머신이 전체 프라이빗 키 보유 불가 | 확인됨 |
| **커스터디** | Bridge 커스터디 | OCC 은행 면허 하에 자산 보관 | 확인됨 |
| **사기 방지** | Stripe Radar | ML 기반 실시간 사기 탐지 (카드 결제와 통합) | 추정 |
| **온체인 모니터링** | 제재 스크리닝 | 지갑 주소 제재 리스트 대조, 이상 패턴 감지 | 확인됨 |
| **KYC/AML** | Bridge 파이프라인 | 계정 레벨 리스크 = KYC 정보 + 거래 + 지역 + 행동 | 확인됨 |
| **노드 보안** | 멀티 리전 클러스터 | 페일오버, 혼잡 우회, 다운타임 자동 라우팅 | 추정 |
| **프라이버시** | Tempo 옵트인 프라이버시 | 민감한 트랜잭션 세부정보 온체인 은닉 가능 | 확인됨 |

### 5.2 규제 기반

| 규제 | 적용 대상 | 상세 |
|------|----------|------|
| **OCC 은행 면허** | Bridge | 연방 은행 감독 하 전자화폐 발행자로 운영 -- 크립토 기업 중 극히 드묾 [확인됨] |
| **GENIUS Act** | 미국 전체 | 2025.07 서명 -- 스테이블코인 규제 프레임워크 수립 [확인됨] |
| **MiCA** | EU | 전자화폐 토큰 규제 -- Open Issuance EU 배포 제한적 [확인됨] |
| **Settlement Services** | 가맹점 | 별도의 Settlement Services Provider 계약 필요 [확인됨] |

---

## 6. 인수 및 투자 현황

### 6.1 크립토 관련 인수

| 시기 | 대상 | 금액 | 목적 |
|------|------|------|------|
| 2024.10 | **Bridge** | $1.1B (11억 달러) | 스테이블코인 인프라 (오케스트레이션, 발행, 커스터디) [확인됨] |
| 2025.06 | **Privy** | 미공개 | 임베디드 월렛 인프라 (75M+ 계정, 1,000+ 개발팀) [확인됨] |
| 2025.12 | **Valora** (인재 인수) | 미공개 | 크립토 결제 앱 팀 -- 블록체인/스테이블코인 통합 가속 [확인됨] |

### 6.2 전략적 투자

| 대상 | 금액 | 관계 |
|------|------|------|
| **Commonware** | Tempo가 $25M 투자 | Simplex BFT 합의 알고리즘 제공 [확인됨] |
| **Tempo Labs** | Stripe + Paradigm 공동 인큐베이팅 | 결제 전용 L1 블록체인 [확인됨] |

### 6.3 파트너십 생태계

| 파트너 | 역할 | 영역 |
|--------|------|------|
| **Visa** | Tempo 검증자, 스테이블코인 링크드 카드 (100개국+) | 블록체인 + 카드 네트워크 [확인됨] |
| **Zodia Custody** (Standard Chartered) | Tempo 검증자 | 기관급 커스터디 [확인됨] |
| **Crypto.com** | Pay with Crypto 연동 | 소비자 크립토 결제 [확인됨] |
| **BlackRock** | Open Issuance 준비금 운용 | 자산 관리 [확인됨] |
| **Fidelity Investments** | Open Issuance 준비금 운용 | 자산 관리 [확인됨] |
| **Superstate** | Open Issuance 준비금 운용 | DeFi 연계 [확인됨] |
| **Circle** | USDC 발행자 | 스테이블코인 공급 [확인됨] |
| **Coinbase** | x402 프로토콜 공동, Base L2 | 결제 프로토콜 [확인됨] |
| **Cloudflare** | x402 Foundation 멤버 | CDN/에지 결제 [확인됨] |
| **Google** | x402 Foundation 멤버 | AI/클라우드 [확인됨] |
| **Paradigm** | Tempo 공동 인큐베이터 | 벤처/블록체인 기술 [확인됨] |
| **Payoneer** | Bridge 기반 스테이블코인 기능 (2026 Q2) | 크로스보더 결제 [확인됨] |

---

## 7. 확장성 평가

### 7.1 스케일업 가능성

| 영역 | 평가 | 근거 |
|------|------|------|
| **가맹점 확장** | 매우 높음 | 기존 수백만 Stripe 가맹점에 플러그인 방식 추가 -- 별도 통합 불필요 |
| **지역 확장** | 높음 | 101개국 Stablecoin Financial Accounts, 단 결제 수취는 현재 US만 |
| **거래량 확장** | 매우 높음 | Tempo 100,000+ TPS, 멀티체인 지원, 배치 정산 |
| **제품 확장** | 매우 높음 | Bridge + Privy + Tempo로 수직 통합 완성, 새 유스케이스 빠른 구축 |
| **AI 에이전트 시장** | 매우 높음 | x402 + MPP 이중 전략으로 에이전트 결제 시장 양면 커버 |

### 7.2 병목 요인

| 병목 | 상세 | 심각도 |
|------|------|--------|
| **규제 지역 제한** | Stablecoin Payments 가맹점 수취가 현재 US만 지원 -- 글로벌 확장에 가장 큰 병목 | 높음 |
| **소비자 월렛 보급** | 일반 소비자의 크립토 월렛 보유율이 아직 낮음 | 높음 |
| **분쟁/소비자 보호** | 차지백 부재, Disputes 미지원 -- 소비자 보호 관점에서 규제 리스크 | 중간 |
| **수수료 경쟁** | 1.5%에 대한 업계 비판 -- 경쟁사(Coinbase 1%, BitPay 1%) 대비 높음 | 중간 |
| **Tempo 검증자 중앙화** | 현재 소수의 초대된 검증자 -- 탈중앙화 전환까지 신뢰 리스크 | 중간 |
| **MiCA/EU 규제** | Open Issuance의 EU 배포 제한 | 중간 |
| **디페그/보안 리스크** | 스마트 컨트랙트 취약점, 브릿지 해킹, 디페그 시나리오 | 낮음 (구조적) |

### 7.3 경쟁 우위의 지속가능성

Stripe의 크립토 전략은 다음 세 가지 구조적 해자(moat)를 구축하고 있다.

1. **네트워크 효과**: 수백만 기존 가맹점 + 400개+ 월렛 지원 -> 양면 네트워크 효과. 새로운 진입자가 이 규모를 복제하기 어려움
2. **수직 통합**: 발행(Bridge) + 블록체인(Tempo) + 월렛(Privy) + 결제(Stripe) + 컴플라이언스(OCC 면허) -- 풀스택 통제로 비용/속도/경험 최적화
3. **개발자 플라이휠**: 기존 Stripe API 패러다임 유지 -- "crypto 지식 제로"로 통합 가능. 개발자 채택 -> 가맹점 증가 -> 사용자 증가의 선순환

---

## 8. 수익 모델 전망

### 8.1 단기 수익 (2026)

| 제품 | 예상 수익 기여 | 근거 |
|------|--------------|------|
| Stablecoin Payments | 높음 | Shadeform 등 AI 기업에서 결제의 ~20%가 스테이블코인 전환 |
| Crypto Onramp | 중간 | ~5% 수수료율로 높은 단위 마진, 단 볼륨 제한적 |
| x402 | 낮음-중간 | 7,500만+ 트랜잭션/30일, 프리뷰 단계 |
| Bridge/Stablecoin FA | 중간 | 101개국 서비스, 전환 수수료 + 준비금 수익 |

### 8.2 중장기 수익 동인 (2027+)

1. **Tempo 네트워크 수수료**: 메인넷 성숙 시 검증/정산 수수료 수익화
2. **Open Issuance 플랫폼화**: 기업 스테이블코인 시장 성장에 따른 인프라 수수료
3. **AI 에이전트 결제 폭증**: MPP/x402 기반 머신간 결제 시장 (현재 연환산 $6억 -> 수십억 전망)
4. **크로스보더 정산**: B2B 스테이블코인 거래량 증가 (2025년 $4,000억, YoY 2배 성장)
5. **Visa 협업**: 스테이블코인 링크드 카드 100개국+ 확대 -- 소비자 접점 확대

---

## 9. 핵심 인사이트

1. **Stripe는 "스테이블코인의 AWS"를 넘어 "스테이블코인의 전체 클라우드"를 구축 중**: IaaS(Bridge/Tempo) + PaaS(API) + SaaS(대시보드/Billing) 전 레이어를 수직 통합하며, 이는 결제 산업에서 유례없는 수준의 통합이다.

2. **1.5% 수수료의 진짜 의미는 "crypto를 없애는 비용"**: 온체인 비용 $0.0002 대비 7,500배 마크업은 논란이지만, Stripe가 제공하는 가치는 "가맹점이 크립토를 전혀 다루지 않아도 되는 추상화 레이어"이며, 이는 카드 결제 2.9%+30c 대비 여전히 저렴하다.

3. **이중 프로토콜 전략(x402 + MPP)은 의도적 헤지**: x402(Coinbase/Base 생태계)와 MPP(자체 Tempo 생태계)를 동시에 지원함으로써, 어느 프로토콜이 시장 표준이 되더라도 Stripe가 결제 처리의 중심에 서는 구조다.

4. **OCC 은행 면허는 크립토 기업 중 가장 강력한 규제 자산**: Bridge의 OCC 면허는 전통 은행 수준의 규제 신뢰도를 부여하며, 이는 기관 고객 유치와 글로벌 확장에서 결정적 차별화 요소다.

5. **구독 스마트 컨트랙트는 크립토 결제의 "킬러 피처"**: 매 트랜잭션 서명이 필요한 블록체인의 근본적 한계를 해결한 Stripe의 사전승인 스마트 컨트랙트는, SaaS/구독 경제와 크립토 결제를 최초로 자연스럽게 연결한다.

6. **Tempo의 "토큰 없는 블록체인" 설계는 전략적 선택**: 네이티브 토큰 없이 스테이블코인만으로 운영되는 설계는, 규제 리스크(증권법)를 회피하면서 결제 인프라로서의 순수 유틸리티에 집중하는 접근이다.

---

## Sources

- [Stripe Stablecoin Payments Documentation](https://docs.stripe.com/payments/stablecoin-payments)
- [Stripe x402 Documentation](https://docs.stripe.com/payments/machine/x402)
- [Stripe Pricing](https://stripe.com/pricing)
- [Stripe Blog: Stablecoin Payments for Subscriptions](https://stripe.com/blog/introducing-stablecoin-payments-for-subscriptions)
- [Stripe Blog: Open Issuance from Bridge](https://stripe.com/blog/introducing-open-issuance-from-bridge)
- [Stripe Blog: Stablecoin Financial Accounts](https://stripe.com/blog/introducing-stablecoin-financial-accounts)
- [Stripe Dev Blog: Stablecoin Payments No Crypto Knowledge](https://stripe.dev/blog/using-stripe-stablecoin-payments-no-crypto-knowledge)
- [Yahoo Finance: Stripe Charges 1.5%](https://finance.yahoo.com/news/stripe-charges-1-5-stablecoin-145737023.html)
- [Bridge.xyz](https://www.bridge.xyz/)
- [x402.org](https://www.x402.org/)
- [Stablecoin Insider: x402 Protocol](https://stablecoininsider.org/x402-protocol/)
- [insights4vc: Tempo Blockchain](https://insights4vc.substack.com/p/tempo-stripes-blockchain-for-stablecoin)
- [insights4vc: Stripe's Stablecoin Strategy](https://insights4vc.substack.com/p/stripes-stablecoin-strategy)
- [Paradigm: Tempo](https://www.paradigm.xyz/2025/09/tempo-payments-first-blockchain)
- [CoinDesk: Visa Tempo Validator](https://www.coindesk.com/business/2026/04/14/visa-throws-its-weight-behind-stripe-s-tempo-blockchain)
- [CoinDesk: Stripe Acquires Privy](https://www.coindesk.com/business/2025/06/11/stripe-to-acquire-crypto-wallet-startup-privy-in-bid-to-expand-web3-capabilities)
- [CoinDesk: Stripe Acqui-Hires Valora](https://www.coindesk.com/business/2025/12/10/stripe-acqui-hires-crypto-payments-startup-valora-venturing-further-into-stablecoins)
- [PYMNTS: Stripe Tempo](https://www.pymnts.com/blockchain/2026/stripe-wants-reinvent-global-settlement-tempo/)
- [The Block: Stripe x402](https://www.theblock.co/post/389352/stripe-adds-x402-integration-usdc-agent-payments)
- [Fortune: Stripe Tempo MPP](https://fortune.com/2026/03/18/stripe-tempo-paradigm-mpp-ai-payments-protocol/)
- [Ledger Insights: Bridge USDB](https://www.ledgerinsights.com/stripe-rolls-out-stablecoin-accounts-in-101-countries-as-bridge-launches-usdb/)
- [WorkOS Blog: x402 vs MPP](https://workos.com/blog/x402-vs-stripe-mpp-how-to-choose-payment-infrastructure-for-ai-agents-and-mcp-tools-in-2026)
- [Stripe Legal: Stablecoin Payments](https://stripe.com/legal/stablecoin-payments)
- [Stripe Connect: Stablecoin Payouts](https://docs.stripe.com/connect/stablecoin-payouts)
- [Stripe: Accept Stablecoin Payments](https://docs.stripe.com/payments/accept-stablecoin-payments)
- [The Paypers: Payoneer Bridge](https://thepaypers.com/crypto-web3-and-cbdc/news/payoneer-to-roll-out-stablecoin-capabilities-supported-by-bridge-in-q2-2026)
- [Blockworks: Stripe Paradigm Tempo](https://blockworks.co/news/stripe-and-paradigm-incubate-tempo)

---

*본 분석은 2026년 4월 15일 기준 공개된 정보를 바탕으로 작성되었습니다. "확인됨"은 공식 문서/발표에서 검증된 정보, "추정"은 공개 정보로부터의 합리적 추론, "불명확"은 정보 부족으로 판단 보류를 의미합니다.*
