# 경쟁사 분석 -- Coinbase Commerce / Coinbase Payment

## 분석 개요

- **분석 대상**: Coinbase Commerce 결제 서비스의 경쟁 환경
- **분석 일시**: 2026-04-14
- **분석 관점**: 결제(Payment) - 정산(Settlement) - 환불(Refund) 프로세스 중심
- **주요 참조 소스**: BitPay 공식 문서, CoinGate 공식 사이트, NOWPayments 공식 사이트, BTCPay Server 문서, PayPal 개발자 문서, Stripe 문서, Circle 공식 발표, G2/Capterra 리뷰, CoinDesk, PYMNTS, Benzinga, Yahoo Finance

---

## 1. 경쟁 구도 요약

- **직접 경쟁사 수**: 6개 (BitPay, CoinGate, NOWPayments, BTCPay Server, Binance Pay, PayPal Crypto)
- **시장 지배자**: BitPay (시장점유율 약 20%)
- **신흥 도전자**: PayPal Pay with Crypto (전통 결제 인프라 + 암호화폐), Stripe Stablecoin Payments
- **간접 경쟁사**: Stripe (스테이블코인 결제), Circle CPN (USDC 인프라), MoonPay (온램프)

### 경쟁 지형의 핵심 특징

1. **수탁형 vs 비수탁형** 구도가 시장을 양분하고 있음
2. **스테이블코인 중심 결제**가 주류로 부상하면서 전통 결제 기업(PayPal, Stripe)의 진입이 가속화
3. **법정화폐 정산 능력**이 가맹점 채택의 핵심 변수로 작용
4. **환불 프로세스의 자동화 수준**이 경쟁사 간 가장 큰 차별점

---

## 2. 경쟁사 분류

| 구분 | 경쟁사명 | 핵심 포지셔닝 |
|------|---------|-------------|
| **직접 경쟁사** | BitPay | 가맹점 채택 1위, 법정화폐 정산 강점 |
| **직접 경쟁사** | CoinGate | 유럽 시장 특화, 규제 준수, SEPA 무료 정산 |
| **직접 경쟁사** | NOWPayments | 최다 암호화폐 지원(350+), 최저 수수료(0.5%) |
| **직접 경쟁사** | BTCPay Server | 완전 자기주권, 오픈소스, 수수료 0% |
| **직접 경쟁사** | Binance Pay | 바이낸스 생태계, 아시아 시장 강점 |
| **직접 경쟁사** | PayPal Crypto | 전통 결제 최대 사업자의 암호화폐 확장 |
| **간접 경쟁사** | Stripe Stablecoin | 기존 Stripe 가맹점에 스테이블코인 결제 추가 |
| **간접 경쟁사** | Circle CPN | USDC 인프라 제공자, 은행/PSP 대상 |
| **잠재 대체재** | MoonPay | 암호화폐 온/오프램프, 결제보다는 구매 인프라 |

---

## 3. 핵심 경쟁사 심층 분석

### 3.1 BitPay -- 시장 1위 가맹점 결제 게이트웨이

**기본 프로필**

| 항목 | 내용 |
|------|------|
| 설립 | 2011년 |
| 본사 | 미국 애틀랜타 |
| 시장점유율 | 약 20% (가맹점 기준 1위) |
| 주요 고객 | Microsoft, AT&T, Newegg, Shopify 가맹점 |
| 라이선스 | 미국 각주 Money Transmitter License |

**결제 프로세스**

- RESTful API 기반 Invoice(청구서) 생성 방식
- 소비자가 BitPay 인보이스에서 암호화폐 전송
- 15개 암호화폐로 결제 가능 (BTC, ETH, XRP, LTC, BCH, DOGE, SHIB, APE, USDC, USDT, EUROC, DAI, GUSD, PAX, WBTC)
- Transaction Speed 설정으로 블록 확인 수 조절 가능

**정산 프로세스**

