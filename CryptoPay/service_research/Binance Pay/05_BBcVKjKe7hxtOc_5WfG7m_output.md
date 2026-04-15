# 바이낸스 페이(Binance Pay) 딥리서치 보고서

## Executive Summary

> - **시장 지배적 규모**: Binance Pay는 누적 거래량 USD 280B+, 연간 USD 121B, 2,000만 가맹점을 보유한 세계 최대 암호화폐 결제 플랫폼이다. 3억 명 이상의 Binance 사용자 기반이 핵심 경쟁력이다.
> - **스테이블코인 중심 결제**: B2C 결제의 98%가 스테이블코인(USDT/USDC)으로 처리되어, 사실상 "디지털 달러 결제 플랫폼"으로 기능하고 있다.
> - **법정화폐 정산 불가가 최대 구조적 약점**: 경쟁사(BitPay, Crypto.com Pay, PayPal, Stripe) 대부분이 법정화폐 직접 은행 입금을 지원하는 반면, Binance Pay는 불가하여 전통 사업자 온보딩에 가장 큰 장벽으로 작용한다.
> - **오프체인 즉시 정산이 핵심 기술 차별점**: Binance Ledger 기반 10,000+ TPS, 10ms 이내 지연, 가스비 제로의 정산 성능은 경쟁사 대비 독보적이나, 탈중앙화 가치와 상충한다.
> - **규제 리스크가 최대 외부 변수**: 미국/영국/EU 일부 시장 미진출(70개국 이상 제한)이 고소득 시장 성장을 제약하며, 스테이블코인 규제 강화와 CBDC 출시가 중장기 위협 요인이다.

---

## 리서치 개요

