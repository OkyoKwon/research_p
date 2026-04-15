# 경쟁사 심층 분석 -- Stripe 크립토 결제 서비스

## 분석 개요

- **분석 대상**: Stripe 크립토 결제 서비스 (Stablecoin Payments, x402, MPP, Onramp, Pay with Crypto) 경쟁사
- **분석 일시**: 2026-04-15
- **선행 분석 참조**: 시장 현황 분석 (`01_Jr4DtyE94kyvJZ0stg_SY_output.md`)
- **주요 참조 소스**: 각 경쟁사 공식 문서, PYMNTS, The Block, CoinDesk, Crossmint, WorkOS Blog, Blockfinances, Messari, 각사 뉴스룸

---

## 1. 경쟁 구도 요약

### 1.1 경쟁 지형

| 항목 | 상세 |
|------|------|
| 직접 경쟁사 수 | 5개 (PayPal Crypto, Coinbase Commerce, Binance Pay, BitPay, CoinGate) |
| 간접 경쟁사 수 | 5개 (NOWPayments, Solana Pay, MoonPay Commerce, Circle CPN, Crypto.com Pay) |
| 시장 지배자 | Stripe (기존 결제 인프라 + 크립토 통합), PayPal (자체 스테이블코인 PYUSD + 4.3억 활성 계정) |
| 신흥 도전자 | Coinbase Commerce (Commerce Payments Protocol + Shopify 연동), Circle CPN (2026.04 Managed Payments 론칭) |
| 머신 결제 경쟁 | x402 (Coinbase), MPP (Stripe/Tempo), ACP (OpenAI/Stripe), AP2 (Google), UCP (Google/Shopify), TAP (Visa) |

### 1.2 전략적 포지셔닝 분류

```
[기존 결제 인프라 통합]                    [크립토 네이티브]

  Stripe  -----  PayPal              Coinbase Commerce
     |                |                      |
  Circle CPN     Crypto.com Pay        Solana Pay
                                             |
                                       NOWPayments
                                             |
  BitPay  ----  CoinGate              MoonPay Commerce

[결제 게이트웨이 전문]                  [프로토콜/인프라]
```

---

## 2. 직접 경쟁사 심층 분석

### 2.1 PayPal Crypto (PYUSD / Pay with Crypto)

#### 기업 프로파일

| 항목 | 상세 |
|------|------|
| 설립 | 1998년 (크립토 결제: 2021년~, PYUSD: 2023년 8월) |
| 규모 | 시가총액 약 800억 달러, 연간 결제 볼륨 5,600억 달러+, 활성 계정 4.3억+ |
| 투자/인프라 | 자체 스테이블코인 PYUSD 발행 (Paxos 신탁), Solana/Ethereum 지원 |
| 타깃 고객 | 기존 PayPal 가맹점 (소규모~대규모), 일반 소비자 |
| 최근 동향 | 2025.07 Pay with Crypto 대규모 확장, 100+ 토큰 지원, Solana PYUSD 결제 |

#### 결제 - 정산 - 환불 프로세스

| 단계 | 상세 |
|------|------|
| **결제** | 소비자가 PayPal 앱 내 크립토/PYUSD 잔고로 결제 -> PayPal이 자동으로 법정화폐 전환 -> 가맹점에 USD 정산 |
| **수수료** | **0.99%** (프로모션, 2026.07.31까지) / 이후 **1.5%** |
| **지원 코인** | 100+ 토큰 (BTC, ETH, SOL, PYUSD, USDC 등) |
| **정산 통화** | USD (법정화폐 자동 전환) |
| **정산 속도** | 수 분 내 (기존 T+2 대비 크게 단축), PYUSD는 즉시 $1:1 전환 |
| **정산 이자** | 잔고 대비 4% APY 제공 |
| **환불** | USD 기준 환불 금액 지정 -> PayPal이 PYUSD로 전환하여 고객 월렛 반환; 네트워크 수수료 가맹점 부담 |
| **분쟁/차지백** | **셀러 보호(Seller Protection) 미적용** -- 크립토 결제는 PayPal 분쟁 시스템 제외 |
| **지원 국가** | 가맹점: 미국만 (현재) / 소비자: PayPal 지원 국가 |

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **강점** | 4.3억 활성 계정 기반 즉각적 도달력; 자체 스테이블코인 PYUSD; 100+ 토큰 지원 폭넓은 코인 커버리지; 프로모션 0.99% 저렴한 수수료; 잔고 4% APY |
| **약점** | 셀러 보호 미적용으로 가맹점 리스크; 크립토 네이티브 개발자 경험 부족; PayPal 계정 필수 (비수탁 월렛 직접 지원 안 함); 환불 시 네트워크 수수료 가맹점 전가 |
| **기회** | PYUSD 크로스보더 결제 확장; Solana 생태계 결제 파트너십 확대; AI 에이전트 결제 "Agent Ready" 프로토콜 론칭 |
| **위협** | Stripe의 기존 가맹점 네트워크 장악력; PYUSD 채택률 불확실; 프로모션 종료 후 수수료 동일화(1.5%) |

---

### 2.2 Coinbase Commerce (Commerce Payments Protocol / Base Pay)

#### 기업 프로파일

| 항목 | 상세 |
|------|------|
| 설립 | 2018년 (Commerce), 2025년 중반 Commerce Payments Protocol 론칭 |
| 규모 | Coinbase 시가총액 약 500억 달러+, 1억+ 인증 사용자 |
| 인프라 | Base L2 (Ethereum), Commerce Payments Protocol (온체인 authorize-capture-refund) |
| 타깃 고객 | 크립토 네이티브 비즈니스, Shopify 가맹점, Web3 서비스 |
| 최근 동향 | Shopify 전체 가맹점 USDC 결제 지원, Coinbase Business로 통합 예정, x402 프로토콜 주도 |