- **정산 주기**: 매 영업일 자동 정산
- **법정화폐 정산**: USD, EUR, GBP 등 지원 (38개국 은행 입금)
- **암호화폐 정산**: 최대 5종 암호화폐로 동시 정산 가능
- **혼합 정산**: 법정화폐 1종 + 암호화폐 최대 5종 조합 가능
- **정산 최소 금액**: USD $20 (ACH 기준)

**환불 프로세스**

- 가맹점 대시보드에서 직접 환불 처리 (전액/부분 환불 가능)
- **BitPay가 환불을 대행**: 가맹점이 환불 요청 시 BitPay가 소비자에게 이메일 발송
- 소비자가 링크를 통해 환불 수령 주소 제출
- 결제 시 사용한 암호화폐로 환불 (가격 통화 기준 또는 결제 통화 기준 선택 가능)
- **환불 수수료**: 마이너 수수료(네트워크 수수료)는 환불금에서 차감 (가맹점이 부담 선택 가능)
- 원래 처리 수수료(Network Cost fee)는 환불 불가

**SWOT 분석**

| 구분 | 내용 |
|------|------|
| **강점** | 시장 1위 점유율, 38개국 법정화폐 정산, 체계적 환불 시스템, 풍부한 API 문서 |
| **약점** | 상대적으로 높은 수수료(1-2%+$0.25), 제한된 암호화폐 수(15종), 수탁형 모델 의존 |
| **기회** | 규제 명확화에 따른 기관 고객 확대, GENIUS Act 수혜 |
| **위협** | PayPal/Stripe의 저수수료 진입, BTCPay Server의 무수수료 대안, Coinbase의 Shopify 독점 파트너십 |

---

### 3.2 NOWPayments -- 최다 암호화폐 지원 및 최저 수수료

**기본 프로필**

| 항목 | 내용 |
|------|------|
| 설립 | 2019년 |
| 본사 | 네덜란드 암스테르담 |
| 주요 특징 | 350+ 암호화폐 지원, 0.5% 최저 수수료 |
| 주요 고객 | 중소규모 가맹점, 게이밍, 기부 플랫폼 |
| 모델 | 비수탁형 옵션 제공 |

**결제 프로세스**

- API, 플러그인, 결제 링크, PoS 등 다양한 통합 방식
- 350+ 암호화폐 지원 (업계 최다)
- 자동 환전(Auto-Conversion) 기능: 고객이 A 코인으로 결제 시 가맹점이 B 코인으로 수령 가능
- 2026년 초 신규 사용자 대상 USDT(TRC20) 네트워크 수수료 무료 프로모션

**정산 프로세스**

- **정산 주기**: 즉시 (암호화폐 정산), 법정화폐 정산은 별도 출금 절차
- **법정화폐 정산**: 가능 (출금 수수료 1.5-2.3%)
- **암호화폐 정산**: 비수탁형 -- 가맹점 지갑으로 직접 전송
- **대량 지급(Mass Payouts)**: 제휴/계약자/파트너 대량 결제 기능

**환불 프로세스**

- **제한적 자동 환불**: 플랫폼 수준의 체계적 환불 시스템 미비
- 거래 실패 시 NOWPayments가 환불 중재 (Partnership Agreement 필요)
- 최소 금액 미달 결제는 환불 불가 (자금 접근 불가)
- 분쟁 해결은 이메일 기반 수동 프로세스 (support@nowpayments.io)

**SWOT 분석**

| 구분 | 내용 |
|------|------|
| **강점** | 업계 최다 암호화폐 지원(350+), 최저 수수료(0.5%), 비수탁형 옵션, 대량 지급 기능 |
| **약점** | 환불 시스템 미흡, 고객 지원 품질 이슈, 법정화폐 정산 수수료 높음(1.5-2.3%) |
| **기회** | 알트코인 결제 수요 증가, 게이밍/기부 시장 확대 |
| **위협** | 주요 경쟁사의 암호화폐 지원 확대, 규제 강화 시 소규모 코인 지원 부담 |

---

### 3.3 PayPal Pay with Crypto -- 전통 결제 최강자의 암호화폐 진출

**기본 프로필**