- **분석 대상**: Binance Pay (바이낸스 페이) -- Binance 거래소 기반 암호화폐 결제 서비스 (https://pay.binance.com/en)
- **분석 범위**: 결제(Payment) - 정산(Settlement) - 환불(Refund) 시나리오 중심의 서비스 심층 분석, 시장 현황, 경쟁사 비교, 사용자 인사이트, 비즈니스 모델/기술 아키텍처
- **작성 일시**: 2026-04-15
- **참여 분석 모듈**: market-analyst, competitor-analyst, user-review-analyst, biz-tech-analyst, research-reviewer

---

## 1. 서비스 개요

### 바이낸스 페이란?

Binance Pay는 세계 최대 암호화폐 거래소인 Binance가 2021년 출시한 **오프체인 암호화폐 결제 서비스**이다. Binance 앱에 내장된 형태로, 개인 간 P2P 송금과 가맹점(Merchant) 결제를 모두 지원하는 통합 결제 플랫폼이다.

### 주요 제품/기능 라인업

| 제품 | 설명 | 대상 |
|------|------|------|
| **P2P 결제** | Binance 사용자 간 무료 즉시 암호화폐 전송 (Pay ID, QR, 이메일, 전화번호) | 개인 사용자 |
| **Merchant 결제** | 가맹점이 고객으로부터 암호화폐 결제를 수취 (API, Hosted Checkout, Payment Links) | 사업자 |
| **Payout** | 가맹점이 다수에게 일괄 출금 (Batch Payout API, 최대 500명/배치) | 사업자 |
| **Payment Links** | 코딩 없이 결제 링크 생성, 이메일/SNS 공유 | 소규모 사업자, 프리랜서 |

### 핵심 수치

| 지표 | 수치 | 기준 시점 | 출처 |
|------|------|-----------|------|
| 누적 거래량 | USD 280B+ | 출시 이후 누적 | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |
| 연간 거래량 | USD 121B | 2025년 | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |
| 누적 거래 건수 | 13.6억 건 | 2026년 2월 기준 | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |
| Binance Pay 거래 수수료 매출 | 약 USD 110M | 2025년 | [Business of Apps](https://www.businessofapps.com/data/binance-statistics/) |
| Binance 전체 등록 사용자 | 3억 명+ | 2025년 말 | [Incrypted](https://incrypted.com/en/binance-reported-for-2025-34t-in-trades-and-300m-users/) |
| Binance Pay 가맹점 수 | 2,000만+ | 2025년 | [Airdrops.io](https://airdrops.io/blog/binance-pay-20-million-merchants-stablecoin-payments/) |
| Binance Pay P2P 활성 사용자 | 4,500만 명+ | 2025년 | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |

> **교차 검증 주석**: 가맹점 2,000만 수치는 Payment Links 기반 소규모 사업자 중심으로, API 통합 대형 가맹점 수는 미공개이다. 2024년 1.2만에서 2025년 2,000만으로의 1,700배 성장은 "가맹점" 정의 범위 확대에 기인한 것으로 추정된다.

---

## 2. 결제(Payment) 시나리오 상세

### 2.1 시나리오 A: P2P 개인 간 결제

P2P 결제는 Binance 사용자 간 직접 암호화폐를 전송하는 방식이다.

**Step-by-step 결제 흐름:**

1. 송금자가 Binance 앱 > Pay 메뉴 진입
2. 상대방의 Pay ID, 이메일, 전화번호 입력 또는 QR 코드 스캔
3. 전송할 암호화폐 종류 선택 (300종 이상 지원)
4. 전송 금액 입력
5. 확인 후 즉시 상대방 Binance Funding Wallet에 이체 완료

**핵심 특성:**
- **수수료**: 0% (무료)
- **처리 속도**: 즉시 (오프체인, Binance 내부 원장 처리)
- **가스비**: 0% (블록체인 트랜잭션이 아님)
- **지원 암호화폐**: 300종 이상
- **전제 조건**: 송수신 양측 모두 Binance 계정 + KYC 인증 필수

### 2.2 시나리오 B: Merchant 결제 (Hosted Checkout)

가맹점이 Binance가 호스팅하는 결제 페이지로 고객을 리다이렉트하여 결제를 수취하는 방식이다. 가장 빠른 통합 방법으로, PCI DSS 부담 없음.

**Step-by-step 결제 흐름:**

1. 가맹점 서버가 Create Order V2 API (`POST /binancepay/openapi/v2/order`) 호출하여 주문 생성
2. API 응답으로 `checkoutUrl`, `qrcodeLink`, `deeplink`, `universalUrl` 수신
3. 고객을 Binance Web Checkout Page로 리다이렉트 (`checkoutUrl`)
4. 고객이 3가지 방법 중 선택: QR 코드 스캔 / Binance 앱 열기(딥링크) / 웹 로그인
5. 고객이 50종 이상의 암호화폐 중 결제 수단 선택
6. 고객이 결제 확인
7. Binance Pay 시스템이 결제 처리 + 자동 환전(필요 시)
8. 가맹점 Binance Funding Wallet에 정산 통화(USDT 등)로 즉시 입금
9. Binance Pay가 가맹점에 Webhook 콜백 발송 (`bizStatus: "PAY_SUCCESS"`)
10. 고객이 `returnUrl`로 리다이렉트

> 출처: [Binance Merchant Docs - Hosted Checkout](https://merchant.binance.com/en/docs/functionalities/single-payment/hosted-checkout-page)

### 2.3 시나리오 C: Merchant 결제 (C2B API / Payment Links)

**C2B Native API 결제 흐름:**

1. 가맹점이 Create Order V2 API 호출
2. 응답의 `qrContent`를 활용하여 가맹점 자체 UI에서 QR 코드 렌더링
3. 또는 `deeplink`를 활용하여 인앱 결제 흐름 구현
4. 고객이 Binance 앱에서 결제 수단 선택 후 결제
5. Webhook으로 결제 결과 수신

**Payment Links 결제 흐름:**

1. 가맹점이 Merchant Management Platform에서 결제 링크 생성 (코딩 불필요)
2. 링크를 이메일, SNS, 웹사이트 등에 공유
3. 고객이 링크 클릭 후 Binance 결제 플로우 진행
4. 결제 완료 시 가맹점 대시보드에서 확인

**적합 대상:** Payment Links는 소규모 사업자/프리랜서, Native API는 대규모 이커머스/앱 서비스에 적합

### 2.4 시나리오 D: QR 코드 결제

오프라인 매장에서의 QR 코드 기반 결제 시나리오이다.

**Step-by-step:**

1. 가맹점이 API로 주문 생성 후 QR 코드를 매장 디스플레이에 표시
2. 고객이 Binance 앱의 스캐너로 QR 코드 스캔
3. 앱이 자동으로 금액, 결제 대상 정보를 인식
4. 고객이 결제할 암호화폐 선택 후 확인
5. 즉시 처리 완료, 가맹점에 Webhook 알림

### 2.5 지원 암호화폐 및 결제 방식

| 구분 | 지원 범위 |
|------|-----------|
| P2P 결제 가능 암호화폐 | 300종 이상 |
| Merchant 결제 가능 암호화폐 | 50종 이상 (BTC, ETH, BNB, USDT, USDC, SOL, XRP 등) |
| 주문 통화 | 법정화폐(USD, EUR 등) 단위 주문 생성 가능. 실제 수취는 크립토로 정산 |
| 결제 인터페이스 | QR 코드, Pay ID, 이메일, 전화번호, Binance 사용자명, Hosted Checkout, Payment Link, 딥링크 |

### 2.6 수수료 구조

| 수수료 항목 | 요율 | 비고 |
|-------------|------|------|
| P2P 송금 수수료 | 0% | Binance 사용자 간 무료 |
| 가맹점 결제 수수료 (MDR) | 1.0% | 고객 결제 금액 기준, Merchant Discount Rate |
| Payout 수수료 | 0.80% (최대 USD 5/건) | 2024년 12월 1일부터 적용. 기존 무료에서 유료 전환 |
| 블록체인 가스비 | 0% | 오프체인 정산으로 불필요 |
| FX 스프레드 (숨겨진 비용) | 추정 0.1~0.5% | 결제 통화와 정산 통화가 다를 때 자동 환전 시 내재 마진. 공식 비공개 |
| P2P 분쟁 처리 수수료 | 4회차부터 부과 | 처음 3회 무료 |

> 출처: [Binance Pay Fees FAQ](https://www.binance.com/en/support/faq/binance-pay-fees-6ff1944867e54b9a9576bce3109c7f7a)

### 2.7 경쟁사 비교 (결제)

| 항목 | Binance Pay | BitPay | Coinbase Commerce | NOWPayments | Crypto.com Pay | PayPal Crypto | Stripe Stablecoin |
|------|:-----------:|:------:|:-----------------:|:-----------:|:--------------:|:-------------:|:-----------------:|
| MDR | 1.0% | 1~2% + $0.25 | 1% | 0.5~1% | 0% | 0.99~1.5% | 1.5% |
| 지원 코인 수 | 50종+(가맹점) | 100종+ | 수백 종(Base) | 300종+ | 20종+ | 100종+ | USDC만 |
| P2P 송금 | 무료, 즉시 | 별도(BitPay Wallet) | 별도(Coinbase Wallet) | 미지원 | 앱 내 | PayPal P2P | 미지원 |
| QR 결제 | 가능 | 가능 | 가능 | 가능 | 가능 | 가능 | 불가 |
| 구독 결제 | **미지원** | 지원 | 지원(온체인) | 지원 | 지원 | 지원 | 지원 |
| Binance 계정 필수 | **예** | 아니오 | 아니오 | 아니오 | 아니오 | 아니오 | 아니오 |

---

## 3. 정산(Settlement) 시나리오 상세

### 3.1 오프체인 즉시 정산 메커니즘

Binance Pay의 핵심 기술적 차별점은 **블록체인을 거치지 않는 오프체인 내부 원장 정산**이다. 블록체인 네트워크 대신 Binance 내부 원장(Binance Ledger)에서 모든 자금 이동을 처리한다.

**정산 처리 흐름:**

```
[고객 Binance Funding Wallet]
     |
     | 1. 고객이 BTC로 결제
     v
+------------------------------------------+
|          Binance Internal Ledger          |
|                                          |
|  2. 고객 잔고에서 BTC 차감 (원장 기록)    |
|  3. FX Engine: BTC -> USDT 변환          |
|     (내부 유동성 풀 활용, 스프레드 내재)   |
|  4. MDR 1% 차감 (Binance 수수료 계정)    |
|  5. 가맹점 잔고에 USDT 가산 (원장 기록)   |
+------------------------------------------+
     |
     v
[가맹점 Binance Funding Wallet에 USDT 즉시 입금]
```

**Binance Ledger 성능 지표 (확인됨):**

| 항목 | 수치 |
|------|------|
| TPS (초당 트랜잭션) | 10,000+ (4노드 클러스터 기준) |
| 트랜잭션 지연 | 대부분 10ms 이내 완료 |
| 페일오버 시간 | 1초 이내 |
| 아키텍처 | Raft 합의 알고리즘 + RocksDB (쓰기 최적화) + 관계형 DB (조회 최적화) |
| 배포 | 멀티 AZ(가용 영역) 분산 배포, 과반수 노드 정상 시 데이터 무손실 |

> 출처: [Binance Blog - How Binance Ledger Powers Your Binance Experience](https://www.binance.com/en/blog/tech/how-binance-ledger-powers-your-binance-experience-5409682424466769892)

### 3.2 정산 통화 옵션

- **기본 정산 통화**: USDT (테더)
- **가맹점 설정 가능**: 가맹점이 정산 설정에서 선호 통화를 정의하면, 고객이 어떤 암호화폐로 결제하든 해당 통화로 자동 환전 후 정산
- **별도 정산 주기 없음**: 결제 완료와 동시에 가맹점 Binance Funding Wallet에 즉시 입금 (T+0 실시간)

| 시나리오 | 처리 방식 | 추가 비용 |
|----------|-----------|-----------|
| 고객이 BTC로 결제, 가맹점 USDT 정산 | Binance FX Engine이 BTC를 USDT로 자동 전환 후 정산 | FX 스프레드 (추정 0.1~0.5%) |
| 고객이 USDT로 결제, 가맹점 USDT 정산 | 환전 불필요, 직접 이체 | 0% |
| 법정화폐 단위 주문 (예: USD 100) | 고객은 50종+ 크립토 중 선택, 가맹점은 USDT로 수취 | FX 스프레드 |

### 3.3 법정화폐 전환 경로 (한계점)

Binance Pay는 **법정화폐 직접 은행 입금이 불가**하다. 가맹점이 법정화폐로 자금을 수취하려면 아래 추가 단계가 필요하다.

```
[결제 수취] --> [USDT로 자동 정산] --> [Binance 거래소에서 수동 환전] --> [법정화폐 출금]
                                       ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                                       가맹점이 직접 처리해야 하는 추가 단계
                                       (거래소 수수료 0.1% + 법정화폐 출금 수수료 별도)
```

**우회 경로:**
- **채널 파트너 경유**: Alchemy Pay 등 채널 파트너를 통해 법정화폐 정산이 가능하나, 추가 수수료와 복잡성을 수반
- **Binance Card**: Visa 네트워크를 통한 법정화폐 결제로, Binance Pay가 커버하지 못하는 법정화폐 소비 보완

### 3.4 Payout API

가맹점이 다수의 수신자에게 일괄 출금할 수 있는 Batch Payout 시스템이다.

**엔드포인트:** `POST /binancepay/openapi/payout/transfer`

| 항목 | 사양 |
|------|------|
| 최대 수신자 | 배치당 500명 |
| 수수료 | 0.80% (건당 최대 USD 5) |
| Binance 사용자 수신 | Funding Wallet에 즉시 입금 |
| 비 Binance 사용자 수신 | 이메일 초대 발송, 72시간 내 KYC 미완료 시 자동 환불 |
| subMerchantId | 채널 파트너의 하위 가맹점 Payout 관리용 (2025년 신규) |
| 수동 처리 | Merchant Management Platform에서 CSV 업로드 |

> 출처: [Binance Pay Batch Payout API](https://developers.binance.com/docs/binance-pay/api-payout)

### 3.5 수수료 구조 (총비용 시뮬레이션)

**시나리오: 가맹점이 USD 10,000 매출을 법정화폐로 최종 수취하는 경우**

| 비용 항목 | Binance Pay | BitPay | Coinbase Commerce | Stripe Stablecoin |
|-----------|:-----------:|:------:|:-----------------:|:-----------------:|
| 결제 수수료 (MDR) | $100 (1%) | $200 (2%) | $100 (1%) | $150 (1.5%) |
| FX 스프레드 | ~$25 (추정 0.25%) | 포함 | 포함 | 포함 |
| 법정화폐 전환 수수료 | $10 (거래소 0.1%) | $0 (포함) | $0 (포함) | $0 (포함) |
| 법정화폐 출금 수수료 | ~$5~15 | $0 (은행 직접) | 변동 | $0 |
| **총비용** | **~$140~150** | **~$200** | **~$100** | **~$150** |
| **실효 수수료율** | **~1.4~1.5%** | **~2.0%** | **~1.0%** | **~1.5%** |

> **주의**: Binance Pay의 법정화폐 전환 경로는 수동 처리가 필요하여 시간/노력 비용이 추가로 발생한다. 단순 수수료 비교만으로는 총비용을 정확히 반영하기 어렵다.

### 3.6 경쟁사 비교 (정산)

| 항목 | Binance Pay | BitPay | Coinbase Commerce | CoinGate | Crypto.com Pay | PayPal Crypto | Stripe Stablecoin |
|------|:-----------:|:------:|:-----------------:|:--------:|:--------------:|:-------------:|:-----------------:|
| 정산 속도 | **즉시** | T+1~T+2 | ~200ms(Base) | 즉시~24h | 수 시간~1일 | 즉시~T+1 | 즉시(USDC)/T+2(법정화폐) |
| 법정화폐 직접 정산 | **불가** | **가능(37개국)** | 가능(Coinbase 경유) | **가능(180개국+)** | **가능** | **자동 USD** | **자동 전환** |
| 크립토 정산 | USDT 기본 | 가능(15종) | USDC 기본 | 가능 | 가능 | PYUSD | USDC |
| 정산 주기 | 실시간 | 매 영업일 | 실시간 | 즉시~24h | T+0~T+1 | 즉시 | 즉시~T+2 |
| 가스비 부담 | 없음(오프체인) | 환불 시 마이너 수수료 | 가맹점(~$0.01) | 네트워크 수수료 | 네트워크 수수료 | 없음 | Stripe 부담 |

---

## 4. 환불(Refund) 시나리오 상세

### 4.1 시나리오 A: 전액 환불

**Step-by-step 흐름:**

1. 가맹점이 Merchant Management Platform > Transaction Tab에서 해당 주문 확인
2. 또는 Refund Order API (`POST /binancepay/openapi/order/refund`) 호출
3. 원래 주문의 `prepayId`와 환불 금액(= 원래 주문 금액) 입력
4. 환불 사유 입력 (선택)
5. Binance Pay가 원래 주문 검증 + 환불 금액 검증 + 중복 요청 확인
6. 가맹점 Binance Funding Wallet에서 환불금 차감
7. 고객 Binance Funding Wallet에 환불금 즉시 입금
8. MDR 수수료도 비례 환불 (`refundCommission`)
9. Webhook으로 `bizStatus: "REFUND_SUCCESS"` 발송
10. 주문 상태가 `FULL_REFUNDED`로 변경

**주요 API 요청 파라미터:**

| 파라미터 | 필수 | 설명 |
|----------|------|------|
| `refundRequestId` | Y | 가맹점이 부여하는 환불 요청 고유 ID (최대 64자) |
| `prepayId` | Y | 원래 주문의 Binance 주문 ID (19자) |
| `refundAmount` | Y | 환불 금액 (원래 주문 금액과 동일) |
| `refundReason` | N | 환불 사유 (최대 256자) |
| `webhookUrl` | N | 환불 결과 웹훅 URL |

### 4.2 시나리오 B: 부분 환불

부분 환불은 주문 금액의 일부만 반환하는 방식으로, 여러 차례 반복 가능하다.

**핵심 규칙:**
- 누적 환불 금액이 원래 주문 금액을 초과할 수 없음
- API 응답의 `remainingAttempts`가 1이면 다음 환불 시 자동으로 전액 환불 처리
- `refundedAmount` 필드로 기 환불된 누적 금액 확인 가능
- `duplicateRequest` 플래그로 중복 요청 감지

**주요 에러 코드:**

| 코드 | 설명 |
|------|------|
| `400202` | ORDER_NOT_FOUND -- 주문을 찾을 수 없음 |
| `400607` | PAYMENT_REFUND_TOO_MANY_TIMES -- 환불 횟수 초과 |
| `400608` | PAYMENT_REFUND_AMOUNT_INVALID -- 잘못된 환불 금액 |
| `400611` | PAYMENT_INSUFFICIENT_BALANCE -- 가맹점 잔액 부족 |

### 4.3 환불 통화 및 금액 처리

환불은 **가맹점이 수취한 정산 통화**로 처리된다. 역환전(reverse conversion)은 수행되지 않는다.

| 시나리오 | 환불 처리 |
|----------|-----------|
| 고객이 BTC로 결제, 가맹점이 USDT로 정산 받음 | 고객에게 **USDT로** 환불 (BTC가 아님) |
| 고객이 ETH로 결제, 가맹점이 USDT로 정산 받음 | 고객에게 **USDT로** 환불 |
| 고객이 USDT로 결제, 가맹점이 USDT로 정산 받음 | 고객에게 **USDT로** 환불 |

**수수료 환불 공식 (추정):**
```
refundCommission = (refundAmount / orderAmount) * originalCommission
```

> **사용자 불만 포인트**: BTC로 결제했는데 USDT로 환불 받으면, BTC 가격 상승 시 고객이 손실을 볼 수 있다. 이는 사용자 인사이트 분석에서 중간 빈도/중간 심각도로 보고된 Pain Point이다.

### 4.4 환불 시간 제한

- **환불 처리 속도**: 즉시 (오프체인 처리)
- **환불 요청 가능 기한**: 공식 문서상 명시적 기한은 확인되지 않으나, 주문이 `PAID` 상태인 한 환불 가능
- **주문 만료**: 미결제 주문은 기본 1시간(최대 15일) 후 `EXPIRED` 상태로 전환, 만료 후 환불 불필요

### 4.5 분쟁 해결 절차

**Merchant 결제 분쟁:**
- 전통적인 신용카드 차지백(chargeback) 메커니즘은 **존재하지 않음**
- 암호화폐 결제의 특성상 결제 확정 후 자동 취소/환불이 불가
- 환불 여부는 **가맹점 재량**으로 결정
- Binance는 중개자로서 분쟁 조정 역할 수행 가능하나 강제력은 제한적
- 구매자 보호 프로그램(PayPal Purchase Protection 등에 해당)은 **없음**

**P2P 거래 분쟁:**
- 고객서비스가 24~48시간 내 분쟁에 응답
- 항소(Appeal) 개시 후 상대방에게 10분간 채팅 협의 기회 부여
- 합의 미달 시 Binance 고객지원팀 중재
- 분쟁 처리 수수료: 4번째 분쟁부터 부과 (처음 3회 무료)

> 출처: [Binance P2P Appeal Handling Rules](https://www.binance.com/en/support/faq/binance-p2p-appeal-handling-rules-360041839052)

### 4.6 경쟁사 비교 (환불/분쟁)

| 항목 | Binance Pay | BitPay | Coinbase Commerce | Crypto.com Pay | PayPal Crypto | Stripe Stablecoin |
|------|:-----------:|:------:|:-----------------:|:--------------:|:-------------:|:-----------------:|
| 환불 지원 | API + 대시보드 | API + 대시보드 | 스마트 컨트랙트 | API + 대시보드 | PayPal 시스템 | Stripe 시스템 |
| 환불 유형 | 전액/부분 | 전액/부분 | 전액/부분 | 전액/부분 | 전액/부분 | 전액/부분 |
| 환불 통화 | 정산 통화(USDT) | 동일 암호화폐 | USDC(온체인) | 고객 선호 설정 가능 | USD | 원래 결제 통화 |
| 차지백 보호 | **없음** | BitPay Guarantee | 에스크로 기반 | 없음 | **PayPal 차지백** | **Stripe 차지백** |
| 분쟁 해결 | 가맹점 재량 + Binance 중재 | BitPay 중재 | 캡처 만료 전 자동 환불 | Crypto.com 중재 | **Purchase Protection** | **Stripe 분쟁 시스템** |
| 구매자 보호 | **없음** | 제한적 | 에스크로 | 제한적 | **있음** | **있음** |

---

## 5. 시장 현황 및 경쟁 환경

### 5.1 시장 규모 및 트렌드

**글로벌 암호화폐 결제 시장 규모:**

| 구분 | 규모 | CAGR | 출처 |
|------|------|------|------|
| 암호화폐 결제 앱 시장 | USD 623.92M (2025) | 16.8% (2026-2035) | [Research Nester](https://www.researchnester.com/reports/cryptocurrency-payment-apps-market/6523) |
| 크립토 결제 게이트웨이 시장 | USD 2.0B (2025) | 18.7% (2026-2030) | [GII Research](https://www.giiresearch.com/report/tbrc1980837-crypto-payment-gateway-global-market-report.html) |
| 크립토 결제 게이트웨이 전망 | USD 4.74B (2030) | - | [GII Research](https://www.giiresearch.com/report/tbrc1980837-crypto-payment-gateway-global-market-report.html) |

> **교차 검증 주석**: 시장 규모 추정치는 리서치 기관마다 정의 범위(앱 vs 게이트웨이 vs 전체 결제)가 다르므로 직접 비교 시 주의 필요.

**핵심 트렌드:**

1. **스테이블코인 결제의 부상**: 2025년 Binance Pay B2C 결제의 98% 이상이 스테이블코인으로 처리 ([CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/)). 결제 시장이 변동성 자산에서 안정 자산 기반으로 전환 중.
2. **두 가지 시장 모델 분화**: (a) 전통 게이트웨이 모델(BitPay, Coinbase)--크립토 수취 후 법정화폐 전환, (b) 생태계 내장형 모델(Binance Pay, Crypto.com Pay)--거래소 생태계 내 크립토-크립토 정산.
3. **전통 결제 기업의 크립토 확장**: PayPal, Stripe가 기존 인프라에 암호화폐 결제를 자연스럽게 통합하여, 별도 크립토 게이트웨이의 존재 의의를 위협.
4. **온체인 프로토콜의 등장**: Coinbase Commerce가 Base L2 기반 오픈소스 프로토콜로 전환, Solana Pay의 기관 통합 가속.

### 5.2 경쟁 구도 및 포지셔닝

암호화폐 결제 시장은 2026년 현재 세 가지 진영으로 분화되어 있다:

| 진영 | 대표 서비스 | 특징 |
|------|-------------|------|
| **거래소 생태계 내장형** | Binance Pay, Crypto.com Pay | 자사 거래소 사용자 기반 활용, 크립토-크립토 정산 중심 |
| **전통 게이트웨이형** | BitPay, CoinGate, NOWPayments | 크립토 수취 후 법정화폐 전환, 기존 사업자 친화적 |
| **전통 결제 확장형 / 온체인 프로토콜형** | PayPal Crypto, Stripe Stablecoin, Coinbase Commerce(Base), Solana Pay | 기존 결제 인프라에 크립토 통합 또는 탈중앙화 결제 레일 구축 |

**Binance Pay의 포지션**: 우측 하단 -- 암호화폐 네이티브 깊이는 최상이나 법정화폐 정산 용이성이 최하. 거래량/생태계 규모는 최대이나 주요 고소득 시장(미국, 영국) 미진출.

### 5.3 핵심 경쟁사 비교표

**경쟁력 스코어카드 (10점 만점)**

| 평가 항목 | Binance Pay | Coinbase Commerce | BitPay | Crypto.com Pay | PayPal Crypto | Stripe Stablecoin |
|-----------|:-----------:|:-----------------:|:------:|:--------------:|:-------------:|:-----------------:|
| 수수료 경쟁력 | 7 | 7 | 4 | 10 | 7 | 6 |
| 정산 속도 | **10** | **10** | 4 | 6 | 8 | 8 |
| 법정화폐 정산 | **2** | 5 | **10** | 8 | **10** | **10** |
| 환불/분쟁 해결 | 6 | 9 | 8 | 7 | **10** | **10** |
| 지원 암호화폐 | **10** | 9 | 7 | 4 | 8 | 2 |
| 통합 용이성 | 6 | 8 | 6 | 7 | **10** | **10** |
| 사용자 기반 | **10** | 7 | 5 | 7 | **10** | 8 |
| 규제 안정성 | 5 | 8 | 8 | 7 | **10** | **10** |
| **종합 평균** | **7.0** | **7.9** | **6.5** | **7.0** | **9.1** | **8.3** |

> 출처: 02_경쟁사 분석 보고서 기반 재구성. PayPal Crypto(9.1)가 종합 최고점이나 미국 한정이라는 지역 제한이 있어, 글로벌 시장에서 Binance Pay와 직접 충돌은 당분간 제한적이다.

---

## 6. 비즈니스 모델 및 기술 아키텍처

### 6.1 수익 구조

| 분류 | 설명 | 2025년 추정 매출 |
|------|------|------------------|
| **1차 수익원** | Merchant Discount Rate (MDR) 1% | ~USD 110M (Merchant 거래량 ~USD 11B 기준) |
| **2차 수익원** | Payout 수수료 0.80% (최대 USD 5/건) | 미공개 |
| **3차 수익원** | FX 스프레드 -- 암호화폐 간 자동 환전 시 내재 마진 (추정 0.1~0.5%) | 미공개 |
| **4차 수익원** | 생태계 유입 효과 -- Binance 거래소 거래 수수료 간접 기여 | 간접적 |

**수익 역산 분석:**
연간 거래량(USD 121B)과 MDR(1%)로 단순 계산하면 이론상 수수료 수입은 USD 1.21B이어야 하나, 실제 매출은 약 USD 110M이다. 이는 **거래량의 약 90%가 수수료 무료인 P2P 전송**이며, Merchant 결제 비중은 전체의 약 9~10%에 불과한 것으로 추정된다.

**Binance 전체 수익 내 비중:** Binance Pay 매출(USD 110M)은 Binance 전체 매출(~USD 17.5B)의 약 0.6%에 불과하다. Binance Pay는 **독립 수익 사업이 아닌 생태계 확장의 전략적 도구**로서의 가치가 더 크다.

> 출처: [Business of Apps](https://www.businessofapps.com/data/binance-statistics/)

### 6.2 기술 스택 (Binance Ledger, API 등)

**백엔드 핵심 기술 (확인됨 + 추정):**

| 기술 | 용도 | 신뢰도 |
|------|------|--------|
| Java / Spring Boot | 핵심 서비스 (결제 엔진) | 확인됨 (채용공고) |
| RocksDB + Raft 합의 | Binance Ledger Raft Domain (고성능 쓰기) | 확인됨 (기술 블로그) |
| 관계형 DB | Binance Ledger View Domain (외부 조회) | 확인됨 |
| Kafka / RabbitMQ | 메시지 큐 / 이벤트 스트리밍 | 확인됨 (채용공고) |
| Redis | 캐시 / 세션 관리 | 확인됨 |
| Docker / Kubernetes | 컨테이너화 / 오케스트레이션 | 확인됨 |
| AWS / Alibaba Cloud | 클라우드 인프라 | 추정 (채용공고) |

**보안 체계:**
- API 인증: HMAC-SHA512 서명 + 타임스탬프 1초 윈도우 + 32자 Nonce
- 사용자 인증: 2FA (Google Authenticator, SMS, Passkey)
- KYC 3단계: Intermediate / Advanced / Advanced Pro
- AML 이중 레이어: AI + 인간 분석가
- 컴플라이언스 투자: 2025년 3분기 기준 누적 USD 1.2B

### 6.3 Merchant API 아키텍처

```
+---------------------------+
|      Merchant Server      |
+---------------------------+
   |         |         |
Create    Query     Refund
Order V2  Order V2  Order
   |         |         |
   v         v         v
+-----------------------------------+
|     Binance Pay API Gateway        |
|  Base URL: bpay.binanceapi.com     |
+-----------------------------------+
|  HMAC-SHA512 Authentication        |
|  Timestamp + Nonce + Body           |
+-----------------------------------+
   |              |
   v              v
+----------------+  +------------------+
| Order Engine   |  | Webhook Engine   |
| (주문 처리)    |  | (최대 6회 재시도) |
+----------------+  +------------------+
   |              |
   v              v
+-----------------------------------+
|      Binance Ledger System         |
|   (내부 원장 - 오프체인 정산)       |
+-----------------------------------+
   |
   v
+-----------------------------------+
|      FX Engine (자동 환전)          |
|   고객 결제 통화 -> 가맹점 정산 통화  |
+-----------------------------------+
```

**주문 생명주기 (9개 상태):**

```
[INITIAL] --> [PENDING] --> [PAID] --> [REFUNDING] --> [REFUNDED/FULL_REFUNDED]
    |             |
    v             v
 [EXPIRED]    [CANCELED]
                  |
                  v
               [ERROR]
```

**통합 방식 3가지:**

| 방식 | 개발 난이도 | 적합 대상 |
|------|-------------|-----------|
| Hosted Checkout Page | 낮음 | 빠른 통합이 필요한 가맹점 |
| Payment Links | 제로 (코딩 불필요) | 소규모 사업자, 프리랜서 |
| Native APIs (C2B) | 높음 | 대규모 이커머스, 앱 서비스 |

> 출처: [Binance Developers - Merchant API](https://developers.binance.com/docs/binance-pay/introduction), [Binance Merchant Docs](https://merchant.binance.com/en/docs/getting-started)

---

## 7. 사용자 경험 및 피드백

### 7.1 소비자 관점

**주요 리뷰 플랫폼 평점:**

| 플랫폼 | 평점 | 비고 |
|--------|------|------|
| Trustpilot | 1.4~1.5/5 (5,700건+) | 불만 사용자 집중 유입, 선택 편향 가능성 |
| App Store | 4.7/5 | Binance 앱 전체 평가 |
| Google Play | 4.6/5 | Binance 앱 전체 평가 |
| Capterra | 4.5/5 | 비즈니스 소프트웨어 관점 |

> **교차 검증 주석**: Trustpilot(1.4/5)과 App Store(4.7/5) 간 극단적 괴리는 각 플랫폼의 리뷰 편향 특성을 반영한다. 실제 만족도는 두 극단 사이에 위치할 것으로 추정된다.

**호평 Top 5:**
1. 즉시 처리 속도 (오프체인) -- "결제가 즉시 처리되며 대기 시간이 없다"
2. P2P 무료 송금 -- 수수료 0%, 가스비 0%
3. 다양한 암호화폐 지원 -- 300종+(P2P), 50종+(가맹점)
4. QR 코드 결제 편의성
5. Binance 앱 내 통합 (별도 앱 설치 불필요)

**불만 Top 5:**
1. 고객 지원 품질 -- 봇 응답 루프, 에스컬레이션 무응답, 장기 지연 (가중 점수 10/10)
2. 계정 동결/잠금 -- 이유 불분명, 60일+ 장기화 (9/10)
3. Binance 계정 필수 -- 비사용자 결제 불가 (8/10)
4. 규제 제한 지역 서비스 차단 (8/10)
5. P2P 사기 -- 가짜 결제 증명, 신원 도용 (7/10)

### 7.2 가맹점 관점

**호평:**
- 통합 속도 양호 ("예상보다 빠르게 통합 완료")
- Hosted Checkout 편의성 (코딩 없이 즉시 결제 수용)
- 자동 환전 정산 (고객 결제 코인과 무관하게 선호 통화로 정산)

**불만 (심각도순):**
1. **법정화폐 직접 정산 불가** (매우 높음) -- "USDT로 정산 후 별도 환전 필요"
2. **KYB 인증 지연** (높음) -- "한 달간 시도했으나 수락되지 않았다"
3. **구독/반복 결제 미지원** (높음) -- SaaS, 멤버십 사업자에게 치명적
4. **플러그인 지원 제한** (중간) -- Shopify, WooCommerce 직접 플러그인 경쟁사 대비 부족
5. **Payout 수수료 신설** (중간) -- 2024년 12월 무료에서 0.8% 유료 전환

### 7.3 개발자 관점

**API 품질 평가:**
- 구조: RESTful, 표준적. 3가지 통합 방식 제공
- 인증: HMAC-SHA512 기반, 보안 수준 양호
- 문제점: 에러 코드 문서화 부족, Webhook 서명 검증 실패 이슈 반복 보고

**주요 개발자 Pain Points:**
1. 서버사이드 공식 SDK 부족 (iOS/Android만 제공, Node.js/Python/Go 등 미제공)
2. Webhook 신뢰성 -- 재시도 6회 소진 후 알림 누락, 서명 검증 로직 불명확
3. KYB 없이 Sandbox 테스트 불가 -- 경쟁사(NOWPayments: KYC 불필요, Stripe: 기존 계정 활용) 대비 열위
4. 문서 분산 -- merchant.binance.com과 developers.binance.com 이중 포털 혼란

**경쟁사 대비 개발자 경험:**

| 항목 | Binance Pay | NOWPayments | Stripe Stablecoin | Coinbase Commerce |
|------|:-----------:|:-----------:|:-----------------:|:-----------------:|
| 공식 SDK 언어 수 | 2 (iOS, Android) | 10종+ | Stripe SDK 전체 | 오픈소스 프로토콜 |
| 이커머스 플러그인 | 제한적 | 풍부 | Stripe 생태계 전체 | Shopify 기본 |
| KYB 없이 테스트 | 불가 | 가능 | 기존 계정 활용 | 기본 KYC만 |
| 문서 품질 | 보통 | 양호 | 최상 | 양호 |

---

## 8. SWOT 분석

| **강점 (Strengths)** | **약점 (Weaknesses)** |
|---|---|
| 3억 명+ Binance 사용자 기반, 2,000만 가맹점 | 법정화폐 직접 정산 불가 (최대 구조적 약점) |
| 오프체인 즉시 정산 + 가스비 제로 (10,000+ TPS) | 미국/영국 등 70개국 이상 서비스 제한 |
| 300종 이상 암호화폐 지원, 1% 고정 MDR | Binance 계정 필수 (폐쇄적 생태계) |
| P2P 무료 송금 + Merchant 결제 통합 앱 | 구독/반복 결제 미지원 |
| Binance 생태계(거래소, Earn, Card, BNB Chain) 시너지 | 고객 지원 품질 심각한 수준 (Trustpilot 1.4/5) |
| B2C 결제 98%가 스테이블코인 (안정적 정산 가치) | 서버사이드 SDK 부족, 문서 분산, Webhook 이슈 |

| **기회 (Opportunities)** | **위협 (Threats)** |
|---|---|
| 신흥국(동남아, 아프리카, 남미) 금융 포용 수요 급증 | PayPal/Stripe의 크립토 결제 기본 통합 (4억+ PayPal 사용자) |
| 법정화폐 정산 기능 추가 시 독보적 포지션 가능 | 주요국 규제 강화 (스테이블코인 규제, MiCA 등) |
| 스테이블코인 결제 대중화 추세 | CBDC 출시로 인한 암호화폐 결제 수요 잠식 |
| B2B 국경 간 결제 시장 확장 가능성 | Coinbase Commerce 오픈소스 프로토콜의 생태계 확장 |
| CBDC 브릿지 역할 가능성 | 보안 사고/규제 제재 발생 시 Binance 브랜드 리스크 파급 |
| 가맹점 네트워크 확대 (2,000만 -> 추가 성장) | 비수탁형(Solana Pay, NOWPayments) 서비스의 수수료 경쟁력 |

---

## 9. 전략적 시사점 및 권고사항

### 핵심 발견 5가지

1. **"생태계 전략 도구"로서의 본질**: Binance Pay는 연간 USD 110M 매출(Binance 전체의 0.6%)의 독립 수익 사업이 아니라, 3억 명 사용자를 활성화하고 자금을 Binance 생태계 내에 체류시키는 전략적 도구이다. 법정화폐 직접 정산이 불가한 것도 이 전략의 의도적 결과일 수 있다.

2. **"속도는 최고, 생태계는 폐쇄적"**: 오프체인 즉시 처리와 제로 가스비는 기술적으로 독보적이나, Binance 계정 필수라는 폐쇄적 구조가 확장을 제약한다. PayPal/Stripe가 기존 인프라에 크립토를 "자연스럽게 통합"하는 개방형 접근과 대조적이다.

3. **법정화폐 정산 간극이 전통 사업자 도입의 최대 장벽**: 회계/세무 보고가 법정화폐 기준인 전통 사업자에게, USDT 정산 후 수동 환전이 필요한 추가 단계는 운영 부담과 규제 리스크를 동시에 초래한다.

4. **규제 환경이 이중 제약**: 미국/영국 미진출(시장 접근 제약)과 스테이블코인(USDT) 규제 강화(핵심 정산 통화 위협)가 동시에 작용하는 이중 병목 구조이다.

5. **P2P의 양면성**: P2P 무료 즉시 송금은 최고 만족도 기능이자 사용자 유입의 핵심 동력이지만, 동시에 P2P 사기(가짜 결제 증명, 신원 도용)는 가장 심각한 보안 이슈이다.

### 기회 요인

- **신흥국 시장 선점**: 은행 인프라가 부족한 동남아, 아프리카, 남미에서 스테이블코인 결제 수요가 급증하고 있으며, Binance의 기존 사용자 기반이 이 시장에서 강점으로 작용
- **법정화폐 정산 추가 시 "게임 체인저"**: 300종 암호화폐 지원 + 즉시 정산 + 법정화폐 은행 입금을 모두 겸비한 서비스는 현재 부재. Binance가 이를 추가하면 독보적 포지션 확보 가능
- **B2B 국경 간 결제**: 기업 간 무역 정산에서 스테이블코인 활용 수요가 증가하고 있으며, Binance의 글로벌 네트워크와 즉시 정산 인프라가 경쟁력

### 위협 요인

- **PayPal/Stripe의 구조적 위협**: 4억 사용자의 PayPal과 수백만 가맹점의 Stripe가 크립토 결제를 기본 통합하면, "크립토 결제"가 별도 카테고리가 아닌 기존 결제 인프라의 일부로 흡수될 가능성. 장기적으로 전용 크립토 게이트웨이의 존재 의의 약화
- **CBDC 경쟁**: 주요국 CBDC 출시 시, 스테이블코인 기반 결제 수요의 일부를 잠식할 가능성
- **Coinbase Commerce의 오픈소스 전략**: Shopify 수백만 가맹점에 기본 제공되는 오픈소스 프로토콜은 Binance Pay의 폐쇄적 생태계와 정반대 접근으로, 가맹점 네트워크 확장에서 구조적 우위

### 권고사항

| 우선순위 | 권고 | 영향도 | 실현 가능성 |
|----------|------|--------|-------------|
| 1 | **고객 지원 체계 전면 개편** -- 인간 상담원 접근 경로 확보, 계정 동결 SLA 명시, 에스컬레이션 투명성 확보 | 매우 높음 | 중간 |
| 2 | **법정화폐 직접 정산 기능 추가** -- 채널 파트너가 아닌 자체 법정화폐 은행 입금 지원 | 매우 높음 | 낮음 (규제 허들) |
| 3 | **구독/반복 결제 기능 출시** -- SaaS, 멤버십 사업자 온보딩의 전제 조건 | 높음 | 높음 |
| 4 | **이커머스 플러그인 확대** -- Shopify, WooCommerce, Magento 공식 플러그인 지원 | 높음 | 높음 |
| 5 | **서버사이드 SDK 및 문서 통합** -- Node.js, Python, PHP, Go 공식 SDK + 단일 문서 포털 | 중간 | 높음 |
| 6 | **게스트 체크아웃 도입** -- Binance 계정 없이 외부 지갑으로 결제 허용 | 높음 | 낮음 (생태계 전략 충돌) |
| 7 | **환불 시 원래 결제 코인 반환 옵션** -- 고객 선택에 따라 원래 암호화폐로 환불 가능 | 중간 | 중간 |
| 8 | **Sandbox 환경 개방** -- KYB 없이 개발자 테스트 가능한 환경 제공 | 중간 | 높음 |

---

## 데이터 신뢰도 평가

| 분석 영역 | 신뢰도 | 주요 한계 |
|-----------|--------|-----------|
| 시장 규모 및 트렌드 | 중간~높음 | 리서치 기관별 정의 범위 상이, 시장 규모 추정치 2배 이상 편차 존재 |
| 핵심 수치 (거래량, 사용자 수) | 높음 | CoinLaw, Business of Apps 등 복수 소스 교차 확인됨. 다만 "가맹점 2,000만" 수치는 정의 범위 확대에 기인한 것으로 추정 |
| 수수료 구조 | 높음 | 공식 FAQ 및 문서 기반. FX 스프레드만 비공개(추정 0.1~0.5%) |
| 경쟁사 비교 | 높음 | 각 서비스 공식 문서 + 2026년 비교 리뷰 다수 참조 |
| 기술 아키텍처 | 중간~높음 | Binance Ledger, API 인증은 확인됨. FX Engine, 일부 인프라는 채용공고/기술 블로그 기반 추정 |
| 사용자 인사이트 | 중간 | Trustpilot(1.4/5)과 App Store(4.7/5) 극단적 괴리. Binance Pay 단독 리뷰 분리 불가. 구조적 패턴 도출에 초점 |
| 수익 역산 분석 | 중간 | Business of Apps의 USD 110M 매출 수치 기반 역산. P2P vs Merchant 비중은 추정 |
| 비즈니스 모델 전략적 해석 | 중간 | 공개 데이터 기반 추론. Binance 내부 전략은 비공개 |

---

## 부록: 출처 목록

### 공식 소스
- [Binance Pay](https://pay.binance.com/en)
- [Binance Merchant Docs](https://merchant.binance.com/en/docs/getting-started)
- [Binance Developers - Merchant API](https://developers.binance.com/docs/binance-pay/introduction)
- [Binance Pay Fees FAQ](https://www.binance.com/en/support/faq/binance-pay-fees-6ff1944867e54b9a9576bce3109c7f7a)
- [Binance Blog - Binance Ledger](https://www.binance.com/en/blog/tech/how-binance-ledger-powers-your-binance-experience-5409682424466769892)
- [Binance P2P Appeal Handling Rules](https://www.binance.com/en/support/faq/binance-p2p-appeal-handling-rules-360041839052)

### 통계 및 시장 데이터
- [CoinLaw - Crypto Payment Gateways Statistics](https://coinlaw.io/crypto-payment-gateways-statistics/)
- [CoinLaw - Binance Exchange Statistics](https://coinlaw.io/binance-exchange-statistics/)
- [Business of Apps - Binance Statistics](https://www.businessofapps.com/data/binance-statistics/)
- [Research Nester - Cryptocurrency Payment Apps Market](https://www.researchnester.com/reports/cryptocurrency-payment-apps-market/6523)
- [GII Research - Crypto Payment Gateway Global Market Report](https://www.giiresearch.com/report/tbrc1980837-crypto-payment-gateway-global-market-report.html)
- [Incrypted - Binance 2025 Report](https://incrypted.com/en/binance-reported-for-2025-34t-in-trades-and-300m-users/)
- [Airdrops.io - Binance Pay 20M Merchants](https://airdrops.io/blog/binance-pay-20-million-merchants-stablecoin-payments/)

### 경쟁사 비교
- [WestAfricaTradeHub - 2026 Buyer's Guide](https://westafricatradehub.com/crypto/best-crypto-payment-gateway-2026-buyers-guide-to-fees-settlement-and-coin-support/)
- [Aurpay - Crypto Payment Gateway Comparison 2026](https://aurpay.net/aurspace/crypto-payment-gateway-comparison-2026/)
- [VentureBurn - Best Crypto Payment Gateway 2026](https://ventureburn.com/best-crypto-payment-gateway/)
- [Paybis - BitPay Fees vs Alternatives 2026](https://paybis.com/blog/bitpay-pricing-fees-breakdown/)
- [NOWPayments vs Binance Pay](https://nowpayments.io/blog/nowpayments-vs-binance-pay)
- [BitPay Pricing](https://www.bitpay.com/pricing)
- [Coinbase Commerce Onchain Protocol Deep Dive](https://www.coinbase.com/blog/coinbase-commerce-onchain-payment-protocol-deep-dive)
- [Stripe Stablecoin Payments Docs](https://docs.stripe.com/payments/stablecoin-payments)

### 사용자 리뷰
- [Trustpilot - Binance Reviews](https://www.trustpilot.com/review/binance.com) (5,700건+)
- [Capterra - Binance Reviews](https://www.capterra.com/p/252490/Binance/reviews/)
- [G2 - Binance Reviews](https://www.g2.com/products/binance/reviews)
- [Binance Developer Community Forum](https://dev.binance.vision/)

### 기술 참조
- [Binance Pay Create Order V2 API](https://developers.binance.com/docs/binance-pay/api-order-create-v2)
- [Binance Pay Refund Order API](https://developers.binance.com/docs/binance-pay/api-order-refund)
- [Binance Pay Batch Payout API](https://developers.binance.com/docs/binance-pay/api-payout)
- [Binance Pay Order Notification (Webhook)](https://developers.binance.com/docs/binance-pay/order-notification)

---

*본 보고서는 2026년 4월 15일 기준 공개 자료를 바탕으로 작성되었으며, 시장 상황 및 규제 환경은 수시로 변동될 수 있습니다. 데이터 신뢰도 평가표를 참조하여 각 분석 영역의 한계를 감안하시기 바랍니다.*