#### 결제 - 정산 - 환불 프로세스

| 단계 | 상세 |
|------|------|
| **결제** | 소비자가 Coinbase 월렛 또는 외부 월렛으로 USDC/BTC/ETH 등 결제 -> Base L2에서 ~200ms 내 확정 |
| **수수료** | **1%** (업계 최저 수준); Coinbase 사용자 -> Coinbase 가맹점 간 전송은 **무료** (오프체인) |
| **지원 코인** | USDC, BTC, ETH, DEGEN, cbBTC 등 7+ 코인 (2026.01 확장) |
| **정산 통화** | **크립토 수취가 기본** (법정화폐 자동 전환 없음); Coinbase Business 전환 시 법정화폐 캐시아웃 가능 예정 |
| **정산 속도** | Base L2 기반 서브-세컨드 (~200ms), 네트워크 수수료 약 $0.01 |
| **환불** | Commerce Payments Protocol에 온체인 환불 기능 내장; 다만 현재 대시보드에서 직접 환불 미지원 -> 수동 프로세스 필요; 높은 반품률 사업에는 운영 부담 |
| **분쟁/차지백** | **없음** -- 온체인 결제 특성상 차지백 불가 (가맹점 유리) |
| **지원 국가** | 가맹점: 100+ 개국 (OFAC 제재국 제외) / 소비자: 글로벌 |

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **강점** | 1% 최저 수수료; Base L2 서브-세컨드 정산; Commerce Payments Protocol (authorize-capture-refund 온체인 구현); Shopify 통합; x402 프로토콜 주도권; Coinbase 내부 전송 무료 |
| **약점** | 법정화폐 자동 정산 미지원 (가맹점이 크립토 노출); 환불 프로세스 수동적; 크립토에 익숙하지 않은 가맹점 진입 장벽; Coinbase Business 전환 과도기 |
| **기회** | Shopify 수백만 가맹점 채널; x402 표준화 주도; Base L2 생태계 확장; Commerce Payments Protocol의 DeFi 결합 |
| **위협** | Stripe의 법정화폐 자동 정산 편의성; PayPal의 소비자 기반 규모; 법정화폐 정산 미지원으로 전통 가맹점 이탈 |

---

### 2.3 BitPay

#### 기업 프로파일

| 항목 | 상세 |
|------|------|
| 설립 | 2011년 (크립토 결제 게이트웨이 선구자) |
| 규모 | 비상장, 누적 투자 약 7,000만 달러 |
| 인프라 | 자체 결제 처리 인프라, BitPay 월렛, BitPay 카드 |
| 타깃 고객 | 중소~대형 가맹점, 고위험 산업 포함 |
| 최근 동향 | 10년+ 운영 경험, 다양한 코인/정산 옵션, 기업 결제 수요 안정적 |

#### 결제 - 정산 - 환불 프로세스

| 단계 | 상세 |
|------|------|
| **결제** | 가맹점이 BitPay 인보이스 생성 -> 소비자가 월렛으로 지불 -> BitPay가 수취 후 변환 |
| **수수료** | **1% + $0.25** (건당) |
| **지원 코인** | BTC, ETH, XRP, DOGE, LTC, SHIB, USDC, BUSD, GUSD 등 16+ 코인 |
| **정산 통화** | USD, EUR, GBP 등 법정화폐 또는 BTC/BCH 크립토 선택 가능 |
| **정산 속도** | T+2 영업일 (은행 입금), 최소 정산 $20, 매 영업일 자동 정산 |
| **환불** | BitPay 중재로 크립토 환불 가능; 채굴자 수수료(miner fee)는 가맹점 부담; BitPay 재량에 따라 처리 |
| **분쟁/차지백** | **공식 차지백 없음**; 고객 불만 접수 시 가맹점에 전달하여 해결 요구; 과도한 불만 시 계정 해지 가능 |
| **지원 국가** | 가맹점: 230+ 개국 / 정산: USD, EUR, GBP 등 주요 법정화폐 |

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **강점** | 10년+ 운영 실적과 브랜드 신뢰; 법정화폐 자동 정산 지원; 광범위한 코인 지원; 230+ 개국 서비스; BitPay 카드로 즉시 사용 가능 |
| **약점** | 수수료 구조 복잡 (1% + $0.25); UI/UX 노후화; 스테이블코인 특화 기능 부족; API 개발자 경험이 Stripe 대비 열위; 환불 프로세스가 BitPay 재량에 의존 |
| **기회** | 레거시 크립토 결제 시장의 안정적 점유; 고위험 산업 틈새시장 |
| **위협** | Stripe/PayPal의 기존 가맹점 네트워크 전환 유도; Coinbase Commerce의 낮은 수수료; 기술 혁신 속도 뒤처짐 |

---

### 2.4 Binance Pay

#### 기업 프로파일

| 항목 | 상세 |
|------|------|
| 설립 | 2021년 (Binance Pay) |
| 규모 | Binance 거래소 세계 최대, 1.8억+ 사용자 |
| 인프라 | Binance 거래소 생태계, 폐쇄형 루프 결제 |
| 타깃 고객 | Binance 사용자 기반 가맹점, 동남아/아프리카 등 신흥시장 |
| 최근 동향 | 남아프리카 65만+ 가맹점 확장, 100+ 크립토 지원 |

#### 결제 - 정산 - 환불 프로세스