| 항목 | 내용 |
|------|------|
| 서비스 출시 | 2025년 7월 |
| 본사 | 미국 산호세 |
| 사용자 기반 | 4억+ PayPal 사용자 |
| 핵심 전략 | PYUSD 스테이블코인 중심, 기존 결제 UX 유지 |
| 지원 지역 | 미국 (뉴욕 제외) |

**결제 프로세스**

- 기존 PayPal Checkout에 암호화폐 결제 옵션 추가
- 100+ 암호화폐 지원 (Coinbase Wallet, MetaMask, Kraken, OKX 등 외부 지갑 연결)
- 소비자가 암호화폐로 결제 시 즉시 PYUSD로 전환
- 가맹점은 기존 PayPal 통합만으로 암호화폐 결제 수령 가능

**정산 프로세스**

- **정산 주기**: 거의 즉시 (PYUSD로 전환 후 PayPal 잔액에 반영)
- **법정화폐 정산**: USD로 자동 정산 (기존 PayPal 출금 프로세스)
- **PYUSD 보유 인센티브**: PayPal에 PYUSD 보유 시 연 4% 수익률 제공
- **수수료**: 0.99% (2026.07.31까지 프로모션), 이후 1.5%

**환불 프로세스**

- 가맹점이 USD 기준으로 환불 금액 지정
- PayPal이 환불 금액을 PYUSD로 변환하여 소비자 지갑에 전송
- **네트워크 수수료**: 가맹점 부담 (추정치와 실제 수수료 차이 발생 가능)
- **핵심 차이점**: 암호화폐 결제는 차지백/분쟁 대상 제외, Seller Protection 미적용
- 환불은 가맹점 자발적 처리 (전통 PayPal과 달리 강제 환불 없음)

**SWOT 분석**

| 구분 | 내용 |
|------|------|
| **강점** | 4억+ 기존 사용자 기반, 매끄러운 UX, 가맹점 추가 통합 불필요, 차지백 없음 |
| **약점** | 미국 한정(뉴욕 제외), PYUSD 중심으로 다른 스테이블코인 제약, 프로모션 종료 후 수수료 인상(1.5%) |
| **기회** | 글로벌 확장 시 최대 위협, 기존 가맹점 자동 전환 가능 |
| **위협** | 규제 변화 리스크, 암호화폐 순수주의자 반발, Stripe과의 경쟁 |

---

## 4. 기타 직접 경쟁사

### 4.1 BTCPay Server -- 완전 자기주권 오픈소스

| 항목 | 내용 |
|------|------|
| 설립 | 2017년 |
| 모델 | 오픈소스 (MIT 라이선스), 셀프 호스팅 |
| 수수료 | **0%** (처리 수수료 없음, 서버 비용 $8/월~만 발생) |
| 지원 코인 | 120+ (BTC + Lightning Network + 알트코인) |
| 정산 | 암호화폐 직접 수령, Strike API 통해 법정화폐 전환 가능 |
| 환불 | 대시보드에서 수동 환불, Lightning/온체인 환불 지원 |
| 통합 | WooCommerce, Shopify, Magento, Prestashop, Drupal 등 |
| 핵심 강점 | 완전한 프라이버시, 수수료 무료, 제3자 의존 없음 |
| 핵심 약점 | 기술적 진입장벽 높음, 법정화폐 정산 제한적, 가맹점 셀프서비스 |

### 4.2 CoinGate -- 유럽 시장 특화

| 항목 | 내용 |
|------|------|
| 설립 | 2014년 |
| 본사 | 리투아니아 빌뉴스 |
| 시장점유율 | 약 14% |
| 수수료 | 1% (셋업/월비 없음) |
| 지원 코인 | 70+ 암호화폐, 11개 블록체인 |
| 정산 통화 | EUR, GBP, USD + 암호화폐 + 스테이블코인 |
| 정산 주기 | 주 1회 (기본), SEPA 출금 무료 |
| 환불 | 대시보드/API에서 전액/부분 환불 가능, 암호화폐로 환불 |
| 핵심 강점 | 유럽 규제 준수(VASP 라이선스), SEPA 무료 정산, 간편한 환불 |
| 핵심 약점 | 상대적으로 적은 코인 수(70+), 주간 정산 주기, 비유럽 시장 약세 |

