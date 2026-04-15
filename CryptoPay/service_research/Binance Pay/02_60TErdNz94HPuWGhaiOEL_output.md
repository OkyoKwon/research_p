# 경쟁사 분석 -- Binance Pay

## 분석 개요

- **분석 대상**: Binance Pay (바이낸스 페이) 경쟁 환경
- **분석 일시**: 2026-04-15
- **선행 분석**: `01_Jr4DtyE94kyvJZ0stg_SY_output.md` (시장 현황 분석) 참조
- **분석 관점**: 결제(Payment) - 정산(Settlement) - 환불(Refund) 프로세스 중심
- **주요 참조 소스**:
  - [WestAfricaTradeHub - 2026 Buyer's Guide](https://westafricatradehub.com/crypto/best-crypto-payment-gateway-2026-buyers-guide-to-fees-settlement-and-coin-support/)
  - [Aurpay - Crypto Payment Gateway Comparison 2026](https://aurpay.net/aurspace/crypto-payment-gateway-comparison-2026/)
  - [VentureBurn - 14 Best Crypto Payment Gateway 2026](https://ventureburn.com/best-crypto-payment-gateway/)
  - [Paybis - BitPay Fees vs Alternatives 2026](https://paybis.com/blog/bitpay-pricing-fees-breakdown/)
  - 각 서비스 공식 문서 및 개발자 포털

---

## 1. 경쟁 구도 요약

- **직접 경쟁사 수**: 5개사 (동일한 암호화폐 결제 게이트웨이/결제 서비스)
- **간접 경쟁사 수**: 4개사 (전통 결제 기업의 크립토 확장 및 온체인 프로토콜)
- **시장 지배자**: BitPay (업력 최장, 법정화폐 정산 선도), Binance Pay (거래량 최대)
- **신흥 도전자**: Coinbase Commerce (Base L2 온체인 프로토콜), Stripe Stablecoin (전통 결제 인프라 + 스테이블코인), PayPal Crypto (대규모 가맹점 네트워크)

### 시장 포지셔닝 개관

암호화폐 결제 시장은 2026년 현재 크게 세 가지 진영으로 분화되고 있다:

1. **거래소 생태계 내장형**: Binance Pay, Crypto.com Pay -- 자사 거래소 사용자 기반 활용, 크립토-크립토 정산 중심
2. **전통 게이트웨이형**: BitPay, CoinGate, NOWPayments -- 크립토 수취 후 법정화폐 전환, 기존 사업자 친화적
3. **전통 결제 확장형 / 온체인 프로토콜형**: PayPal Crypto, Stripe Stablecoin, Coinbase Commerce (Base), Solana Pay -- 기존 결제 인프라에 크립토를 통합하거나, 탈중앙화 온체인 결제 레일 구축

---

## 2. 경쟁사 분류

| 구분 | 경쟁사명 | 유형 | 핵심 특징 |
|------|----------|------|-----------|
| **직접 경쟁사** | Coinbase Commerce | 거래소 기반 게이트웨이 | Base L2 온체인 결제 프로토콜, Shopify 통합, 1% 수수료 |
| **직접 경쟁사** | BitPay | 전통 게이트웨이 | 2011년 설립, 법정화폐 직접 은행 입금, 37개국 지원 |
| **직접 경쟁사** | CoinGate | 전통 게이트웨이 | EU 라이선스 보유, 즉시 법정화폐 전환, 70종+ 코인 |
| **직접 경쟁사** | NOWPayments | 비수탁형 게이트웨이 | 0.5% 최저 수수료, 300종+ 코인, 비수탁(non-custodial) |
| **직접 경쟁사** | Crypto.com Pay | 거래소 기반 게이트웨이 | 0% 가맹점 수수료, 8천만 사용자, 법정화폐 정산 지원 |
| **간접 경쟁사** | PayPal Crypto | 전통 결제 확장 | 100종+ 코인 결제, 자동 USD 정산, 4억+ 사용자 |
| **간접 경쟁사** | Stripe Stablecoin | 전통 결제 확장 | USDC 결제, 1.5% 수수료, 100개국+ 지원 |
| **간접 경쟁사** | Coinbase Commerce (Base Protocol) | 온체인 프로토콜 | 오픈소스 스마트 컨트랙트, ~200ms 정산, Shopify 통합 |
| **잠재 대체재** | Solana Pay | 탈중앙 결제 레일 | 수수료 $0.001 미만, 오픈소스, 프로토콜 레벨 |

---

## 3. 직접 경쟁사 심층 분석

### 3.1 Coinbase Commerce

**기업 프로필**

| 항목 | 내용 |
|------|------|
| 설립 | 2018년 (Coinbase 자회사) |
| 본사 | 미국 (San Francisco) |
| 모회사 | Coinbase Global, Inc. (NASDAQ: COIN) |
| 사용자 기반 | Coinbase 전체 1억 명+ |
| 주요 타깃 | 이커머스 가맹점, SaaS 사업자, Shopify 머천트 |

**결제-정산-환불 프로세스**

| 항목 | 상세 |
|------|------|
| **결제 수수료** | 1% (정산 통화에서 차감) |
| **지원 암호화폐** | 수백 종 (Base L2 프로토콜 전환 이후 대폭 확대) |
| **정산 통화** | USDC 기본, 자동 DEX 스왑으로 모든 토큰을 USDC로 전환 |
| **정산 속도** | ~200ms (Base L2), 즉시~1일 (레거시) |
| **정산 방식** | 온체인 스마트 컨트랙트 기반, 가맹점 지갑으로 직접 정산 |
| **법정화폐 정산** | Coinbase Business 통합으로 법정화폐 출금 가능 (2025~) |
| **환불** | 스마트 컨트랙트 기반 환불 (authorize-capture-refund 플로우) |
| **환불 기한** | 캡처 전까지 환불 가능, 캡처 후 만료 기간 내 환불 |
| **분쟁 해결** | 온체인 에스크로 기반, 스마트 컨트랙트가 자동 중재 |
| **통합 방식** | Shopify 플러그인, API, 오픈소스 프로토콜 |

**SWOT 요약**

| 강점 | 약점 |
|------|------|
| Base L2 기반 혁신적 온체인 프로토콜 | 미국 중심, 글로벌 확장 제한 |
| Shopify 통합으로 수백만 가맹점 접근 | 온체인 전환으로 기존 사용자 학습 비용 |
| 오픈소스로 생태계 확장 가능 | Coinbase 계정/지갑 의존도 |
| Coinbase 브랜드 신뢰도 | 스테이블코인(USDC) 외 정산 옵션 제한 |

---

### 3.2 BitPay

**기업 프로필**

| 항목 | 내용 |
|------|------|
| 설립 | 2011년 |
| 본사 | 미국 (Atlanta, GA) |
| 누적 투자 | $72M+ |
| 처리 실적 | 연간 수십억 달러 |
| 주요 타깃 | 전통 이커머스, 기업 결제, 인보이스 |

**결제-정산-환불 프로세스**

| 항목 | 상세 |
|------|------|
| **결제 수수료** | 1~2% + $0.25 (월 거래량 기반 차등) |
| | - $1M+/월: 1% + $0.25 |
| | - $500K~$1M/월: 1.5% + $0.25 |
| | - $500K 미만/월: 2% + $0.25 |
| **지원 암호화폐** | 100종+ (결제), 15종 (정산) |
| **정산 통화** | 법정화폐(USD, EUR, GBP 등) 또는 암호화폐(BTC, ETH, USDC 등) |
| **정산 속도** | T+1~T+2 영업일 (은행 입금), 매일 자동 정산 |
| **정산 방식** | 법정화폐 은행 직접 입금 (37개국), 크립토 지갑 정산 |
| **최소 정산 금액** | $20 USD / 0.01 BTC |
| **법정화폐 정산** | 가능 (핵심 강점) |
| **환불** | 가맹점이 승인 후 BitPay가 처리, 동일 암호화폐로 환불 |
| **환불 유형** | 전액 환불, 부분 환불 (현재 시세 또는 고정 환율 선택 가능) |
| **환불 수수료** | 마이너 수수료(가스비)를 가맹점 원장에서 차감 |
| **분쟁 해결** | BitPay 중재, BitPay Guarantee (차지백 보호 프로그램) |
| **통합 방식** | API, Shopify/WooCommerce 플러그인, 인보이스, POS |

**SWOT 요약**

| 강점 | 약점 |
|------|------|
| 14년 업력, 가장 성숙한 생태계 | 높은 수수료 (소규모 가맹점 2% + $0.25) |
| 법정화폐 직접 은행 입금 (37개국) | 긴 KYC 승인 과정 (수일~수주) |
| BitPay Guarantee 차지백 보호 | 정산 속도 T+1~T+2 (경쟁사 대비 느림) |
| 전통 기업 친화적 인터페이스 | 지원 암호화폐 수 (정산 시 15종 한정) |

---

### 3.3 CoinGate

**기업 프로필**

| 항목 | 내용 |
|------|------|
| 설립 | 2014년 |
| 본사 | 리투아니아 (빌뉴스) |
| 규제 라이선스 | EU 라이선스 보유 (리투아니아 등록) |
| 주요 타깃 | 유럽 중심 이커머스, iGaming, 디지털 서비스 |

**결제-정산-환불 프로세스**

| 항목 | 상세 |
|------|------|
| **결제 수수료** | 1% (기본) |
| **환전 수수료** | ~1% (암호화폐 간 또는 크립토-법정화폐 전환 시) |
| **카드 결제 수수료** | 8% (카드로 암호화폐 구매 시) |
| **지원 암호화폐** | 70종+ (결제), 90종+ (기프트카드) |
| **정산 통화** | EUR, USD, GBP 또는 BTC, ETH, LTC, BCH 등 크립토 |
| **정산 속도** | 즉시 (크립토-크립토), 최대 24시간 (크립토-법정화폐) |
| **정산 방식** | 법정화폐 은행 입금, 크립토 지갑 정산, 혼합 가능 |
| **법정화폐 정산** | 가능 (EUR, USD, GBP) -- 180개국+ |
| **환불** | 크립토 환불 지원 (전액/부분), 가맹점 계정 잔고에서 차감 |
| **환불 수수료** | 0.25 EUR 고정 + 환율 차이 발생 시 0.1% 추가 |
| **분쟁 해결** | 가맹점-고객 간 직접 해결, CoinGate 중재 지원 |
| **통합 방식** | API, Shopify/WooCommerce/Magento 플러그인, Payment Link |

**SWOT 요약**

| 강점 | 약점 |
|------|------|
| EU 라이선스 보유 (규제 준수) | 미국 시장 제한적 |
| 즉시 법정화폐 전환 정산 | 사용자 기반이 대형 경쟁사 대비 소규모 |
| 유연한 정산 옵션 (법정화폐/크립토/혼합) | 브랜드 인지도 낮음 |
| iGaming, 디지털 서비스에 특화 | 카드 결제 수수료 높음 (8%) |

---

## 4. 직접 경쟁사 -- 추가 프로파일

### 4.1 NOWPayments

| 항목 | 상세 |
|------|------|
| **설립** | 2019년 |
| **본사** | 네덜란드 (암스테르담) |
| **결제 수수료** | 0.5% (동일 코인), 1% (자동 환전 시) |
| **지원 암호화폐** | 300종+ |
| **정산 통화** | 모든 지원 암호화폐, 법정화폐는 제3자 파트너 경유 |
| **정산 속도** | 블록체인 컨펌 시간에 의존 (즉시~수분) |
| **정산 방식** | 비수탁형 -- 가맹점 지갑에 직접 입금 |
| **법정화폐 정산** | 직접 불가, 제3자 파트너 경유 |
| **환불** | 가맹점이 직접 처리 (NOWPayments는 비수탁이므로 자금 미보유) |
| **환불 지원** | Partnership Agreement 체결 시 간소화된 환불 프로세스 |
| **분쟁 해결** | 가맹점-고객 간 직접 해결 (NOWPayments 비관여) |
| **통합** | API, Shopify/WooCommerce 플러그인, 위젯, 인보이스, PoS |
| **특이사항** | 가장 낮은 수수료, 가장 많은 코인 지원, KYC 불필요(기본) |

### 4.2 Crypto.com Pay

| 항목 | 상세 |
|------|------|
| **설립** | 2019년 (Crypto.com Pay 출시) |
| **본사** | 싱가포르 |
| **모회사 사용자** | 8천만 명+ (Crypto.com 전체) |
| **결제 수수료** | 0% (가맹점 수수료 무료) |
| **Payout 수수료** | 정산 시 출금 수수료 별도 (블록체인 수수료 + 송금 수수료) |
| **지원 암호화폐** | 20종+ (결제) |
| **정산 통화** | USD, EUR, GBP, AUD 등 법정화폐 + 암호화폐 |
| **정산 속도** | 수 시간~1 영업일 (법정화폐), 즉시 (크립토) |
| **법정화폐 정산** | 가능 (핵심 강점) |
| **환불** | 전액/부분 환불 지원, Crypto.com App 사용자에게 자동 반환 |
| **환불 통화** | 고객이 선호 환불 통화 설정 가능 |
| **환불 수수료** | 블록체인 수수료 차감 가능 |
| **분쟁 해결** | Crypto.com 고객지원 중재 |
| **통합** | API, Shopify/WooCommerce 플러그인, Payment Button |

---

## 5. 간접 경쟁사 분석

### 5.1 PayPal Crypto ("Pay with Crypto")

| 항목 | 상세 |
|------|------|
| **출시** | 2025년 7월 (가맹점 결제 기능 확대) |
| **사용자 기반** | 4억 명+ (PayPal 전체) |
| **결제 수수료** | 0.99% (프로모션, 2026년 7월까지), 이후 1.5% |
| **지원 암호화폐** | 100종+ (결제), PYUSD 포함 |
| **정산 통화** | USD (기본), PYUSD (선택, 4% 연 수익률 제공) |
| **정산 속도** | 즉시~T+1 (PayPal 잔액으로) |
| **법정화폐 정산** | 자동 USD 전환 정산 (핵심 강점) |
| **환불** | PayPal 기존 환불/분쟁 시스템 활용 |
| **분쟁 해결** | PayPal Purchase Protection 적용 |
| **통합** | 기존 PayPal Checkout에 자동 통합, 추가 개발 불필요 |
| **지역 제한** | 미국 가맹점 한정 (2026년 4월 기준) |

### 5.2 Stripe Stablecoin

| 항목 | 상세 |
|------|------|
| **출시** | 2025년 (Bridge 인수 후 본격화) |
| **결제 수수료** | 1.5% (카드 2.9% + $0.30 대비 저렴) |
| **지원 스테이블코인** | USDC (Ethereum, Solana, Base, Polygon, Arbitrum, Avalanche, Optimism, Stellar) |
| **정산 통화** | USD, EUR, GBP 등 법정화폐 또는 USDC |
| **정산 속도** | 거의 즉시 (스테이블코인), T+2 (법정화폐) |
| **법정화폐 정산** | 자동 전환 정산 (Stripe가 가스비 부담) |
| **환불** | Stripe 기존 환불 시스템 활용 |
| **분쟁 해결** | Stripe 기존 분쟁 시스템 활용 |
| **통합** | 기존 Stripe API에 자연스럽게 통합, 크립토 지식 불필요 |
| **지역 제한** | 가맹점 수취: 미국 한정 (2026년 4월 기준), 결제자: 100개국+ |
| **특이사항** | Stripe가 가스비 전액 흡수, 추가 비용 없음 |

### 5.3 Coinbase Commerce Payments Protocol (Base L2)

| 항목 | 상세 |
|------|------|
| **출시** | 2025년 (온체인 프로토콜 전환) |
| **수수료** | 1% (온체인에서 자동 차감) |
| **정산** | USDC로 가맹점 지갑 직접 정산, ~200ms (Base L2) |
| **환불** | 스마트 컨트랙트 기반 authorize-capture-refund 플로우 |
| **분쟁 해결** | 온체인 에스크로 (캡처 만료 전까지 환불 가능) |
| **통합** | Shopify 플러그인, 오픈소스 프로토콜, 누구나 인스턴스 운영 가능 |
| **특이사항** | 오픈소스, 탈중앙화, Shopify 수백만 가맹점에 기본 제공 |

### 5.4 Solana Pay

| 항목 | 상세 |
|------|------|
| **출시** | 2022년 (프로토콜), 2025~2026년 기관 통합 가속 |
| **수수료** | $0.001 미만 (블록체인 가스비만, 프로토콜 수수료 없음) |
| **정산** | USDC on Solana 즉시 정산, 24/7 운영 |
| **거래량** | 2025년 $1T+ 스테이블코인 처리, 2026년 분기 $2T |
| **통합** | Shopify 플러그인, 오픈소스, 탈중앙 |
| **환불** | 프로토콜 레벨에서 환불 메커니즘 없음, 가맹점이 직접 처리 |
| **특이사항** | Visa, PayPal, Western Union 등 기관 통합 진행 중 |

---

## 6. 핵심 비교표

### 6.1 수수료 비교

| 경쟁사 | 결제 수수료 | 정산/출금 수수료 | 환불 수수료 | 가스비 부담 | 총비용 평가 |
|--------|------------|-----------------|------------|------------|-------------|
| **Binance Pay** | 1% MDR | 0.8% (최대 $5) | 없음 | 없음 (오프체인) | 중간 |
| **Coinbase Commerce** | 1% | 없음 (온체인 직접) | 없음 | 가맹점 (Base L2 ~$0.01) | 낮음 |
| **BitPay** | 1~2% + $0.25 | 은행 송금 수수료 | 마이너 수수료 차감 | 환불 시 마이너 수수료 | 높음 |
| **CoinGate** | 1% | 법정화폐 전환 ~1% | 0.25 EUR 고정 | 출금 시 네트워크 수수료 | 중간 |
| **NOWPayments** | 0.5~1% | 없음 (비수탁) | 없음 (가맹점 직접) | 가맹점 (블록체인 수수료) | 최저 |
| **Crypto.com Pay** | 0% | Payout 수수료 + 블록체인 수수료 | 블록체인 수수료 가능 | 출금 시 네트워크 수수료 | 낮음 |
| **PayPal Crypto** | 0.99% (프로모션) / 1.5% | 없음 (PayPal 잔액) | PayPal 기존 정책 | 없음 | 중간~높음 |
| **Stripe Stablecoin** | 1.5% | 없음 | Stripe 기존 정책 | Stripe 부담 | 중간 |
| **Solana Pay** | 0% (프로토콜) | 없음 | 없음 | ~$0.001 | 최저 |

### 6.2 정산 방식 비교

| 경쟁사 | 정산 속도 | 법정화폐 직접 정산 | 크립토 정산 | 정산 주기 | 정산 통화 옵션 |
|--------|----------|-------------------|------------|----------|---------------|
| **Binance Pay** | 즉시 | 불가 (거래소 환전 필요) | USDT 기본 | 실시간 | USDT 등 크립토 |
| **Coinbase Commerce** | ~200ms (Base) | Coinbase Business 경유 | USDC 기본 | 실시간 | USDC + 수백 종 토큰 |
| **BitPay** | T+1~T+2 | 가능 (37개국) | 가능 (15종) | 매 영업일 | USD, EUR, GBP + 15종 크립토 |
| **CoinGate** | 즉시~24h | 가능 (180개국+) | 가능 | 즉시~24h | EUR, USD, GBP + 크립토 |
| **NOWPayments** | 블록체인 컨펌 | 불가 (제3자 경유) | 가능 (300종+) | 실시간 | 300종+ 크립토 |
| **Crypto.com Pay** | 수 시간~1일 | 가능 | 가능 | T+0~T+1 | USD, EUR, GBP, AUD + 크립토 |
| **PayPal Crypto** | 즉시~T+1 | 자동 USD 전환 | PYUSD | 즉시 | USD, PYUSD |
| **Stripe Stablecoin** | 즉시 (USDC) / T+2 (법정화폐) | 자동 전환 | USDC | 즉시~T+2 | USD, EUR, GBP + USDC |
| **Solana Pay** | ~400ms | 불가 (직접) | USDC on Solana | 실시간 | USDC, SOL 등 |

### 6.3 환불/분쟁 해결 비교

| 경쟁사 | 환불 지원 | 환불 유형 | 환불 통화 | 차지백 | 분쟁 해결 |
|--------|----------|----------|----------|--------|----------|
| **Binance Pay** | API + 대시보드 | 전액/부분 | 정산 통화(USDT 등) | 없음 | 가맹점 재량 + Binance 중재 |
| **Coinbase Commerce** | 스마트 컨트랙트 | 전액/부분 | 온체인 (USDC) | 없음 (에스크로 기반) | 캡처 만료 전 자동 환불 |
| **BitPay** | API + 대시보드 | 전액/부분 | 동일 암호화폐 | BitPay Guarantee | BitPay 중재 + 차지백 보호 |
| **CoinGate** | 대시보드 | 전액/부분 | 크립토 (계정 잔고) | 없음 | CoinGate 중재 |
| **NOWPayments** | 가맹점 직접 | 전액/부분 | 가맹점 선택 | 없음 | 가맹점-고객 직접 |
| **Crypto.com Pay** | API + 대시보드 | 전액/부분 | 고객 선호 통화 | 없음 | Crypto.com 중재 |
| **PayPal Crypto** | PayPal 시스템 | 전액/부분 | USD | PayPal 차지백 | PayPal Purchase Protection |
| **Stripe Stablecoin** | Stripe 시스템 | 전액/부분 | 원래 결제 통화 | Stripe 차지백 | Stripe 분쟁 시스템 |
| **Solana Pay** | 없음 (프로토콜) | N/A | N/A | 없음 | 없음 |

### 6.4 가맹점 통합 난이도 비교

| 경쟁사 | 통합 난이도 | 주요 통합 방식 | KYC 요구 | 승인 소요 | 플러그인 지원 |
|--------|-----------|---------------|---------|----------|--------------|
| **Binance Pay** | 중간 | API, Hosted Checkout, Payment Link | KYB 필수 | 수일 | 제한적 |
| **Coinbase Commerce** | 낮음 | Shopify 플러그인, API, 오픈소스 프로토콜 | 기본 KYC | 즉시~수일 | Shopify 기본 통합 |
| **BitPay** | 중간 | API, Shopify/WooCommerce 플러그인, POS | KYB 필수 | 수일~수주 | 풍부 |
| **CoinGate** | 낮음 | API, 플러그인, Payment Link | KYC 필요 | 수일 | 풍부 (Shopify, WooCommerce, Magento 등) |
| **NOWPayments** | 매우 낮음 | API, 위젯, 플러그인, 인보이스 | 기본 불필요 | 즉시 | 풍부 |
| **Crypto.com Pay** | 낮음 | API, Shopify/WooCommerce 플러그인, Button | KYC 필요 | 수일 | 보통 |
| **PayPal Crypto** | 매우 낮음 | 기존 PayPal Checkout 자동 통합 | 기존 PayPal 가맹점 | 즉시 | PayPal 생태계 전체 |
| **Stripe Stablecoin** | 매우 낮음 | 기존 Stripe API 자연 통합 | 기존 Stripe 가맹점 | 즉시 | Stripe 생태계 전체 |
| **Solana Pay** | 높음 | 오픈소스 SDK, Shopify 플러그인 | 없음 | N/A | 제한적 |

### 6.5 지원 암호화폐 및 결제 방식 비교

| 경쟁사 | 지원 코인 수 | 주요 결제 방식 | P2P 송금 | QR 코드 | 구독 결제 |
|--------|------------|---------------|---------|---------|----------|
| **Binance Pay** | 300종+ (P2P), 50종+ (가맹점) | QR, Pay ID, 이메일, API | 가능 | 가능 | 미지원 |
| **Coinbase Commerce** | 수백 종 (Base) | Checkout, API, Shopify | 불가 | 가능 | 지원 (온체인) |
| **BitPay** | 100종+ | 인보이스, API, POS | 불가 | 가능 | 지원 |
| **CoinGate** | 70종+ | API, Payment Link, 플러그인 | 불가 | 가능 | 지원 |
| **NOWPayments** | 300종+ | API, 위젯, 인보이스 | 불가 | 가능 | 지원 |
| **Crypto.com Pay** | 20종+ | API, Button, 플러그인 | Crypto.com App 내 | 가능 | 지원 |
| **PayPal Crypto** | 100종+ | PayPal Checkout | PayPal P2P | 가능 | 지원 |
| **Stripe Stablecoin** | USDC만 | Stripe Checkout, API | 불가 | 불가 | 지원 (Private Preview) |
| **Solana Pay** | Solana 기반 토큰 | SDK, QR | 가능 | 가능 | 미지원 |

### 6.6 P2P vs Merchant 결제 차별화 비교

| 경쟁사 | P2P 결제 | Merchant 결제 | P2P-Merchant 통합도 |
|--------|----------|---------------|-------------------|
| **Binance Pay** | 무료, 즉시, 300종+ | 1% MDR, 즉시, API/Checkout | 높음 (동일 앱 내 통합) |
| **Coinbase Commerce** | Coinbase Wallet 별도 | 1%, 온체인 프로토콜 | 낮음 (별도 제품) |
| **BitPay** | BitPay Wallet 별도 | 1~2%, 은행 정산 | 낮음 (별도 제품) |
| **CoinGate** | 미지원 | 1%, 법정화폐/크립토 정산 | N/A |
| **NOWPayments** | 미지원 | 0.5~1%, 비수탁 | N/A |
| **Crypto.com Pay** | Crypto.com App 내 | 0%, 법정화폐/크립토 정산 | 높음 (동일 앱 내) |
| **PayPal Crypto** | PayPal P2P | 0.99~1.5%, USD 정산 | 매우 높음 (완전 통합) |
| **Stripe Stablecoin** | 미지원 | 1.5%, 법정화폐 정산 | N/A |
| **Solana Pay** | 프로토콜 수준 | 프로토콜 수준 | 동일 프로토콜 |

### 6.7 규제/지역 제한 비교

| 경쟁사 | 서비스 가능 지역 | 미국 | EU | 영국 | 아시아 | 규제 라이선스 |
|--------|----------------|------|-----|------|--------|-------------|
| **Binance Pay** | 180개국+ (70개국 제한) | 차단 | 일부 제한 | 차단 | 일부 가능 | 18개+ |
| **Coinbase Commerce** | 글로벌 (OFAC 제재국 제외) | 가능 | 가능 | 가능 | 일부 | Coinbase 라이선스 활용 |
| **BitPay** | 37개국 (은행 정산) | 가능 | 가능 | 가능 | 제한적 | MSB 등록 (미국) |
| **CoinGate** | 180개국+ (결제) | 제한적 | 가능 (핵심) | 가능 | 일부 | EU 라이선스 |
| **NOWPayments** | 글로벌 (비수탁) | 가능 | 가능 | 가능 | 가능 | 제한적 |
| **Crypto.com Pay** | 글로벌 | 가능 | 가능 | 가능 | 가능 (핵심) | 다수 보유 |
| **PayPal Crypto** | 미국 한정 (가맹점) | 가능 (핵심) | 미지원 | 미지원 | 미지원 | PayPal 라이선스 |
| **Stripe Stablecoin** | 100개국+ (결제자) / 미국 (가맹점) | 가능 (핵심) | 제한적 | 미지원 | 미지원 | Stripe 라이선스 |
| **Solana Pay** | 글로벌 (탈중앙) | 가능 | 가능 | 가능 | 가능 | N/A (프로토콜) |

---

## 7. 경쟁사 포지셔닝 맵

두 가지 핵심 축을 기준으로 경쟁사의 포지셔닝을 텍스트로 표현한다.

### 맵 1: 법정화폐 정산 용이성 vs 암호화폐 네이티브 깊이

```
                    법정화폐 정산 용이성 (높음)
                              |
                   PayPal     |    Stripe
                   Crypto     |    Stablecoin
                              |
                    BitPay    |
                              |
                   CoinGate   |   Crypto.com Pay
                              |
    ──────────────────────────┼──────────────────────────
    암호화폐 네이티브 깊이     |     암호화폐 네이티브 깊이
    (낮음)                    |     (높음)
                              |
                              |   Coinbase Commerce
                              |   (Base Protocol)
                              |
                NOWPayments   |   Binance Pay
                              |
                              |
                 Solana Pay   |
                              |
                    법정화폐 정산 용이성 (낮음)
```

**해석**:
- **우측 상단 (법정화폐 정산 쉬움 + 크립토 깊음)**: Crypto.com Pay가 유일하게 양쪽 강점을 겸비
- **좌측 상단 (법정화폐 중심)**: PayPal, Stripe, BitPay -- 전통 사업자에게 가장 친숙
- **우측 하단 (크립토 네이티브)**: Binance Pay, Coinbase Commerce -- 크립토 생태계 내 강력하나 법정화폐 정산 허들 존재
- **좌측 하단**: NOWPayments, Solana Pay -- 탈중앙/비수탁 지향, 양쪽 모두 가맹점이 직접 처리

### 맵 2: 가맹점 진입 장벽 vs 거래량/생태계 규모

```
                    거래량/생태계 규모 (대규모)
                              |
                   PayPal     |   Binance Pay
                   Crypto     |
                              |
                    Stripe    |   Crypto.com Pay
                              |
                              |   Coinbase Commerce
    ──────────────────────────┼──────────────────────────
    가맹점 진입 장벽           |     가맹점 진입 장벽
    (높음)                    |     (낮음)
                              |
                    BitPay    |   NOWPayments
                              |
                              |   CoinGate
                              |
                              |   Solana Pay
                              |
                    거래량/생태계 규모 (소규모)
```

**해석**:
- **우측 상단**: Binance Pay는 최대 거래량 + 낮은 진입 장벽(Binance 사용자 기준)
- **좌측 상단**: PayPal, Stripe는 대규모이나 미국 한정/기존 가맹점 전용
- **우측 하단**: NOWPayments, CoinGate는 진입이 쉬우나 생태계 규모 제한
- **좌측 하단**: BitPay는 긴 KYC 과정 + 상대적 소규모 (크립토 네이티브 시장 내)

---

## 8. 차별화 기회 및 경쟁 공백 분석

### 8.1 Binance Pay의 핵심 경쟁 우위

1. **압도적 사용자 기반**: 3억 명+ Binance 사용자가 즉시 활용 가능한 결제 네트워크
2. **즉시 정산 + 제로 가스비**: 오프체인 처리로 가장 빠르고 저렴한 정산
3. **최다 암호화폐 지원**: P2P 300종+, 가맹점 50종+
4. **P2P + Merchant 통합**: 하나의 앱에서 개인 송금과 가맹점 결제를 모두 지원

### 8.2 Binance Pay의 핵심 취약점

1. **법정화폐 직접 정산 불가**: BitPay, CoinGate, Crypto.com Pay, PayPal, Stripe 모두 법정화폐 직접 정산 가능
2. **주요 고소득 시장 미진출**: 미국, 영국 차단 -- PayPal, Stripe, BitPay, Coinbase의 핵심 시장
3. **Binance 계정 필수**: 비사용자는 결제 불가, PayPal/Stripe는 기존 인프라에 자연 통합
4. **규제 리스크**: 글로벌 규제 환경에서 Binance 브랜드 리스크

### 8.3 경쟁 공백 (White Space)

| 공백 영역 | 설명 | 진입 가능성 |
|-----------|------|------------|
| **법정화폐 자동 정산 + 크립토 300종 지원** | BitPay는 법정화폐 정산이 강하나 코인 수 제한, NOWPayments는 300종이나 법정화폐 정산 약함. 양쪽을 겸비한 서비스 부재 | 높음 -- Binance가 법정화폐 정산을 추가하면 독보적 |
| **글로벌 구독 결제** | 크립토 구독 결제 시장은 Stripe, Coinbase가 선점 중이나 아직 초기. Binance Pay는 구독 미지원 | 중간 -- 기술적 구현 가능하나 규제 허들 |
| **온체인 에스크로 기반 분쟁 해결** | Coinbase Commerce Protocol만 스마트 컨트랙트 기반 분쟁 해결 제공. 나머지는 수동/중재 방식 | 중간 -- BNB Chain 기반 구현 가능 |
| **신흥국 소상공인 결제** | 동남아, 아프리카, 남미에서 암호화폐 결제 수요 급증하나 전문 솔루션 부족 | 매우 높음 -- Binance의 신흥국 강점 활용 |
| **오프라인 POS 크립토 결제** | BitPay만 POS 지원, 나머지는 온라인 중심 | 중간 -- QR 코드 기반 확장 가능 |

### 8.4 위협 요인

1. **PayPal/Stripe의 크립토 확장**: 4억+ PayPal 사용자, 수백만 Stripe 가맹점에 크립토 결제가 기본 통합되면 별도 크립토 게이트웨이의 존재 의의 약화
2. **Coinbase Commerce Protocol의 오픈소스 전략**: Shopify 수백만 가맹점에 기본 제공, 오픈소스로 생태계 확장 -- Binance Pay의 폐쇄적 생태계와 대조
3. **Solana Pay 기관 통합**: Visa, PayPal, Western Union이 Solana 기반 정산을 채택하면 프로토콜 레벨에서 경쟁 발생
4. **CBDC 출시**: 주요국 CBDC가 크립토 결제 수요를 일부 대체할 가능성

---

## 9. 종합 평가

### 경쟁력 스코어카드 (10점 만점)

| 평가 항목 | Binance Pay | Coinbase Commerce | BitPay | CoinGate | NOWPayments | Crypto.com Pay | PayPal Crypto | Stripe Stablecoin |
|-----------|:-----------:|:-----------------:|:------:|:--------:|:-----------:|:--------------:|:-------------:|:-----------------:|
| 수수료 경쟁력 | 7 | 7 | 4 | 7 | 9 | 10 | 7 | 6 |
| 정산 속도 | 10 | 10 | 4 | 7 | 6 | 6 | 8 | 8 |
| 법정화폐 정산 | 2 | 5 | 10 | 9 | 3 | 8 | 10 | 10 |
| 환불/분쟁 해결 | 6 | 9 | 8 | 7 | 3 | 7 | 10 | 10 |
| 지원 암호화폐 | 10 | 9 | 7 | 7 | 10 | 4 | 8 | 2 |
| 통합 용이성 | 6 | 8 | 6 | 8 | 9 | 7 | 10 | 10 |
| 사용자 기반 | 10 | 7 | 5 | 4 | 3 | 7 | 10 | 8 |
| 규제 안정성 | 5 | 8 | 8 | 8 | 5 | 7 | 10 | 10 |
| P2P + Merchant 통합 | 10 | 3 | 3 | 1 | 1 | 8 | 9 | 1 |
| **종합 평균** | **7.3** | **7.3** | **6.1** | **6.4** | **5.4** | **7.1** | **9.1** | **7.2** |

### 핵심 인사이트

1. **PayPal Crypto가 가장 강력한 위협**: 수수료, 정산, 환불, 통합, 사용자 기반, 규제 모든 면에서 높은 점수. 다만 미국 한정이라는 치명적 지역 제한이 있어 당분간 글로벌 시장에서 Binance Pay와 직접 충돌하지 않음.

2. **Binance Pay vs Coinbase Commerce**: 종합 점수는 동일하나 강점 영역이 정반대. Binance Pay는 사용자 기반과 P2P 통합에서 우세, Coinbase Commerce는 온체인 혁신과 환불 체계에서 우세. 향후 Base L2 프로토콜의 성장이 핵심 변수.

3. **법정화폐 정산이 최대 과제**: Binance Pay의 법정화폐 정산 점수(2/10)는 전체 경쟁사 중 최저. 이 한 가지 약점이 전통 사업자 도입의 가장 큰 장벽이며, Binance가 채널 파트너를 통해 법정화폐 정산을 확대하면 경쟁력이 크게 향상될 것.

4. **비수탁형 vs 수탁형의 분화**: NOWPayments, Solana Pay 등 비수탁형 서비스는 수수료와 검열 저항성에서 우세하나, 환불/분쟁 해결에서 취약. 반대로 수탁형(Binance Pay, BitPay 등)은 체계적 환불을 제공하나 규제 리스크 존재.

5. **Stripe/PayPal의 "크립토 지식 불필요" 전략**: 기존 가맹점이 추가 개발 없이 크립토 결제를 수용할 수 있다는 점은 전용 크립토 게이트웨이에 대한 구조적 위협. 장기적으로 "크립토 결제"가 별도 카테고리가 아닌 기존 결제 인프라의 일부로 흡수될 가능성.

---

## Sources

- [BitPay Pricing](https://www.bitpay.com/pricing)
- [BitPay Settlement](https://developer.bitpay.com/docs/settlement)
- [BitPay Fees FAQ](https://support.bitpay.com/hc/en-us/articles/203324073-What-fees-will-I-pay-to-use-BitPay-for-payment-processing)
- [BitPay Fees vs Alternatives 2026](https://paybis.com/blog/bitpay-pricing-fees-breakdown/)
- [Coinbase Commerce Fees](https://help.coinbase.com/en/commerce/getting-started/fees)
- [Coinbase Commerce Onchain Protocol Deep Dive](https://www.coinbase.com/blog/coinbase-commerce-onchain-payment-protocol-deep-dive)
- [Commerce Payments Protocol - Shopify Engineering](https://shopify.engineering/commerce-payments-protocol)
- [CoinGate Pricing](https://coingate.com/pricing)
- [CoinGate Settlements and Withdrawals](https://coingate.com/blog/post/payouts-fiat-settlements)
- [CoinGate Merchant Refund](https://coingate.com/blog/post/merchant-refund)
- [NOWPayments Pricing](https://nowpayments.io/pricing)
- [NOWPayments Refund Policy](https://nowpayments.io/help/payments/common/refund-policy)
- [Crypto.com Pay Docs](https://pay-docs.crypto.com/)
- [Crypto.com Pay Settlement Currencies](https://help.crypto.com/en/articles/6063012-what-are-the-supported-settlement-currencies)
- [Crypto.com Pay Refund](https://help.crypto.com/en/articles/6014589-how-to-get-a-refund)
- [PayPal Pay with Crypto](https://web3.bitget.com/en/academy/paypal-pay-with-crypto-how-it-works-fees-and-what-it-means-for-merchants-in-2025)
- [PayPal Crypto Payments Expansion - CoinDesk](https://www.coindesk.com/business/2025/07/28/paypay-expands-crypto-payments-for-u-s-merchants-to-cut-cross-border-fees)
- [Stripe Stablecoin Payments Docs](https://docs.stripe.com/payments/stablecoin-payments)
- [Stripe 1.5% Fee - Yahoo Finance](https://finance.yahoo.com/news/stripe-charges-1-5-stablecoin-145737023.html)
- [Solana Pay](https://solanapay.com/)
- [Solana Payments.org 2026](https://stablecoininsider.org/solanas-new-payments-org/)
- [WestAfricaTradeHub - 2026 Buyer's Guide](https://westafricatradehub.com/crypto/best-crypto-payment-gateway-2026-buyers-guide-to-fees-settlement-and-coin-support/)
- [Aurpay - Crypto Payment Gateway Comparison 2026](https://aurpay.net/aurspace/crypto-payment-gateway-comparison-2026/)
- [VentureBurn - Best Crypto Payment Gateway 2026](https://ventureburn.com/best-crypto-payment-gateway/)

---

*본 보고서는 2026년 4월 15일 기준 공개 자료를 바탕으로 작성되었으며, 각 서비스의 수수료 및 정책은 수시로 변동될 수 있습니다.*