| 단계 | 상세 |
|------|------|
| **결제** | Binance 앱 사용자가 QR 코드 또는 링크로 결제 -> Binance 내부 장부 이전 |
| **수수료** | **1% MDR** (가맹점); 사용자 간 전송은 **무료**; 가스비 없음 |
| **지원 코인** | 100+ 크립토 (USDT, USDC, BTC, BNB 등) |
| **정산 통화** | **크립토만 정산** -- 법정화폐 직접 은행 입금 불가; Binance 거래소에서 별도 환전 필요 |
| **정산 속도** | 즉시 (내부 장부 이전) |
| **Payout 수수료** | 0.80% (캡: $5) -- 외부 크립토 전송 시 |
| **환불** | Binance Pay 내 환불 기능 제한적; 가맹점 직접 처리 |
| **분쟁/차지백** | **없음** |
| **지원 국가** | Binance 서비스 가능 국가 (미국 제한적, 유럽 일부 제한) |

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **강점** | 1.8억 사용자 기반; 100+ 코인 지원; 내부 전송 무료 + 즉시 정산; 신흥시장 강점 (남아프리카 등) |
| **약점** | 법정화폐 정산 미지원 (가맹점 운영 부담); 폐쇄형 생태계 (Binance 사용자만); 미국/EU 규제 리스크; 환불/분쟁 시스템 미비 |
| **기회** | 신흥시장 확장; BNB 체인 DeFi 결합 |
| **위협** | 규제 강화로 서비스 지역 축소; Stripe/PayPal의 법정화폐 정산 편의성과 경쟁 불가 |

---

### 2.5 CoinGate

#### 기업 프로파일

| 항목 | 상세 |
|------|------|
| 설립 | 2014년 (리투아니아) |
| 규모 | 중소 규모, MiCA 라이선스 보유 (2025.12 취득 -- 리투아니아 370개 크립토 기업 중 3곳만 생존) |
| 인프라 | 자체 결제 게이트웨이, EU 규제 준수 |
| 타깃 고객 | EU 중심 중소 가맹점, iGaming 산업 |
| 최근 동향 | MiCA 라이선스 취득, 2026년 실시간 처리/자동 정산 로드맵 |

#### 결제 - 정산 - 환불 프로세스

| 단계 | 상세 |
|------|------|
| **결제** | 가맹점이 CoinGate 체크아웃 생성 -> 소비자가 70+ 크립토로 결제 |
| **수수료** | **1%** (결제 처리); 환전 수수료 약 1% 추가; 환불 시 통화 상이하면 +0.1% |
| **지원 코인** | 70+ 크립토 (BTC, ETH, LTC, USDT, USDC 등) |
| **정산 통화** | EUR, GBP, USD 또는 크립토 선택 가능 (유연한 혼합 정산) |
| **정산 속도** | 즉시 정산 (법정화폐 전환 포함) |
| **환불** | 크립토 환불 지원 (업계 희소 기능); 소액 고정 수수료 |
| **분쟁/차지백** | **없음** |
| **지원 국가** | 180+ 개국 정산 지원; EU MiCA 완전 준수 |

#### SWOT 분석

| 구분 | 내용 |
|------|------|
| **강점** | MiCA 라이선스 (EU 규제 준수 최상위); 법정화폐 즉시 정산; 유연한 정산 혼합 (법정화폐+크립토); 크립토 환불 기능; 180+ 개국 |
| **약점** | 브랜드 인지도 낮음; 개발자 생태계 규모 작음; 대규모 가맹점 사례 부족 |
| **기회** | EU MiCA 규제로 경쟁사 탈락 -> 시장 점유율 확대; iGaming 등 틈새시장 |
| **위협** | Stripe/PayPal의 EU 진출; 대형 플랫폼 대비 기술/규모 열위 |

---

## 3. 간접 경쟁사 분석

### 3.1 NOWPayments

| 항목 | 상세 |
|------|------|
| **수수료** | 0.5% (업계 최저) + 자동 환전 시 추가 0.5% |
| **지원 코인** | 350+ 크립토 (최다 지원) |
| **정산** | 크립토 정산만 지원 (법정화폐 직접 정산 불가, 환전 파트너 필요); 자동 환전으로 원하는 크립토로 수취 가능 |
| **환불** | 별도 환불 시스템 미공개 |
| **지원 국가** | 글로벌 (규제 제한 최소) |
| **특징** | 최저 수수료 + 최다 코인 지원; 커뮤니티 중심; WooCommerce/Shopify 등 플러그인 지원 |

### 3.2 Solana Pay

| 항목 | 상세 |
|------|------|
| **수수료** | 사실상 무료 (~$0.00025/건, 서브-센트) |
| **지원 코인** | SOL, USDC, USDT 등 Solana 생태계 토큰 |
| **정산** | P2P 직접 전송 (가맹점 월렛에 즉시 입금); 법정화폐 전환은 가맹점이 별도 처리 |
| **환불** | 프로토콜 수준 환불 미지원; 가맹점이 직접 온체인 전송으로 환불 |
| **지원 국가** | 글로벌 (탈중앙화 프로토콜) |
| **특징** | 400ms 내 확정; 65,000 TPS; Visa/PayPal/Stripe 모두 Solana 통합; 2026년 분기 $2조+ 이체량 |

### 3.3 MoonPay Commerce (구 Helio)

| 항목 | 상세 |
|------|------|
| **수수료** | 0.25% ~ 2.00% (기능별 차등); 고위험 플랫폼 최소 2% |
| **지원 코인** | USDC, USDT, ETH, SOL, BTC |
| **정산** | 비수탁(non-custodial) P2P 결제 -- 가맹점 월렛에 즉시 입금; 법정화폐 정산 옵션 제공 |
| **환불** | 차지백 없음; 환불은 가맹점 직접 처리 |
| **지원 국가** | 글로벌, 6,000+ 비즈니스 이용 |
| **특징** | 2025.01 MoonPay가 Helio $1.75억 인수; Shopify/Ledger/CoinMarketCap 통합; 온/오프램프 + 결제 통합 플랫폼 |