### 4.3 Binance Pay -- 바이낸스 생태계 활용

| 항목 | 내용 |
|------|------|
| 설립 | 2021년 |
| 모델 | 바이낸스 거래소 연동 |
| 수수료 | 약 1% MDR, 내부 이체 무료 |
| 정산 | **암호화폐 전용** (법정화폐 직접 정산 불가) |
| 환불 | 제한적 (바이낸스 내부 이체로 처리) |
| 지원 코인 | 70+ |
| 핵심 강점 | 바이낸스 1.8억+ 사용자 기반, 내부 이체 무료, 아시아 시장 |
| 핵심 약점 | 법정화폐 정산 불가, 규제 리스크(미국 시장 제한), 바이낸스 의존 |

---

## 5. 간접 경쟁사 분석

### 5.1 Stripe Stablecoin Payments

| 항목 | 내용 |
|------|------|
| 출시 | 2025년 |
| 수수료 | **1.5%** |
| 지원 스테이블코인 | USDC, USDP, USDG |
| 지원 네트워크 | Ethereum, Solana, Polygon, Base |
| 정산 | USD로 자동 정산 (Stripe 잔액) 또는 USDC 외부 지갑 전송 |
| 가맹점 기반 | 수백만 기존 Stripe 가맹점 (34개국 Shopify 연동) |
| 핵심 위협 | 기존 Stripe 통합만으로 스테이블코인 결제 수령 가능, Crypto.com과 파트너십 |

### 5.2 Circle CPN Managed Payments

| 항목 | 내용 |
|------|------|
| 출시 | 2026년 4월 8일 |
| 대상 고객 | PSP, 핀테크, 은행 (B2B2C) |
| 핵심 기능 | 기관이 법정화폐만 취급하고 Circle이 USDC 생명주기 전체 관리 |
| 지원 네트워크 | 20+ 블록체인 + 국내 결제 레일 |
| 포지셔닝 | Coinbase Commerce와 협력 관계이나, 장기적으로 USDC 결제 인프라 대체 가능 |

### 5.3 MoonPay

| 항목 | 내용 |
|------|------|
| 설립 | 2019년 |
| 핵심 기능 | 암호화폐 온/오프램프 (구매/판매 인프라) |
| 수수료 | 카드 결제 4.5%, 은행 이체 1% (실질 총비용 7-8%) |
| 포지셔닝 | 가맹점 결제보다는 개인의 암호화폐 구매/판매 인프라에 특화 |
| Coinbase 관련성 | 잠재 대체재이나 직접 경쟁은 제한적, 보완적 역할 |

---

## 6. 결제-정산-환불 프로세스 비교표

### 6.1 수수료 구조 비교

| 경쟁사 | 거래 수수료 | 셋업/월비 | 법정화폐 출금 수수료 | 총비용 (USD 정산 기준) |
|--------|-----------|----------|-------------------|---------------------|
| **Coinbase Commerce** | 1% | 없음 | 추가 1-1.5% (거래소 스프레드) | **약 2-2.5%** |
| **BitPay** | 1-2% + $0.25 | 없음 | 포함 (정산에 내재) | **약 1-2.25%** |
| **CoinGate** | 1% | 없음 | SEPA 무료 / 기타 0.5-1% | **약 1-2%** |
| **NOWPayments** | 0.5% (단일통화) / 1% (환전 포함) | 없음 | 1.5-2.3% | **약 2-3.3%** |
| **BTCPay Server** | 0% | 서버 $8/월~ | 자체 환전 (거래소 수수료 별도) | **약 0.5-1.5%** |
| **Binance Pay** | 약 1% | 없음 | 직접 정산 불가 (거래소 환전) | **약 1.5-2.5%** |
| **PayPal Crypto** | 0.99% (프로모션) / 1.5% (정상) | 없음 | 기존 PayPal 출금 수수료 | **약 1-1.5%** (프로모션) / **약 1.5-2%** (정상) |
| **Stripe Stablecoin** | 1.5% | 없음 | 기존 Stripe 출금 프로세스 | **약 1.5%** |

