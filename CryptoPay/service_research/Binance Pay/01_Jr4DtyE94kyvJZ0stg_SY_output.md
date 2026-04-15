# 시장 현황 분석 -- Binance Pay

## 분석 개요

- **분석 대상**: Binance Pay (바이낸스 페이) -- Binance 거래소 기반 암호화폐 결제 서비스
- **분석 일시**: 2026-04-14
- **서비스 URL**: https://pay.binance.com/en
- **주요 참조 소스**:
  - Binance 공식 문서 및 개발자 포털 (merchant.binance.com, developers.binance.com)
  - CoinLaw 통계 리포트 (coinlaw.io)
  - Business of Apps -- Binance Statistics (businessofapps.com)
  - Research and Markets / Research Nester 시장 보고서
  - NOWPayments, BitPay, Coinbase Commerce 비교 자료
  - 각종 암호화폐 미디어 (incrypted.com, cryptonomist.ch 등)

---

## 1. 서비스 개요

Binance Pay는 세계 최대 암호화폐 거래소인 Binance가 운영하는 **비수탁형(contactless) 암호화폐 결제 서비스**이다. 2021년 출시 이후, Binance 생태계 내 사용자 간 P2P 송금과 가맹점(Merchant) 결제를 모두 지원하는 통합 결제 플랫폼으로 성장하였다.

### 핵심 특징

- **QR 코드, Pay ID, 이메일/전화번호, 사용자명** 기반 결제 지원
- **300종 이상**의 암호화폐 지원 (결제 수단으로서)
- **오프체인(off-chain) 즉시 정산**: 블록체인 가스비 없이 Binance 내부에서 즉시 이체
- **P2P 개인 간 송금** + **Merchant 가맹점 결제** 이중 구조
- Binance 앱 내장형 서비스로, 별도 앱 설치 불필요

---

## 2. 암호화폐 결제 시장 규모

### 글로벌 시장 규모 및 성장률