### 3.4 Circle CPN (Circle Payments Network)

| 항목 | 상세 |
|------|------|
| **수수료** | 0% 처리 수수료 (USDC 직접 사용 시); CPN 플랫폼 수수료는 미공개 |
| **지원 코인** | USDC (Circle 발행) |
| **정산** | CPN Managed Payments (2026.04 론칭) -- Circle이 민팅/소각/정산/컴플라이언스 전체 관리; 금융기관이 법정화폐만으로 상호작용 가능 |
| **환불** | 기관 레벨 정산 -- 환불은 참여 금융기관 정책에 따름 |
| **지원 국가** | 글로벌 (기관 파트너 네트워크 통해) |
| **특징** | USDC 발행사로서 $70조+ 온체인 정산 실적; Mastercard 파트너십; 은행/PSP가 크립토 인프라 없이 스테이블코인 정산 가능 |

### 3.5 Crypto.com Pay

| 항목 | 상세 |
|------|------|
| **수수료** | 0% 거래 수수료 + **0.5% 정산 수수료**만 부과 |
| **지원 코인** | Crypto.com 보유 전체 크립토 + 스테이블코인 |
| **정산** | 법정화폐 또는 크립토 정산 선택; 법정화폐 정산 시 국제 송금 수수료 추가 가능 |
| **환불** | 가맹점이 부분/전체 환불 가능; Crypto.com 앱 사용자는 자동 반환; 외부 월렛 사용자는 이메일로 환불 클레임 링크 발송 |
| **지원 국가** | Shopify 전체 가맹점 지원, Crypto.com 서비스 국가 |
| **특징** | Stripe x Crypto.com 파트너십 (2026.01); Shopify 통합; 체계적 환불 프로세스 보유 |

---

## 4. 핵심 비교표

### 4.1 수수료 비교

| 경쟁사 | 거래 수수료 | 정산 수수료 | 실질 총비용 | 비고 |
|--------|-----------|-----------|-----------|------|
| **Stripe** | **1.5%** | 포함 | **1.5%** | 법정화폐 자동 정산 포함 |
| PayPal | 0.99% (프로모션) / 1.5% | 포함 | 0.99~1.5% | 2026.07까지 프로모션; 이후 동일 |
| Coinbase Commerce | 1% | 없음 (크립토 수취 시) | 1% | 법정화폐 전환 시 추가 비용 발생 |
| BitPay | 1% + $0.25 | 포함 | ~1.25% (평균) | 건당 고정비 포함 |
| Binance Pay | 1% | 0.80% (외부 전송) | 1~1.8% | 법정화폐 정산 미지원 |
| CoinGate | 1% | 환전 1% | ~2% | 법정화폐 전환 포함 시 |
| NOWPayments | 0.5% | 환전 0.5% | 0.5~1% | 법정화폐 직접 정산 불가 |
| Solana Pay | ~0% ($0.00025) | 없음 | ~0% | 법정화폐 전환 별도 |
| MoonPay Commerce | 0.25~2% | 없음 | 0.25~2% | 기능별 차등 |
| Circle CPN | 0% | 미공개 | 미공개 | 기관 대상, 고볼륨 |
| Crypto.com Pay | 0% | 0.5% | 0.5% | 최저 실질 비용군 |

> **인사이트**: Stripe의 1.5%는 "법정화폐 자동 정산 포함" 기준으로는 합리적이나, 순수 온체인 비용(~$0.0002) 대비 750배 이상의 마진이므로 업계 비판이 존재한다. PayPal 프로모션 종료 후에는 Stripe와 동일한 1.5%가 되어 수수료 차별화가 사라진다.

---

### 4.2 정산 방식 비교

| 경쟁사 | 법정화폐 자동 정산 | 정산 속도 | 정산 통화 | 가맹점 크립토 노출 |
|--------|------------------|----------|----------|------------------|
| **Stripe** | **지원** | T+2 (카드와 동일) | USD | **없음** (완전 차폐) |
| PayPal | **지원** | 수 분 내 | USD | **없음** |
| Coinbase Commerce | **미지원** (예정) | 즉시 (~200ms) | 크립토 | **있음** |
| BitPay | **지원** | T+2 | USD/EUR/GBP | **없음** (선택 시) |
| Binance Pay | **미지원** | 즉시 (내부) | 크립토만 | **있음** |
| CoinGate | **지원** | 즉시 | EUR/GBP/USD | **없음** (선택 시) |
| NOWPayments | **미지원** | 즉시 | 크립토만 | **있음** |
| Solana Pay | **미지원** | 즉시 (~400ms) | 크립토 | **있음** |
| MoonPay Commerce | **부분 지원** | 즉시 | 크립토/법정화폐 | **선택 가능** |
| Circle CPN | **지원** (기관) | 미공개 | USD (법정화폐) | **없음** |
| Crypto.com Pay | **지원** | 미공개 | 법정화폐/크립토 | **선택 가능** |

> **인사이트**: Stripe의 핵심 우위는 "가맹점이 크립토를 전혀 만지지 않는다"는 점이다. 법정화폐 자동 정산을 지원하는 경쟁사는 Stripe, PayPal, BitPay, CoinGate, Circle CPN, Crypto.com Pay 6곳뿐이며, 이 중 기존 결제 인프라와 통합 관리되는 곳은 Stripe과 PayPal 둘뿐이다.

---

### 4.3 환불/분쟁 해결 비교