### 6.2 정산 방식 비교

| 경쟁사 | 정산 주기 | 법정화폐 정산 | 정산 통화 | 자동 환전 |
|--------|----------|-------------|---------|----------|
| **Coinbase Commerce** | 즉시(Coinbase 유저) / 블록 확인 후 | O (Coinbase-Managed만) | USD + 암호화폐 | O (USDC/USD) |
| **BitPay** | 매 영업일 | **O (38개국)** | USD, EUR, GBP 등 + 15종 암호화폐 | O |
| **CoinGate** | 주 1회 (기본) | O | EUR, GBP, USD + 암호화폐 | O |
| **NOWPayments** | 즉시 (암호화폐) | O (별도 출금) | 법정화폐 + 350+ 암호화폐 | O |
| **BTCPay Server** | 즉시 (직접 지갑) | 제한적 (Strike API) | 암호화폐 위주 | X (수동) |
| **Binance Pay** | 즉시 (암호화폐) | **X** | 암호화폐 전용 | O (USDT) |
| **PayPal Crypto** | 거의 즉시 | **O (자동)** | USD (PYUSD) | O (PYUSD -> USD) |
| **Stripe Stablecoin** | Stripe 잔액 반영 | **O (자동)** | USD + USDC 선택 | O |

### 6.3 환불/분쟁 해결 비교

| 경쟁사 | 환불 방식 | 자동 환불 | 부분 환불 | 분쟁 해결 | 차지백 리스크 |
|--------|----------|----------|----------|----------|-------------|
| **Coinbase Commerce** | 가맹점 수동 (Self) / 대시보드 (Managed) / 에스크로 (Protocol) | 제한적 | O (Protocol) | 직접 해결 -> Coinbase 검토 (45영업일) | 없음 |
| **BitPay** | **대시보드 환불 + BitPay 대행** | **O** | **O** | BitPay 중재 가능 | 없음 |
| **CoinGate** | **대시보드/API 환불** | **O** | **O** | CoinGate 지원팀 | 없음 |
| **NOWPayments** | 이메일 기반 수동 | X | 제한적 | 이메일 지원 | 없음 |
| **BTCPay Server** | 대시보드 수동 환불 | X | O | 없음 (가맹점 자체) | 없음 |
| **Binance Pay** | 바이낸스 내부 이체 | 제한적 | 제한적 | 바이낸스 고객센터 | 없음 |
| **PayPal Crypto** | **가맹점 USD 기준 환불 -> PYUSD 전송** | **O** | **O** | 없음 (차지백 면제) | **없음** |
| **Stripe Stablecoin** | Stripe 대시보드 | O | O | Stripe 분쟁 시스템 | 없음 |

### 6.4 지원 암호화폐 및 네트워크 비교

| 경쟁사 | 지원 코인 수 | 주요 코인 | 지원 네트워크 | Lightning Network |
|--------|------------|---------|-------------|-----------------|
| **Coinbase Commerce** | 100+ | BTC, ETH, USDC, DAI, DOGE, LTC, BCH | Base, Ethereum, Polygon + EVM 호환 | X |
| **BitPay** | 15 | BTC, ETH, XRP, LTC, BCH, DOGE, USDC, USDT | Bitcoin, Ethereum, XRP Ledger 등 | X |
| **CoinGate** | 70+ | BTC, ETH, USDT, USDC, DOGE, LTC | 11개 (Solana, Polygon, Lightning, BSC, Arbitrum, Tron 등) | **O** |
| **NOWPayments** | **350+** | BTC, ETH, SOL, USDT, USDC + 다수 알트코인 | 다수 네트워크 | O |
| **BTCPay Server** | 120+ | BTC (핵심) + 알트코인 | Bitcoin, Lightning Network | **O** |
| **Binance Pay** | 70+ | BTC, ETH, BNB, USDT, BUSD | BSC, Ethereum 등 | X |
| **PayPal Crypto** | 100+ | 외부 지갑 100+ 코인, PYUSD 중심 | Ethereum, Solana | X |
| **Stripe Stablecoin** | 3 (스테이블코인만) | USDC, USDP, USDG | Ethereum, Solana, Polygon, Base | X |