| 구분 | 규모 | 기준 연도 | CAGR | 출처 |
|------|------|-----------|------|------|
| 암호화폐 결제 앱 시장 | USD 623.92M | 2025 | 16.8% (2026-2035) | [Research Nester](https://www.researchnester.com/reports/cryptocurrency-payment-apps-market/6523) |
| 암호화폐 결제 앱 시장 (대체 추정) | USD 1.25B | 2025 | 20.5% (2025-2026) | [GII Research](https://www.giiresearch.com/report/tbrc1980840-cryptocurrency-payment-apps-global-market-report.html) |
| 크립토 결제 게이트웨이 시장 | USD 2.0B | 2025 | 19.0% (2025-2026) | [GII Research](https://www.giiresearch.com/report/tbrc1980837-crypto-payment-gateway-global-market-report.html) |
| 크립토 결제 게이트웨이 시장 (전망) | USD 4.74B | 2030 | 18.7% (2026-2030) | [GII Research](https://www.giiresearch.com/report/tbrc1980837-crypto-payment-gateway-global-market-report.html) |
| 글로벌 크립토 결제 산업 전체 | -- | -- | 14.2% (2024-2030) | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |

> **참고**: 시장 규모 추정치는 리서치 기관마다 정의 범위(앱 vs 게이트웨이 vs 전체 결제)가 다르므로 직접 비교 시 주의 필요.

### 시장 성장 동인

- **스테이블코인 결제 확산**: 2025년 Binance Pay B2C 결제의 98% 이상이 스테이블코인으로 처리 ([CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/))
- **신흥국 금융 포용**: 은행 계좌 없이도 암호화폐 지갑으로 결제 가능
- **기업 도입 가속화**: 전통 결제 대비 낮은 수수료, 즉시 정산, 국경 없는 결제의 장점
- **규제 명확화**: MiCA(EU), 일본 자금결제법 등 주요국 규제 프레임워크 정비

### 시장 저해 요인

- **가격 변동성**: 비스테이블코인의 가격 변동이 가맹점 리스크 유발
- **규제 불확실성**: 미국, 영국 등 주요 시장에서의 서비스 제한
- **사용자 경험**: 일반 소비자에게 암호화폐 결제는 여전히 진입 장벽 존재
- **보안 리스크**: 해킹, 사기 등 암호화폐 고유의 보안 이슈

---

## 3. Binance Pay 시장 내 포지셔닝

### 핵심 지표

| 지표 | 수치 | 기준 시점 | 출처 |
|------|------|-----------|------|
| 누적 거래량 | USD 280B 초과 | 출시 이후 누적 | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |
| 연간 거래량 | USD 121B | 2025년 (2026년 2월 기준) | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |
| 누적 거래 건수 | 13.6억 건 | 2026년 2월 기준 | [CoinLaw](https://coinlaw.io/crypto-payment-gateways-statistics/) |
| 거래 수수료 매출 | 약 USD 110M | 2025년 | [Business of Apps](https://www.businessofapps.com/data/binance-statistics/) |
| Binance 전체 등록 사용자 | 3억 명 초과 | 2025년 말 | [Incrypted](https://incrypted.com/en/binance-reported-for-2025-34t-in-trades-and-300m-users/) |
| Binance 거래소 시장 점유율 | 39.2% | 2026년 초 | [CoinLaw](https://coinlaw.io/binance-exchange-statistics/) |

### 경쟁사 비교

| 항목 | Binance Pay | BitPay | Coinbase Commerce |
|------|-------------|--------|-------------------|
| **설립 연도** | 2021 | 2011 | 2018 |
| **지원 암호화폐** | 300종 이상 | 100종 이상 | 주요 토큰 위주 |
| **수수료 (가맹점)** | 1% MDR | 1-2% (거래량 기반) | 기본 무료 (환전 수수료 별도) |
| **정산 방식** | 크립토 정산 (USDT 등) | 법정화폐 은행 입금 | 크립토 보유 또는 법정화폐 전환 |
| **정산 속도** | 즉시 (오프체인) | 1-2 영업일 | 즉시~1일 |
| **법정화폐 직접 입금** | 불가 (거래소 환전 필요) | 가능 | 가능 (Base L2 경유) |
| **주요 장점** | 대규모 사용자 기반, 즉시 정산 | 오랜 실적, 법정화폐 직접 정산 | 브랜드 신뢰도, 무료 기본 처리 |
| **주요 약점** | 규제 리스크, 법정화폐 직접 정산 불가 | 높은 수수료 | 제한된 토큰 지원 |

> 출처: [WestAfricaTradeHub](https://westafricatradehub.com/crypto/best-crypto-payment-gateway-2026-buyers-guide-to-fees-settlement-and-coin-support/), [Aurpay](https://aurpay.net/aurspace/crypto-payment-gateway-comparison-2026/), [VentureBurn](https://ventureburn.com/best-crypto-payment-gateway/)

---

## 4. 결제(Payment) 프로세스

### 4.1 P2P 결제 (개인 간 송금)

P2P 결제는 Binance 사용자 간 직접 암호화폐를 전송하는 방식이다.

**결제 흐름:**
1. 송금자가 Binance 앱에서 상대방의 Pay ID, 이메일, 전화번호, 또는 QR 코드를 입력
2. 전송할 암호화폐 종류와 금액 선택
3. 확인 후 즉시 상대방 Binance 지갑으로 이체 완료

**주요 특징:**
- **수수료**: 무료 (Binance 사용자 간 P2P 전송 시 수수료 없음)
- **처리 속도**: 즉시 (오프체인 처리)
- **가스비**: 없음 (블록체인 트랜잭션이 아닌 Binance 내부 원장 처리)
- **지원 암호화폐**: 300종 이상

### 4.2 Merchant 결제 (가맹점 결제)

가맹점 결제는 사업자가 Binance Pay를 통해 고객으로부터 암호화폐 결제를 수취하는 방식이다.

**결제 흐름 (Hosted Checkout):**
1. 가맹점이 Create Order API를 호출하여 주문 생성
2. API 응답으로 `checkoutURL` 수신
3. 고객을 Binance Web Checkout Page로 리다이렉트
4. 고객이 QR 코드 스캔, Binance 앱 열기, 또는 웹 로그인으로 결제
5. 고객이 50종 이상의 암호화폐 중 결제 수단 선택
6. 결제 완료 후 가맹점에 Webhook 콜백 발송

> 출처: [Binance Merchant Docs - Hosted Checkout](https://merchant.binance.com/en/docs/functionalities/single-payment/hosted-checkout-page)

**통합 방식 3가지:**

| 방식 | 설명 | 적합 대상 |
|------|------|-----------|
| **Hosted Checkout Page** | Binance가 호스팅하는 결제 페이지로 리다이렉트 | 빠른 통합이 필요한 가맹점 |
| **Payment Links** | 코딩 없이 결제 링크 생성 | 소규모 사업자, 프리랜서 |
| **Native APIs** | 직접 API 통합으로 결제 경험 커스터마이즈 | 대규모 이커머스, 앱 서비스 |

> 출처: [Binance Merchant - Payment APIs](https://merchant.binance.com/en/products/payment-apis)

**결제 시나리오:**
- **온라인 결제**: 이커머스, 구독 서비스, 디지털 상품
- **오프라인 결제**: 매장 내 QR 코드 스캔
- **인앱 결제**: 딥링크 기반 결제 흐름

### 4.3 지원 암호화폐 및 결제 수단

- **고객 결제 가능 암호화폐**: 50종 이상 (BTC, ETH, BNB, USDT, USDC, SOL, XRP 등)
- **가맹점 수취 가능 화폐**: 법정화폐(USD, EUR 등) 단위로 주문 생성 가능하되, 실제 수취는 USDT 등 크립토로 정산
- **결제 UI**: 고객이 자유롭게 보유 암호화폐 중 결제 수단 선택

### 4.4 수수료 구조

| 수수료 항목 | 요율 | 비고 |
|-------------|------|------|
| P2P 송금 수수료 | 0% | Binance 사용자 간 무료 |
| 가맹점 결제 수수료 (MDR) | 1.0% | Merchant Discount Rate |
| Payout 수수료 | 0.80% (최대 USD 5) | 2024년 12월 1일부터 적용 |
| 블록체인 가스비 | 0% | 오프체인 정산으로 불필요 |

> 출처: [Binance Pay Fees FAQ](https://www.binance.com/en/support/faq/binance-pay-fees-6ff1944867e54b9a9576bce3109c7f7a)

---

## 5. 정산(Settlement) 프로세스

### 5.1 정산 방식

Binance Pay는 **오프체인 즉시 정산(off-chain instant settlement)** 방식을 사용한다. 이는 블록체인 네트워크를 거치지 않고 Binance 내부 원장에서 처리되므로, 가스비가 발생하지 않으며 처리 속도가 즉각적이다.

### 5.2 정산 통화

- **기본 정산 통화**: USDT (테더) -- 가맹점 Payout API는 USDT 정산을 기본 지원
- **가맹점 설정 가능**: 가맹점이 정산 설정에서 선호 통화를 정의하면, 고객이 어떤 암호화폐로 결제하든 해당 통화로 정산
- **법정화폐 직접 은행 입금**: 불가 -- 법정화폐로 출금하려면 Binance 거래소에서 별도로 크립토를 매도 후 법정화폐로 출금해야 함

> 출처: [Binance Merchant Docs - Payout](https://merchant.binance.com/en/docs/functionalities/payout)

### 5.3 정산 주기

- **즉시 정산**: 결제 완료와 동시에 가맹점의 Binance 지갑에 정산 금액 입금
- **별도 정산 주기 없음**: 전통적인 T+1, T+2 정산 주기가 아닌 실시간 처리
- **채널 파트너를 통한 법정화폐 정산**: Binance Pay 채널 파트너사를 통해 가맹점이 법정화폐 또는 크립토로 정산 수취 방식 선택 가능

### 5.4 환전 정책

| 시나리오 | 처리 방식 |
|----------|-----------|
| 고객이 BTC로 결제, 가맹점이 USDT 정산 선호 | Binance가 자동으로 BTC를 USDT로 전환 후 정산 |
| 고객이 ETH로 결제, 가맹점이 법정화폐 원함 | USDT로 정산 후 가맹점이 수동으로 거래소에서 환전 |
| 법정화폐 단위 주문 생성 (예: USD 100) | 고객은 50종 이상 크립토 중 선택, 가맹점은 USDT로 수취 |

### 5.5 정산 프로세스 흐름도

```
[고객] ---(암호화폐 결제)---> [Binance Pay 시스템]
                                    |
                          [자동 환전 (필요 시)]
                                    |
                    [가맹점 Binance 지갑에 즉시 입금]
                                    |
                        (선택) [Binance 거래소]
                                    |
                        (선택) [법정화폐 출금]
```

---

## 6. 환불(Refund) 프로세스

### 6.1 환불 가능 여부

Binance Pay Merchant 결제에서는 **환불이 가능**하다. 가맹점이 Merchant Management Platform 또는 Refund Order API를 통해 환불을 처리할 수 있다.

### 6.2 환불 유형

| 유형 | 설명 |
|------|------|
| **전액 환불 (Full Refund)** | 주문 전체 금액을 고객에게 반환 |
| **부분 환불 (Partial Refund)** | 주문 금액의 일부만 반환. 여러 차례 부분 환불 가능 (원래 주문 금액 초과 불가) |

### 6.3 환불 프로세스

1. 가맹점이 Merchant Management Platform의 Transaction Tab에서 해당 주문 확인
2. 환불 금액, 사유, 상세 설명 입력
3. 환불 요청 제출
4. **즉시 처리**: 환불 금액이 고객의 Binance 지갑에 즉시 입금

> 출처: [Binance Merchant Docs - Refund Order](https://merchant.binance.com/en/docs/functionalities/refund-order)

### 6.4 환불 통화

- 환불은 **가맹점이 수취한 정산 통화**로 처리됨
- 예: 가맹점이 USDT로 정산 받았으면, 고객에게 USDT로 환불
- 고객이 원래 BTC로 결제했더라도, 환불은 USDT로 지급될 수 있음

### 6.5 API 기반 환불 (개발자)

Binance Pay는 Refund Order API를 제공하여 프로그래밍 방식의 환불 처리를 지원한다.

- **엔드포인트**: Refund Order API ([developers.binance.com](https://developers.binance.com/docs/binance-pay/api-order-refund))
- **기능**: 주문 ID 기반 전액/부분 환불 요청
- **응답**: 환불 상태, 환불 금액, 처리 시간 등

### 6.6 분쟁 해결 (Dispute Resolution)

Binance Pay Merchant 결제에 대한 분쟁 해결 절차는 P2P 거래와 상이하다.

**P2P 거래 분쟁 해결:**
- 고객서비스가 24-48시간 내 분쟁에 응답
- 항소(Appeal) 개시 후 상대방에게 10분간 채팅 협의 기회 부여
- 합의 도달 시 항소 취소 가능
- 합의 미달 시 Binance 고객지원팀이 개입하여 중재
- **분쟁 처리 수수료**: 4번째 분쟁부터 수수료 부과 (처음 3회 무료)

> 출처: [Binance P2P Appeal Handling Rules](https://www.binance.com/en/support/faq/binance-p2p-appeal-handling-rules-360041839052), [Dispute Handling Fee FAQ](https://www.binance.com/en/support/faq/what-is-the-dispute-handling-fee-6cc534c4d10b4328aedfd625bfdd0df4)

**Merchant 결제 분쟁:**
- 전통적인 신용카드 차지백(chargeback) 메커니즘은 **존재하지 않음**
- 암호화폐 결제의 특성상 결제 확정 후 자동 취소/환불이 불가
- 가맹점 재량으로 환불 처리 여부 결정
- Binance는 중개자로서 분쟁 조정 역할 수행 가능

---

## 7. P2P 결제 vs Merchant 결제 비교

| 항목 | P2P 결제 | Merchant 결제 |
|------|----------|---------------|
| **대상** | Binance 사용자 간 | 사업자 - 고객 간 |
| **수수료** | 무료 | 1% MDR |
| **결제 수단** | Pay ID, QR, 이메일, 전화번호 | API, Checkout Page, Payment Link |
| **정산** | 즉시 (상대방 지갑) | 즉시 (가맹점 지갑, USDT 등) |
| **환불** | 수동 재전송 | API/플랫폼 기반 체계적 환불 |
| **결제 확인** | 앱 알림 | Webhook 콜백 + 대시보드 |
| **적합 시나리오** | 개인 송금, 더치페이 | 이커머스, 구독, 매장 결제 |
| **가입 요건** | Binance 계정 | Merchant 계정 + KYB 인증 |
| **분쟁 해결** | P2P Appeal 프로세스 | 가맹점 재량 + Binance 중재 |

> Binance P2P 거래(Binance P2P Trading)는 Binance Pay와는 별개의 서비스로, 법정화폐-암호화폐 간 교환을 700개 이상의 결제 수단으로 지원하는 마켓플레이스이다. P2P Merchant 프로그램은 이 마켓플레이스에서 거래량이 높은 인증된 거래자를 위한 프로그램이다. 출처: [Binance P2P Merchant Program](https://www.binance.com/en/blog/p2p/what-is-the-binance-p2p-merchant-program-and-why-you-should-become-a-merchant-7451535141299655261)

---

## 8. 규제 환경 및 리스크

### 8.1 서비스 가용 국가

- **서비스 가능**: 180개국 이상, 50종 이상의 법정화폐 지원
- **완전 차단**: 미국, 캐나다, 쿠바, 이란, 시리아, 북한 등 70개국 이상 제한
- **규제 라이선스**: 18개 이상의 규제 라이선스 보유 (2026년 기준)

> 출처: [DataWallet](https://www.datawallet.com/crypto/binance-restricted-countries), [WorldPopulationReview](https://worldpopulationreview.com/country-rankings/binance-countries)

### 8.2 주요 규제 이슈

| 지역 | 규제 현황 | Binance Pay 영향 |
|------|-----------|-----------------|
| **미국** | SEC, CFTC 규제로 완전 차단 | 미국 시장 진입 불가. Binance.US는 별도 법인 |
| **EU** | MiCA 규제 2024년 12월 시행 | 일부 유럽 국가 철수 (벨기에 등) |
| **영국** | FCA 명령으로 2021년 서비스 중단 | 영국 시장 미진출 |
| **네덜란드** | EUR 3.3M 벌금 부과 | AML 규정 미준수 제재 |
| **일본/한국** | 현지 거래소 규제 프레임워크 | 현지 파트너십 또는 별도 라이선스 필요 |

> 출처: [CryptoWinRate](https://www.cryptowinrate.com/binance-restricted-supported-countries), [Wikipedia - Binance](https://en.wikipedia.org/wiki/Binance)

### 8.3 컴플라이언스 투자

- 2025년 3분기 기준 컴플라이언스 비용 **USD 1.2B** 지출
- 14개의 신규 지역 법인 설립
- KYC/AML 강화, 여행 규칙(Travel Rule) 준수

### 8.4 향후 규제 전망

- **스테이블코인 규제 강화**: 주요국의 스테이블코인 규제법 도입이 Binance Pay의 핵심 결제 수단(USDT)에 직접적 영향
- **CBDC 경쟁**: 중앙은행 디지털 화폐 출시 시 암호화폐 결제 수요 잠식 가능성
- **글로벌 조세 투명성**: OECD 암호화폐 과세 프레임워크(CARF) 적용으로 보고 의무 강화
- **긍정적 측면**: 규제 명확화가 오히려 기관 투자자 및 대형 가맹점 도입을 촉진할 수 있음

---

## 9. 산업 트렌드 및 시사점

### 9.1 스테이블코인 결제의 부상

2025년 Binance Pay B2C 결제의 **98% 이상이 스테이블코인**으로 처리되었다. 이는 암호화폐 결제 시장이 BTC/ETH 같은 변동성 자산에서 USDT/USDC 같은 안정 자산 기반으로 빠르게 전환되고 있음을 시사한다.

### 9.2 두 가지 시장 모델의 분화

2026년 현재, 암호화폐 결제 시장은 두 가지 모델로 분화되고 있다:

1. **전통 게이트웨이 모델** (BitPay, Coinbase Commerce): 크립토 수취 -> 법정화폐 전환 -> 은행 입금. 이커머스, 인보이스, POS에 최적화.
2. **생태계 내장형 모델** (Binance Pay): 거래소 생태계 내에서 크립토-크립토 정산. Binance 사용자 기반 활용에 최적화.

Binance Pay는 후자 모델의 대표 주자로, 3억 명 이상의 기존 사용자 기반이 핵심 경쟁력이다. 다만, 법정화폐 직접 정산이 불가하다는 점이 전통 사업자 도입의 장벽으로 작용할 수 있다.

### 9.3 기술 혁신 동향

- **L2 네트워크 활용**: Coinbase Commerce가 Base L2를 활용한 결제 프로토콜 도입
- **AI 기반 사기 탐지**: 결제 플랫폼들의 머신러닝 기반 이상 거래 탐지 강화
- **크로스체인 결제**: 다중 블록체인 간 원활한 결제 연동 기술 발전

---

## 10. 종합 평가

### SWOT 분석

| 강점 (Strengths) | 약점 (Weaknesses) |
|-------------------|-------------------|
| 3억 명 이상 Binance 사용자 기반 | 법정화폐 직접 정산 불가 |
| 즉시 정산 + 0% 가스비 | 미국/영국 등 주요 시장 미진출 |
| 300종 이상 암호화폐 지원 | Binance 계정 필수 (비사용자 결제 불가) |
| 경쟁력 있는 1% MDR | 규제 리스크에 대한 시장 우려 |

| 기회 (Opportunities) | 위협 (Threats) |
|----------------------|----------------|
| 신흥국 디지털 결제 성장 | 주요국 규제 강화 |
| 스테이블코인 결제 대중화 | CBDC 출시로 인한 수요 잠식 |
| 가맹점 네트워크 확대 | BitPay/Coinbase 등 경쟁 심화 |
| 법정화폐 정산 기능 추가 가능성 | 보안 사고 발생 시 신뢰도 하락 |

### 핵심 인사이트

1. **시장 지배력**: Binance Pay는 누적 거래량 USD 280B, 연간 USD 121B로 암호화폐 결제 시장에서 가장 큰 거래량을 처리하는 플랫폼 중 하나이다.
2. **스테이블코인 중심**: B2C 결제의 98%가 스테이블코인이라는 사실은, Binance Pay가 사실상 "디지털 달러 결제 플랫폼"으로 기능하고 있음을 보여준다.
3. **규제가 최대 변수**: 서비스 자체의 기술적 완성도는 높으나, 미국/EU/영국 등 고소득 시장에서의 서비스 제한이 성장의 가장 큰 제약이다.
4. **법정화폐 정산 간극**: BitPay 대비 법정화폐 직접 은행 입금이 불가하다는 점은 전통 사업자 도입 시 추가 허들로 작용한다.
5. **생태계 잠금 효과**: Binance 계정이 필수라는 점은 양날의 검으로, 기존 사용자에게는 편리하지만 신규 사용자 확보에는 장벽이 된다.

---

*본 보고서는 2026년 4월 14일 기준 공개 자료를 바탕으로 작성되었으며, 시장 상황 및 규제 환경은 수시로 변동될 수 있습니다.*