| 경쟁사 | 환불 지원 | 환불 방식 | 분쟁/차지백 | 소비자 보호 수준 |
|--------|----------|----------|-----------|----------------|
| **Stripe** | **지원** | 스테이블코인 -> 원래 월렛 (온체인) | **미지원** | 낮음 |
| PayPal | **지원** | USD -> PYUSD 전환 -> 월렛; 네트워크 수수료 가맹점 부담 | **미지원** (셀러 보호 제외) | 낮음 |
| Coinbase Commerce | **부분** | 수동 온체인 전송; 대시보드 미지원 | **없음** | 매우 낮음 |
| BitPay | **지원** (재량) | BitPay 중재 크립토 환불; 마이너 수수료 가맹점 부담 | 불만 접수 -> 가맹점 전달 | 낮음 |
| Binance Pay | **제한적** | 가맹점 직접 처리 | **없음** | 매우 낮음 |
| CoinGate | **지원** | 크립토 환불 (업계 희소); 소액 수수료 | **없음** | 중간 |
| NOWPayments | **미공개** | 미공개 | **없음** | 매우 낮음 |
| Solana Pay | **미지원** | 가맹점 직접 온체인 전송 | **없음** | 매우 낮음 |
| MoonPay Commerce | **제한적** | 가맹점 직접 처리 | **없음** | 낮음 |
| Circle CPN | **기관 정책** | 참여 기관별 상이 | 기관 정책 | 기관 수준 |
| Crypto.com Pay | **지원** | 앱 사용자 자동 반환 / 외부 월렛 이메일 클레임 | **없음** | **중상** (가장 체계적) |

> **인사이트**: 크립토 결제의 구조적 한계로 모든 경쟁사가 전통적 차지백/분쟁 시스템을 지원하지 않는다. 이는 가맹점에게는 차지백 사기 제거라는 이점이지만, 소비자 보호 관점에서는 공통된 약점이다. Crypto.com Pay가 가장 체계적인 환불 프로세스를 보유하고 있으며, CoinGate의 크립토 환불 기능은 업계에서 드문 차별점이다.

---

### 4.4 가맹점 통합 난이도 비교

| 경쟁사 | 기존 인프라 통합 | 코드 변경 규모 | 개발자 경험 | 통합 시간 |
|--------|----------------|--------------|-----------|----------|
| **Stripe** | **기존 Stripe 대시보드/API에 플러그인** | 수 줄의 코드 (PaymentIntent에 stablecoin 추가) | **최상** (기존 Stripe 패러다임 동일) | 수 분 (기존 가맹점) |
| PayPal | 기존 PayPal 결제에 통합 | 최소 변경 (기존 PayPal 가맹점) | 상 | 수 시간 |
| Coinbase Commerce | 별도 통합 필요 | 중간 규모 | 중상 (크립토 지식 필요) | 수 시간~1일 |
| BitPay | 별도 API 통합 | 중간 규모 | 중 | 1~2일 |
| Binance Pay | Binance API 별도 통합 | 중간 규모 | 중 | 1~2일 |
| CoinGate | 플러그인 기반 (WooCommerce 등) | 최소 (플러그인) | 중상 | 수 시간 |
| NOWPayments | 플러그인 기반 | 최소 (플러그인) | 중 | 수 시간 |
| Solana Pay | SDK 직접 통합 | 중~대규모 | 중하 (블록체인 지식 필수) | 수 일 |
| MoonPay Commerce | 플러그인/API | 최소~중간 | 중상 | 수 시간 |
| Circle CPN | 기관급 API | 대규모 | 상 (기관 대상) | 수 주 |
| Crypto.com Pay | Shopify 플러그인/API | 최소~중간 | 중상 | 수 시간 |

> **인사이트**: Stripe의 결정적 우위는 **기존 수백만 Stripe 가맹점이 코드 몇 줄만 추가하면 크립토 결제를 수취**할 수 있다는 점이다. 새로운 대시보드, 새로운 정산 계정, 새로운 API를 배울 필요가 없다. PayPal도 유사한 이점을 가지지만, 개발자 친화적 API 품질에서 Stripe에 뒤진다.

---

### 4.5 지원 국가 및 규제 비교

| 경쟁사 | 가맹점 수취 국가 | 소비자 결제 국가 | 주요 규제 준수 |
|--------|----------------|----------------|--------------|
| **Stripe** | 미국만 (현재) | 글로벌 | GENIUS Act 준수; 가맹점 확대 예정 |
| PayPal | 미국만 (현재) | PayPal 지원국 | GENIUS Act 준수 |
| Coinbase Commerce | 100+ 개국 | 글로벌 | OFAC 제재국 제외 |
| BitPay | 230+ 개국 | 글로벌 | MSB 라이선스 (미국), 다국적 |
| Binance Pay | Binance 허용국 | Binance 허용국 | 국가별 상이, 미국/일부 EU 제한 |
| CoinGate | 180+ 개국 | 글로벌 | **MiCA 라이선스** (EU 최상위) |
| NOWPayments | 글로벌 | 글로벌 | 최소 규제 (리스크) |
| Solana Pay | 글로벌 (탈중앙화) | 글로벌 | 프로토콜 수준 (가맹점 책임) |
| MoonPay Commerce | 글로벌 | 글로벌 | 다수 국가 라이선스 |
| Circle CPN | 기관 파트너 국가 | 글로벌 | 미국 MSB, EU 라이선스, 글로벌 컴플라이언스 |
| Crypto.com Pay | Crypto.com 서비스국 | Crypto.com 서비스국 | 다국적 라이선스 |

> **인사이트**: Stripe의 가장 큰 약점은 **현재 미국 가맹점만 수취 가능**하다는 지역 제한이다. BitPay(230+개국), CoinGate(180+개국), Coinbase Commerce(100+개국)가 글로벌 커버리지에서 크게 앞선다. Stripe의 Stablecoin Financial Accounts는 101개국을 지원하므로, 향후 결제 수취 국가 확대가 핵심 과제이다.

---

## 5. 머신/AI 에이전트 결제 경쟁 비교 (x402 vs 경쟁 프로토콜)