### 6.5 가맹점 통합 난이도 비교

| 경쟁사 | 통합 난이도 | 핵심 통합 방식 | 주요 플러그인 | 개발자 문서 품질 |
|--------|-----------|-------------|-------------|---------------|
| **Coinbase Commerce** | 중 | API, 결제 링크, Shopify 네이티브 | Shopify, WooCommerce | 중 |
| **BitPay** | 중 | RESTful API, 플러그인 | Shopify, WooCommerce, Magento | **상** |
| **CoinGate** | **하** | API, 플러그인, 결제 버튼 | Shopify, WooCommerce, Prestashop, WHMCS | 상 |
| **NOWPayments** | **하** | API, 플러그인, 결제 링크, PoS | Shopify, WooCommerce, Magento, Ecwid | 상 |
| **BTCPay Server** | **상** | 셀프 호스팅 필수, API | WooCommerce, Shopify, Magento, Prestashop | 상 |
| **Binance Pay** | 중 | API, 플러그인 | Shopify, WooCommerce, WordPress | 중 |
| **PayPal Crypto** | **최하** | 기존 PayPal Checkout 자동 활성화 | 기존 PayPal 통합 모두 | 상 |
| **Stripe Stablecoin** | **최하** | 기존 Stripe 통합에 추가 옵션 | 기존 Stripe 통합 모두 | **최상** |

---

## 7. 경쟁사 포지셔닝 맵

### 축 1: 통합 용이성 (좌: 어려움 -- 우: 쉬움)
### 축 2: 법정화폐 정산 역량 (하: 약함 -- 상: 강함)

```
법정화폐 정산 역량 (강)
    ^
    |
    |   PayPal Crypto ****         Stripe Stablecoin ***
    |                        BitPay *****
    |
    |            CoinGate ****
    |
    |   Coinbase Commerce ***
    |            NOWPayments **
    |                    Binance Pay *
    |
    |   BTCPay Server *
    |
    +-------------------------------------------------> 통합 용이성 (쉬움)
  (어려움)
```

**범례**: 별(*)의 수는 해당 축에서의 상대적 강도를 나타냄

### 축 1: 수수료 경쟁력 (좌: 비쌈 -- 우: 저렴)
### 축 2: 암호화폐 지원 범위 (하: 적음 -- 상: 많음)

```
암호화폐 지원 범위 (많음)
    ^
    |
    |                              NOWPayments (350+, 0.5%)
    |
    |   BTCPay Server (120+, 0%)
    |
    |          Coinbase Commerce (100+, 1%)
    |                   PayPal Crypto (100+, 0.99%)
    |
    |     CoinGate (70+, 1%)
    |     Binance Pay (70+, 1%)
    |
    |                BitPay (15, 1-2%)
    |
    |                                         Stripe (3, 1.5%)
    |
    +-------------------------------------------------> 수수료 경쟁력 (저렴)
  (비쌈)
```

---

## 8. 차별화 기회 및 경쟁 공백 분석

### 8.1 Coinbase Commerce의 경쟁 우위 영역

| 우위 영역 | 설명 | 위협 수준 |
|----------|------|----------|
| **Base 네트워크 소유** | 자체 L2로 약 $0.01 수수료, 약 200ms 정산 -- 어떤 경쟁사도 자체 네트워크를 보유하지 않음 | 낮음 |
| **Commerce Payments Protocol** | 인가-캡처-환불을 온체인으로 구현한 유일한 오픈소스 프로토콜 | 낮음 |
| **Shopify 독점 파트너십** | 네이티브 USDC 결제로 수백만 가맹점 접근, Stripe도 Shopify 연동하나 Coinbase와는 직접 프로토콜 공동개발 관계 | 중간 (Stripe 경쟁) |
| **Coinbase 생태계** | 1억+ 사용자 내 무료 즉시 결제, 거래소/지갑/커스터디 통합 | 중간 (Binance, PayPal 대비) |