### 5.1 주요 에이전트 결제 프로토콜 비교

2026년 초, 90일 이내에 모든 주요 결제 플랫폼이 AI 에이전트 결제 프로토콜을 론칭하며 "에이전트 결제 전쟁"이 본격화되었다.

| 프로토콜 | 주도 기업 | 레이어 | 결제 모델 | 정산 방식 | 주요 파트너 |
|---------|----------|--------|----------|----------|-----------|
| **x402** | Coinbase | HTTP 네이티브 | 요청당 즉시 결제 (402 상태 코드) | 온체인 즉시 (USDC on Base) | Cloudflare, Google, Visa, Stripe |
| **MPP** | Stripe/Tempo | 세션 기반 | 사전 승인 -> 스트리밍 마이크로페이먼트 -> 배치 정산 | 온체인 배치 (Tempo L1) | Visa, Zodia, Paradigm |
| **ACP** | OpenAI/Stripe | 체크아웃 플로우 | 에이전트-가맹점 간 표준 체크아웃 | Stripe 기존 인프라 | Shopify, Salesforce, PayPal, URBN |
| **AP2** | Google | 인증/신뢰 | 에이전트 지출 권한 관리 (감사 추적, 한도 설정) | 기존 결제 레일 활용 | Amex, Coinbase, Mastercard, 60+ 파트너 |
| **UCP** | Google/Shopify | 커머스 인프라 | 기존 커머스 인프라(장바구니, 체크아웃, 반품)를 에이전트 네이티브로 | 기존 커머스 인프라 | Shopify, 20+ 파트너 |
| **TAP** | Visa | 카드 네트워크 | 기존 카드 인프라 위 에이전트 결제 | Visa 네트워크 | Visa 가맹점 전체 |
| **Agent Ready** | PayPal | PayPal 생태계 | PayPal 결제 인프라 위 에이전트 | PayPal/PYUSD | PayPal 가맹점 |

### 5.2 Stripe의 포지셔닝 (x402 + MPP 이중 전략)

Stripe는 독특하게 **두 개의 프로토콜에 동시 참여**하고 있다:

| 관점 | x402 참여 | MPP 자체 운영 |
|------|----------|-------------|
| **역할** | x402 Foundation 멤버, Base 기반 통합 | Tempo L1과 공동 개발, 주도 |
| **결제 수단** | USDC on Base (크립토 전용) | 스테이블코인 + 카드 + BTC Lightning (멀티) |
| **정산** | 온체인 즉시 | 배치 정산, 기존 Stripe 잔고 통합 |
| **유스케이스** | 단건 API 호출, 데이터 구매 | 대량 마이크로페이먼트, 장기 세션 |
| **전략적 의도** | 크립토 네이티브 에이전트 생태계 접근 | 기존 가맹점 + 에이전트 경제 브릿지 |

### 5.3 프로토콜 간 상호보완성

실제 운영에서 이 프로토콜들은 경쟁보다 **계층적 상호보완** 관계이다:

```
[인증/신뢰 계층]     AP2 (Google) -- 에이전트 지출 권한 관리
        |
[커머스 계층]        ACP (OpenAI/Stripe) / UCP (Google/Shopify) -- 체크아웃 플로우
        |
[결제 실행 계층]     x402 (Coinbase) / MPP (Stripe/Tempo) -- 실제 자금 이동
        |
[네트워크 계층]      TAP (Visa) / Agent Ready (PayPal) -- 기존 결제 네트워크 활용
```

> **인사이트**: Stripe는 ACP(커머스 계층) + MPP(결제 실행 계층)에서 핵심 위치를 차지하며, x402에도 참여하여 크립토 네이티브 생태계와의 접점을 유지한다. 이 다층적 포지셔닝이 Stripe의 에이전트 결제 전략의 핵심이다.

---

## 6. 경쟁 포지셔닝 맵

### 6.1 축: 법정화폐 통합 수준 vs 크립토 네이티브 수준

```
                    법정화폐 통합 수준 (높음)
                           |
                   Stripe  |  PayPal
                     *     |    *
                           |
              Circle CPN * |        * BitPay
                           |
         CoinGate *        |
                           |
    ───────────────────────+───────────────────────
    크립토 네이티브 (낮음)  |           크립토 네이티브 (높음)
                           |
           MoonPay *       |     * Crypto.com Pay
                           |
                           |  * Coinbase Commerce
                           |
              NOWPayments *|        * Binance Pay
                           |
                    * Solana Pay
                           |
                    법정화폐 통합 수준 (낮음)
```

### 6.2 축: 가맹점 규모/통합 용이성 vs 수수료 경쟁력

```
                    수수료 낮음 (저렴)
                           |
              Solana Pay * |
                           |
           NOWPayments *   |   * Crypto.com Pay
                           |
              Coinbase *   |        * CoinGate
                           |
    ───────────────────────+───────────────────────
    소규모/전문 가맹점      |           대규모/기존 가맹점
                           |
          MoonPay *        |    * PayPal (프로모션)
                           |
           Binance Pay *   |       * BitPay
                           |
                           |   * Stripe
                           |   * PayPal (정가)
                           |
                    수수료 높음 (비쌈)
```

---

## 7. Stripe의 구조적 우위와 열위

### 7.1 구조적 우위