### 8.2 경쟁 공백 -- Coinbase Commerce가 취약한 영역

| 공백 영역 | 현재 상태 | 강력한 경쟁사 | 개선 필요 수준 |
|----------|----------|-------------|-------------|
| **법정화폐 정산 범위** | USD 중심, Self-Managed는 법정화폐 불가 | BitPay (38개국, USD/EUR/GBP) | **높음** |
| **환불 자동화** | Self-Managed 수동, Protocol은 에스크로 기반이나 제한적 | BitPay (대시보드 자동 환불 + 대행), CoinGate (API 환불) | **높음** |
| **유럽 시장 특화** | SEPA 정산 미지원, 유럽 규제 대응 제한적 | CoinGate (SEPA 무료, VASP 라이선스) | 중간 |
| **다양한 암호화폐** | 100+ (충분하나 최다 아님) | NOWPayments (350+) | 낮음 |
| **Lightning Network** | 미지원 | BTCPay Server, CoinGate | 중간 |
| **기존 가맹점 전환 용이성** | 별도 통합 필요 | PayPal/Stripe (기존 통합에 추가) | **높음** |

### 8.3 전략적 시사점

**단기 위협 (6-12개월)**

1. **PayPal Pay with Crypto**: 2026년 7월 프로모션 종료 후에도 1.5%로 Coinbase Commerce(1%+환전비)와 총비용이 유사하며, 4억+ 기존 사용자 기반과 무통합 활성화가 핵심 위협
2. **Stripe Stablecoin**: 1.5% 수수료로 기존 수백만 Stripe 가맹점에 스테이블코인 결제를 제로 통합 비용으로 제공, Shopify 34개국 연동

**중기 위협 (1-2년)**

1. **Circle CPN Managed Payments**: USDC 생태계의 인프라 계층을 장악하며, Coinbase가 의존하는 USDC 레일 자체를 Circle이 직접 서비스화
2. **BitPay의 규제 우위 확대**: 38개국 법정화폐 정산 네트워크는 단기간 복제 불가

**Coinbase Commerce 방어 전략 제안**

1. **환불 자동화 강화**: Commerce Payments Protocol의 에스크로 기반 환불을 가맹점 대시보드에서 원클릭으로 처리할 수 있도록 UX 개선
2. **법정화폐 정산 확대**: Coinbase-Managed 플랜의 USD 정산을 EUR/GBP/JPY 등으로 확대, SEPA 지원 추가
3. **Base 네트워크 차별화 극대화**: Base의 속도/비용 우위를 마케팅 핵심 메시지로 활용, 경쟁사 대비 정산 속도(200ms vs 영업일 단위) 강조
4. **Shopify 파트너십 심화**: Commerce Payments Protocol을 Shopify 생태계 표준으로 포지셔닝, 다른 커머스 플랫폼(BigCommerce, Magento)으로 확장

---

## 9. 종합 경쟁력 평가 매트릭스

| 평가 항목 (10점 만점) | Coinbase Commerce | BitPay | CoinGate | NOWPayments | BTCPay Server | PayPal Crypto | Stripe Stablecoin |
|---------------------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 수수료 경쟁력 | 7 | 5 | 7 | **9** | **10** | 7 | 6 |
| 법정화폐 정산 | 6 | **9** | 8 | 5 | 3 | **9** | **9** |
| 환불 자동화 | 5 | **8** | **8** | 3 | 4 | 7 | 8 |
| 암호화폐 다양성 | 7 | 4 | 6 | **10** | 8 | 7 | 2 |
| 통합 용이성 | 6 | 7 | 8 | 8 | 3 | **10** | **10** |
| 정산 속도 | **9** | 6 | 5 | 8 | **9** | 8 | 7 |
| 보안/신뢰도 | **9** | 8 | 7 | 6 | 8 | **9** | **9** |
| 생태계/네트워크효과 | **9** | 6 | 5 | 4 | 5 | **9** | 8 |
| **종합** | **7.3** | 6.6 | 6.8 | 6.6 | 6.3 | **8.3** | **7.4** |