| 우위 요소 | 상세 |
|----------|------|
| **기존 가맹점 네트워크 락인** | 수백만 Stripe 가맹점이 코드 몇 줄로 크립토 결제 추가 가능. 경쟁사는 "새로운 결제 시스템 도입"이지만, Stripe는 "기존 시스템에 체크박스 추가" 수준 |
| **법정화폐 완전 차폐** | 가맹점이 크립토를 전혀 이해/관리할 필요 없음. Coinbase Commerce, Binance Pay, NOWPayments, Solana Pay는 가맹점에 크립토 노출 |
| **통합 대시보드** | 카드 결제, ACH, 스테이블코인 결제가 하나의 Stripe 대시보드에서 통합 관리. 경쟁사는 별도 시스템 |
| **수직 통합 (Bridge + Tempo)** | 스테이블코인 발행(Bridge) -> 블록체인(Tempo) -> 결제 처리(Stripe) 풀스택 보유. 경쟁사 중 이 수준의 수직 통합은 없음 |
| **에이전트 결제 다층 전략** | ACP + MPP + x402 세 프로토콜에 동시 참여. 어떤 표준이 승리하든 Stripe가 결제 레이어에 존재 |
| **구독 결제 지원** | 스마트 컨트랙트 기반 반복 결제 (매 트랜잭션 재서명 불필요). 크립토 구독 결제를 지원하는 경쟁사는 극소수 |
| **10만+ 가맹점 온보딩 실적** | 2024년 론칭 이후 10만+ 가맹점 온보딩, 카드 결제 대비 12% 높은 전환율 보고 |

### 7.2 구조적 열위

| 열위 요소 | 상세 |
|----------|------|
| **수수료 프리미엄** | 1.5%는 온체인 비용 대비 750배+ 마진. PayPal 프로모션(0.99%), Coinbase(1%), NOWPayments(0.5%), Solana Pay(~0%)에 열위. 다만 법정화폐 정산 포함 가격이므로 단순 비교는 부적절 |
| **지역 제한** | 가맹점 수취는 미국만 가능. BitPay(230+개국), CoinGate(180+개국), Coinbase(100+개국)에 크게 뒤짐 |
| **분쟁 해결 부재** | 기존 Stripe 카드 결제의 강력한 Disputes 시스템이 크립토에는 미적용. 이는 업계 공통 한계이지만, 기존 Stripe 가맹점 기대 수준과의 갭 존재 |
| **코인 지원 범위** | USDC, USDP, USDG 등 스테이블코인 위주. PayPal(100+토큰), NOWPayments(350+), Binance Pay(100+)에 비해 제한적 |
| **크립토 네이티브 개발자 거부감** | 중앙화된 인프라에 대한 크립토 커뮤니티의 본질적 반발; 탈중앙화 프로토콜(Solana Pay 등) 선호 세력 존재 |
| **정산 속도** | T+2 영업일은 기존 카드 결제와 동일하지만, Coinbase Commerce(~200ms), Solana Pay(~400ms), Binance Pay(즉시) 대비 느림 |

---

## 8. 차별화 기회 및 경쟁 공백

### 8.1 경쟁 공백 지점

| 공백 | 현황 | 기회 |
|------|------|------|
| **환불/분쟁 통합 시스템** | 모든 경쟁사가 전통적 차지백 미지원; Coinbase Commerce Payments Protocol만 온체인 환불 시도 중 | 스마트 컨트랙트 기반 에스크로 + 분쟁 중재 시스템을 최초 구현하는 플레이어가 소비자 보호 표준 선점 가능 |
| **글로벌 법정화폐 자동 정산** | Stripe/PayPal은 미국만, BitPay/CoinGate는 법정화폐 정산은 글로벌이나 API 품질 열위 | 글로벌 법정화폐 자동 정산 + Stripe급 개발자 경험을 결합한 플레이어 부재 |
| **즉시 정산 + 법정화폐 전환** | Coinbase/Solana는 즉시지만 크립토, Stripe/PayPal은 법정화폐지만 T+2 | "즉시 법정화폐 정산"은 아직 어느 경쟁사도 완성하지 못한 영역 |
| **원클릭 크립토 결제 (월렛리스)** | 대부분 크립토 월렛 보유 전제; PayPal만 기존 계정으로 크립토 결제 가능 | 월렛 없이 크립토의 저비용 장점을 누리는 결제 경험 (Stripe의 Pay with Crypto + Crypto.com 방향) |

### 8.2 Stripe의 전략적 권고

1. **지역 확대 최우선**: 미국 전용 제한을 EU, 영국, 일본 등 주요 시장으로 조기 확대해야 함. Stablecoin Financial Accounts(101개국)의 인프라를 결제 수취에 활용 가능
2. **실시간 정산 도입**: Tempo 블록체인의 서브-세컨드 확정 능력을 활용하여 T+2를 T+0(즉시)로 단축하면 경쟁사 대비 결정적 차별화 가능
3. **수수료 볼륨 할인**: 고볼륨 가맹점 대상 1% 이하 수수료 티어 도입으로 Coinbase Commerce(1%), NOWPayments(0.5%)와의 수수료 경쟁력 확보
4. **온체인 분쟁 해결 파일럿**: Tempo 스마트 컨트랙트 기반 에스크로/분쟁 중재 시스템을 파일럿으로 도입하면 소비자 보호 표준 선점 가능
5. **코인 지원 확대**: 스테이블코인 위주 전략은 가맹점 리스크 차폐에 유리하나, BTC/ETH 직접 수취 옵션 추가로 크립토 네이티브 시장 접근 강화

---

## 9. 핵심 인사이트

1. **Stripe의 핵심 모트(moat)는 기술이 아니라 네트워크**: 수백만 기존 가맹점이 "한 줄의 코드"로 크립토 결제를 켤 수 있는 분배력이 최대 경쟁 우위이다. Coinbase Commerce가 Shopify 통합으로 유사한 전략을 추구하고 있으나, Stripe의 직접 통합 깊이에는 미치지 못한다.

2. **수수료 1.5%는 "편의성 프리미엄"으로 방어 가능하지만 장기적 리스크**: 법정화폐 자동 정산, 통합 대시보드, 컴플라이언스 포함 가격으로는 합리적이나, PayPal 프로모션(0.99%), Coinbase(1%), NOWPayments(0.5%)의 저가 공세가 지속되면 고볼륨 가맹점 이탈 리스크가 존재한다.

3. **"분쟁 미지원"은 업계 공통 한계이지 Stripe만의 약점은 아니다**: 모든 크립토 결제 경쟁사가 전통적 차지백을 지원하지 않는다. 다만 Coinbase의 Commerce Payments Protocol이 온체인 authorize-capture-refund를 구현하면서, 이 영역에서의 혁신 경쟁이 시작되었다.

4. **에이전트 결제 전쟁에서 Stripe는 가장 유리한 위치**: ACP(OpenAI 연합) + MPP(자체 프로토콜) + x402(Coinbase 연합)에 동시 참여하여, 어떤 표준이 승리하든 결제 실행 레이어에 Stripe가 존재한다. 이는 Google(AP2), Visa(TAP), PayPal(Agent Ready)이 각각 단일 프로토콜에만 베팅하는 것과 대비된다.

5. **지역 제한이 가장 시급한 해결 과제**: 미국 전용 가맹점 수취 제한은 글로벌 스테이블코인 결제 시장(B2B 4,000억 달러)의 대부분을 경쟁사에게 양보하는 것과 같다. 101개국 Stablecoin Financial Accounts 인프라를 결제 수취로 확장하는 것이 최우선 과제이다.

---

## Sources

- [Coinbase Commerce Fees](https://help.coinbase.com/en/commerce/getting-started/fees)
- [Coinbase Commerce Onchain Payment Protocol](https://www.coinbase.com/blog/coinbase-commerce-onchain-payment-protocol-deep-dive)
- [Coinbase Commerce Updates: No Fees](https://www.coinbase.com/blog/coinbase-commerce-updates-faster-payments-no-fees-more-currency-options)
- [Commerce Payments Protocol - Shopify Engineering](https://shopify.engineering/commerce-payments-protocol)
- [PayPal Crypto Payment Terms](https://www.paypal.com/us/legalhub/paypal/crypto-payment-method)
- [PayPal Drives Crypto Payments Mainstream](https://newsroom.paypal-corp.com/2025-07-28-PayPal-Drives-Crypto-Payments-into-the-Mainstream,-Reducing-Costs-and-Expanding-Global-Commerce)
- [PayPal Business Fees](https://www.paypal.com/us/business/paypal-business-fees)
- [BitPay Pricing](https://www.bitpay.com/pricing)
- [BitPay Settlements](https://developer.bitpay.com/docs/settlement)
- [BitPay Refund Process](https://support.bitpay.com/hc/en-us/articles/360000051746)
- [Binance Pay Fees](https://www.binance.com/en/support/faq/binance-pay-fees-6ff1944867e54b9a9576bce3109c7f7a)
- [NOWPayments Pricing](https://nowpayments.io/pricing)
- [NOWPayments Review 2026](https://coingape.com/nowpayments-review/)
- [CoinGate Pricing](https://coingate.com/pricing)
- [CoinGate 2026 Roadmap](https://coingate.com/blog/post/roadmap-for-2026)
- [Solana Payments](https://solana.com/docs/payments)
- [Solana Payments.org 2026](https://stablecoininsider.org/solanas-new-payments-org/)
- [MoonPay Acquires Helio](https://www.coindesk.com/business/2025/01/13/moon-pay-buys-crypto-payment-processor-helio-for-175-m)
- [MoonPay Commerce](https://www.hel.io/)
- [Circle CPN Managed Payments](https://www.circle.com/pressroom/circle-launches-cpn-managed-payments-a-full-stack-platform-for-seamless-stablecoin-settlement)
- [Circle CPN - The Block](https://www.theblock.co/post/396727/circle-rolls-out-usdc-payments-platform-that-lets-users-pay-without-holding-stablecoins)
- [Crypto.com Pay Documentation](https://pay-docs.crypto.com/)
- [Crypto.com Pay Refund](https://help.crypto.com/en/articles/6014589-how-to-get-a-refund)
- [Crypto.com Pay Settlement Currencies](https://help.crypto.com/en/articles/6063012-what-are-the-supported-settlement-currencies)
- [x402 Protocol](https://www.x402.org/)
- [x402 vs ACP vs UCP Comparison](https://dev.to/ai-agent-economy/x402-vs-acp-vs-ucp-which-agent-payment-protocol-should-you-actually-use-in-2026-2ecp)
- [Agent Payment Protocol War](https://blockeden.xyz/blog/2026/03/14/payment-giants-agent-protocol-war-visa-tap-google-ap2-coinbase-x402-paypal-ai-commerce/)
- [x402 vs Stripe MPP - WorkOS](https://workos.com/blog/x402-vs-stripe-mpp-how-to-choose-payment-infrastructure-for-ai-agents-and-mcp-tools-in-2026)
- [Agentic Payments Protocols Compared - Crossmint](https://www.crossmint.com/learn/agentic-payments-protocols-compared)
- [Stripe vs Coinbase Commerce 2026](https://blockfinances.fr/en/stripe-crypto-vs-coinbase-commerce-comparison-2026)
- [Crypto Payment Gateway 2026 Buyer's Guide](https://westafricatradehub.com/crypto/best-crypto-payment-gateway-2026-buyers-guide-to-fees-settlement-and-coin-support/)
- [Stripe Reportedly Mulling PayPal Acquisition](https://www.coindesk.com/business/2026/02/24/payments-giant-stripe-reportedly-mulling-paypal-acquisition)

---

*본 보고서는 2026년 4월 15일 기준 공개된 정보를 바탕으로 작성되었습니다. 수수료, 지원 국가, 정책 등은 각 기업의 업데이트에 따라 변동될 수 있습니다.*