**핵심 인사이트**: Coinbase Commerce는 기술적 우위(Base 네트워크, Commerce Payments Protocol)에서 차별화되나, PayPal과 Stripe이 기존 가맹점 기반과 통합 용이성에서 강력한 위협이 됨. 법정화폐 정산 범위와 환불 자동화가 가장 시급한 개선 영역.

---

## Sources

- [BitPay Pricing](https://www.bitpay.com/pricing)
- [BitPay Settlement Documentation](https://developer.bitpay.com/docs/settlement)
- [BitPay Refund Documentation](https://developer.bitpay.com/docs/refunding-payments)
- [BitPay Support - Fees](https://support.bitpay.com/hc/en-us/articles/203324073-What-fees-will-I-pay-to-use-BitPay-for-payment-processing)
- [CoinGate Pricing](https://coingate.com/pricing)
- [CoinGate Settlements Blog](https://coingate.com/blog/post/payouts-fiat-settlements)
- [CoinGate Supported Currencies](https://coingate.com/supported-currencies)
- [NOWPayments Pricing](https://nowpayments.io/pricing)
- [NOWPayments Refund Policy](https://nowpayments.io/help/payments/common/refund-policy)
- [NOWPayments Review 2026 - CoinGape](https://coingape.com/nowpayments-review/)
- [NOWPayments Zero Network Fees Promotion - Benzinga](https://www.benzinga.com/pressreleases/26/02/50481935/nowpayments-offers-zero-network-fees-on-usdt-trc20-payments-for-new-users)
- [BTCPay Server Official](https://btcpayserver.org/)
- [BTCPay Server Refund Documentation](https://docs.btcpayserver.org/Refund/)
- [BTCPay Server Review 2026](https://blockfinances.fr/en/btcpay-server-review)
- [PayPal Crypto Payment Solutions](https://www.paypal.com/us/business/business-types/crypto)
- [PayPal Pay with Crypto Terms](https://www.paypal.com/us/legalhub/paypal/crypto-payment-method)
- [PayPal Crypto Expansion - CoinDesk](https://www.coindesk.com/business/2025/07/28/paypay-expands-crypto-payments-for-u-s-merchants-to-cut-cross-border-fees)
- [PayPal Pay with Crypto Explained - CCN](https://www.ccn.com/education/crypto/paypal-pay-with-crypto-explained-100-coins-lower-fees-faster-checkout/)
- [Stripe Stablecoin Payments Documentation](https://docs.stripe.com/payments/stablecoin-payments)
- [Stripe Stablecoin Fees - Yahoo Finance](https://finance.yahoo.com/news/stripe-charges-1-5-stablecoin-145737023.html)
- [Stripe Shopify Stablecoin Payments](https://stripe.com/newsroom/news/shopify-stripe-stablecoin-payments)
- [Circle CPN Managed Payments Launch](https://www.circle.com/pressroom/circle-launches-cpn-managed-payments-a-full-stack-platform-for-seamless-stablecoin-settlement)
- [Circle CPN - PYMNTS](https://www.pymnts.com/cryptocurrency/2026/circle-launches-managed-payments-for-stablecoin-settlement/)
- [Binance Pay Fees](https://www.binance.com/en/support/faq/detail/6ff1944867e54b9a9576bce3109c7f7a)
- [MoonPay Review 2026 - CoinSpot](https://coinspot.io/en/reviews/moonpay/)
- [Crypto Payment Gateway 2026 Buyer's Guide](https://westafricatradehub.com/crypto/best-crypto-payment-gateway-2026-buyers-guide-to-fees-settlement-and-coin-support/)
