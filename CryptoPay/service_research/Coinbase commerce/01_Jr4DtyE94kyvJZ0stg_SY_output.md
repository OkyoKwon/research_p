# 시장 현황 분석 -- Coinbase Commerce / Coinbase Payment

## 분석 개요

- **분석 대상**: Coinbase Commerce (암호화폐 결제 게이트웨이) 및 Coinbase Payments (스테이블코인 결제 스택)
- **분석 일시**: 2026-04-14
- **주요 참조 소스**: Grand View Research, Fortune Business Insights, Research Nester, CoinLaw, Credence Research, Coinbase 공식 블로그, Shopify Engineering, ESMA, 미국 의회 법안 자료, Finextra, CoinDesk, CNBC

---

## 1. 암호화폐 결제 시장 규모

### 1.1 글로벌 시장 규모

| 구분 | 규모 | 기준 연도 | 출처 |
|------|------|-----------|------|
| 암호화폐 결제 앱 시장 | USD 6.24억 | 2025 | Research Nester |
| 암호화폐 결제 앱 시장 | USD 7.18억 | 2026 (추정) | Research Nester |
| 암호화폐 결제 앱 시장 (대안 추정) | USD 12.5억 | 2025 | TBRC |
| 암호화폐 결제 앱 시장 (대안 추정) | USD 15.0억 | 2026 (추정) | TBRC |
| 크립토 결제 게이트웨이 시장 | USD 16.8억 | 2024 | Credence Research |
| 크립토 결제 게이트웨이 시장 | USD 20.0억 | 2025 | TBRC |
| 크립토 결제 게이트웨이 시장 | USD 23.9억 | 2026 (추정) | TBRC |
| 크립토 결제 게이트웨이 시장 | USD 67.4억 | 2032 (전망) | Credence Research |
| 비트코인 결제 생태계 | USD 30.0억 | 2025 | Research Nester |
| 비트코인 결제 생태계 | USD 41.0억 | 2026 (추정) | Research Nester |
| 스테이블코인 시장 시가총액 | 약 USD 3,000억 | 2026 Q1 | 업계 추산 |

### 1.2 성장률 (CAGR)

| 구분 | CAGR | 기간 | 출처 |
|------|------|------|------|
| 암호화폐 결제 앱 | 16.8% | 2026-2035 | Research Nester |
| 암호화폐 결제 앱 (대안) | 20.5% | 2025-2026 YoY | TBRC |
| 크립토 결제 게이트웨이 | 19.0% | 2024-2032 | Credence Research |
| 크립토 결제 게이트웨이 | 18.7% | 2026-2030 | TBRC |
| 비트코인 결제 생태계 | 36.9% | 2026-2035 | Research Nester |
| 전체 암호화폐 시장 | 15.6% | 2026-2034 | Fortune Business Insights |

### 1.3 시장 성숙도 평가

암호화폐 결제 시장은 **초기 성장기(Early Growth Stage)**에 위치한다. 스테이블코인 결제가 시장의 성장 엔진 역할을 하며, 전통 결제 인프라(Shopify, Stripe)와의 통합이 가속화되고 있다. 미국 가맹점의 암호화폐 결제 수용률은 39%에 달하며, 2024-2026년 사이 82.1% 증가가 예상된다.

---

## 2. 코인베이스 결제 서비스 현황 및 포지셔닝

### 2.1 제품 라인업 변천

| 시기 | 제품 | 특징 |
|------|------|------|
| 2018-2024 | Coinbase Commerce (Legacy) | 전통적 결제 게이트웨이, API 기반 |
| 2024-2025 | Coinbase Commerce (Onchain Payment Protocol) | 온체인 결제 프로토콜로 전환, 스마트 컨트랙트 기반 |
| 2025.06 | Coinbase Payments | Shopify 연동 스테이블코인 결제 스택, Base 네트워크 기반 |
| 2025.10 | Commerce Payments Protocol | Shopify와 공동 개발, 오픈소스 상거래 결제 프로토콜 |
| 2026.01 | Coinbase Commerce 업데이트 | 무료 즉시 결제(Coinbase 유저), 7개 신규 암호화폐 추가 |
| 2026 진행중 | Coinbase Business 통합 | Commerce를 Coinbase Business로 통합, 커스터디 및 법정화폐 인출 기능 강화 |

### 2.2 시장 점유율

| 게이트웨이 | 시장 점유율 | 특징 |
|-----------|-----------|------|
| **BitPay** | **20%** | 가맹점 채택 1위, 법정화폐 정산 강점 |
| **CoinGate** | **14%** | 유럽 시장 강점 |
| **Coinbase Commerce** | **12%** | 기관 통합, Shopify 파트너십 |
| **Binance Pay** | **8%** | 아시아 시장, 바이낸스 생태계 |
| NOWPayments | - | 300+ 코인 지원, 낮은 수수료(0.5%) |
| BTCPay Server | - | 완전 자기주권, 오픈소스 |

Coinbase Commerce는 단독 점유율 12%로 3위이나, PayPal/Crypto.com Pay와 합산 시 상위 3사가 전체의 34%를 차지한다. Shopify 파트너십과 Base 네트워크를 통한 스테이블코인 전략으로 점유율 확대를 도모하고 있다.

---

## 3. 결제(Payment) 프로세스 상세

### 3.1 결제 흐름

#### 기본 결제 흐름 (Coinbase Commerce)

```
소비자 -> 가맹점 체크아웃 -> Commerce 결제 페이지 생성
  -> 소비자 지갑에서 암호화폐 전송
  -> 온체인 결제 프로토콜 (스마트 컨트랙트)
  -> DEX를 통한 자동 환전 (선택 시)
  -> 수수료 차감 (1%)
  -> 가맹점 지갑에 정산
```

#### Commerce Payments Protocol (Authorize-Capture 모델)

```
1. Authorization (인가)
   소비자 -> 지갑에서 결제 정보 서명
   -> 가맹점 -> 오퍼레이터 서비스에 결제 인가 요청
   -> 오퍼레이터 -> 에스크로 스마트 컨트랙트에 인가 트랜잭션 제출
   -> 결제 확인 (자금은 에스크로에 보관)

2. Capture (캡처) / Void (취소)
   가맹점 -> 상품 준비 완료 후 캡처 요청
   -> 에스크로에서 가맹점 지갑으로 자금 이동
   (또는 Void 시 소비자에게 자금 반환)

3. Refund (환불)
   가맹점 -> 환불 요청 (캡처 후 만료 기한 이전)
   -> 에스크로에서 소비자에게 자금 반환
```

### 3.2 지원 암호화폐

| 카테고리 | 지원 자산 |
|---------|----------|
| 주요 암호화폐 | BTC, ETH, LTC, BCH, DOGE 등 |
| 스테이블코인 | USDC, DAI, EURC |
| 총 지원 코인 | 100+ 종 |
| 자동 환전 대상 | USDC (Uniswap DEX 통해 자동 스왑) |
| 2026.01 추가 | 7개 신규 암호화폐 |

### 3.3 지원 네트워크

| 네트워크 | 특징 |
|---------|------|
| **Base** (핵심) | Coinbase L2, 약 200ms 정산, 수수료 약 $0.01 |
| Ethereum | 메인넷, 높은 가스비 |
| Polygon | L2, 저비용 |
| 기타 | 다수 EVM 호환 네트워크 |

### 3.4 API 구조

- **RESTful API**: 프로그래밍 방식의 Charge(결제 요청) 생성
- **Webhooks**: 트랜잭션 상태 업데이트 실시간 알림
- **온체인 결제 프로토콜**: 오픈소스 스마트 컨트랙트 기반
  - 원자적(Atomic) 결제: 가맹점이 정확한 금액을 수령하거나 트랜잭션이 완전 롤백
  - 지갑 비종속(Wallet-agnostic): 어떤 지갑에서든 결제 가능
  - 자동 환전: Uniswap 유동성을 활용한 토큰 스왑
- **GitHub**: `coinbase/commerce-onchain-payment-protocol` (오픈소스)
- **Shopify 통합**: Shopify Payments 내 네이티브 USDC 결제 (별도 게이트웨이 불필요)

### 3.5 결제 수단별 특징

| 결제 유형 | 설명 |
|----------|------|
| Coinbase 유저 -> Commerce 가맹점 | **무료, 즉시 정산** (2026.01 업데이트) |
| 외부 지갑 -> Commerce 가맹점 | 네트워크 수수료 + 1% Commerce 수수료 |
| Shopify USDC 결제 | Base 네트워크, 외환 수수료 없음 |

---

## 4. 정산(Settlement) 프로세스 상세

### 4.1 정산 플랜 비교

| 항목 | Self-Managed (자체 관리) | Coinbase-Managed (코인베이스 관리) |
|------|------------------------|----------------------------------|
| 커스터디 모델 | **비수탁형** (12단어 시드 구문) | **수탁형** (Coinbase Exchange 연동) |
| 정산 통화 | 암호화폐 전용 | 암호화폐 + **법정화폐(USD 등)** |
| 법정화폐 인출 | 불가 | **가능** (연결 은행 계좌로 출금) |
| 자동 환전 | USDC로 자동 스왑 (DEX 경유) | **USD로 자동 환전** (가격 변동 리스크 제거) |
| 출금 방식 | 외부 암호화폐 주소 또는 Coinbase.com 계정 | 은행 계좌, Coinbase 계정 |
| 수수료 처리 | 정산 시 1% 차감 | 정산 시 1% 자동 차감 |
| 거래 관리 | 머천트 대시보드 | 머천트 대시보드 + Coinbase Exchange |

### 4.2 정산 속도

| 조건 | 정산 속도 |
|------|----------|
| Coinbase 유저 결제 (Coinbase-Managed) | **즉시** |
| Base 네트워크 결제 | **약 200ms** (최적 조건) |
| 일반 온체인 결제 | 블록 확인 시간 (네트워크별 상이) |
| 법정화폐 인출 (은행 계좌) | 1-3 영업일 (업계 추산) |

### 4.3 정산 수수료 구조

| 수수료 항목 | 요율/금액 | 비고 |
|------------|----------|------|
| Commerce 거래 수수료 | **1%** | 모든 결제에 적용 |
| 네트워크(가스) 수수료 | **약 $0.01** (Base) | 네트워크별 상이 |
| 자동 환전 수수료 (DEX) | DEX 스왑 비용 | Uniswap 수수료 포함 |
| 법정화폐 환전 수수료 | 추가 1-1.5% (업계 추산) | Coinbase Exchange 스프레드 |
| 월 고정 비용 | **없음** | |
| 셋업 비용 | **없음** | |

**총비용 비교**:
- USDC 수령 후 암호화폐 보유 시: **약 1%**
- USD로 환전까지 포함 시: **약 2-2.5%**
- 참고: Stripe 2.9% + $0.30, PayPal 2.49% + $0.49

### 4.4 환전 정책

- **자동 환전 (Auto-Convert)**: 가맹점이 선택적으로 활성화 가능. 결제 수령 시 즉시 USDC 또는 USD로 자동 환전
- **수동 환전**: 가맹점이 원하는 시점에 Coinbase Exchange에서 직접 환전
- **변동성 보호**: USDC 자동 환전 시 DEX 스왑이 결제 시점에 즉시 실행되어 가격 변동 리스크 최소화
- **Shopify 통합 시**: 가맹점이 현지 법정화폐를 기본으로 수령하거나, USDC 직접 수령 선택 가능

---

## 5. 환불(Refund) 정책 상세

### 5.1 환불 정책 개요

Coinbase Commerce는 **비수탁형(non-custodial)** 솔루션이므로, 플랫폼 자체가 Commerce API를 통해 환불을 처리할 수 없다. 환불은 가맹점이 직접 처리해야 한다.

### 5.2 플랜별 환불 프로세스

#### Self-Managed 플랜

```
1. 소비자가 가맹점에 환불 요청
2. 가맹점이 소비자의 수령 주소 확인
3. 가맹점이 직접 해당 암호화폐를 소비자 주소로 전송
4. (결제와 동일한 네트워크로 환불 권장)
```

- 환불은 전적으로 가맹점의 책임
- Commerce API를 통한 자동 환불 불가
- 네트워크 수수료는 가맹점 부담

#### Coinbase-Managed 플랜

```
1. 소비자가 가맹점에 환불 요청
2. 가맹점이 Coinbase Exchange 인터페이스에서 환불 처리
3. Coinbase Exchange를 통해 소비자에게 자금 반환
```

- Coinbase Exchange를 통한 보다 체계적인 환불 가능
- 법정화폐로 환전된 경우 재환전 필요

#### Commerce Payments Protocol (신규)

```
1. 캡처 후 만료 기한 이전에 환불 요청
2. 에스크로 스마트 컨트랙트를 통해 자금 반환
3. 만료 기한 이후 캡처된 결제는 최종(final) 처리
```

- 인가-캡처 모델에서의 프로그래밍 방식 환불 지원
- 만료 기한(expiry) 개념 도입으로 환불 기간 제한
- Void(취소): 캡처 전 전액 취소 가능

### 5.3 환불 관련 수수료

| 항목 | 내용 |
|------|------|
| 환불 수수료 (Commerce 플랫폼) | 별도 청구 없음 |
| 네트워크 수수료 | 가맹점 부담 (환불 트랜잭션의 가스비) |
| 환전 손실 | 결제 시점 대비 환율 차이로 인한 손실 가능 |
| Commerce 수수료 반환 | 환불 시 이미 차감된 1% 수수료는 **반환되지 않음** (업계 추산) |

### 5.4 분쟁 해결 절차

1. **1단계 - 직접 해결**: 소비자가 가맹점에 직접 연락하여 환불 협의
2. **2단계 - 증빙 제출**: 거래 ID, 고객 정보, 상품/서비스 설명, 환불/취소 정책, 고객과의 커뮤니케이션 기록 제출
3. **3단계 - Coinbase 검토**: Coinbase에 공식 불만 접수 시, 접수일로부터 **45 영업일 이내** 응답
4. **핵심 차이점**: 전통 카드 결제의 차지백(Chargeback)과 달리, 블록체인 거래는 비가역적이므로 소비자 보호 장치가 제한적

---

## 6. 산업 트렌드 및 성장 동인

### 6.1 주요 트렌드 (2025-2026)

| 트렌드 | 설명 | 코인베이스 영향 |
|--------|------|---------------|
| **스테이블코인 결제 급성장** | USDC/USDT가 암호화폐 결제의 주축으로 부상, 스테이블코인 시가총액 약 $3,000억 돌파 | USDC 중심 전략과 직접적으로 정렬, Circle과의 협력 관계가 핵심 자산 |
| **전통 커머스 플랫폼 통합** | Shopify, Stripe 등 주요 플랫폼이 암호화폐 결제 네이티브 통합 | Shopify와의 직접 파트너십, Commerce Payments Protocol 공동 개발 |
| **L2 네트워크 기반 결제** | Base, Polygon 등 L2를 통한 저비용/고속 결제 확산 | Base 네트워크 소유/운영이라는 독보적 우위 |
| **규제 명확화** | GENIUS Act(미국), MiCA(EU) 등 스테이블코인/암호화폐 규제 프레임워크 확립 | 규제 준수 선두주자로서의 포지셔닝 강화 |
| **인가-캡처 모델 도입** | 전통 결제의 인가/캡처/환불 플로우를 온체인으로 구현 | Commerce Payments Protocol로 선제 대응 |
| **B2B 스테이블코인 결제** | 기업 간 국제 송금/결제에 스테이블코인 활용 확대 | Coinbase Business 통합으로 기업 고객 확대 전략 |

### 6.2 성장 동인

1. **스테이블코인 규제 확립**: GENIUS Act(미국, 2025.07 서명) 시행으로 스테이블코인의 법적 지위 명확화. 100% 준비금 요구, 월간 공시 의무 등 소비자 보호 강화
2. **전통 커머스 플랫폼 채택**: Shopify의 수백만 가맹점에 USDC 결제 네이티브 도입 (2025.06)
3. **비용 우위**: 전통 카드 결제(2.9%+$0.30) 대비 암호화폐 결제(1-2.5%)의 비용 절감
4. **글로벌 접근성**: 은행 인프라가 부족한 지역에서의 결제 수단으로서 가치
5. **즉시 정산**: 24/7 즉시 정산 vs 전통 결제의 2-3 영업일 정산 주기

### 6.3 저해 요인 및 리스크

1. **가격 변동성**: BTC/ETH 등 비스테이블코인 결제 시 환율 리스크 (자동 USDC 환전으로 부분 해소)
2. **사용자 경험**: 지갑 관리, 시드 구문, 가스비 등 진입장벽
3. **규제 불확실성**: MiCA 완전 시행(2026.06)까지 유럽 내 과도기, 국가별 상이한 이행 일정
4. **환불/소비자 보호 한계**: 블록체인의 비가역성으로 인한 분쟁 해결 어려움
5. **경쟁 심화**: BitPay(20%), CoinGate(14%) 등 기존 플레이어 + Stripe/PayPal의 암호화폐 결제 진출

---

## 7. 규제 환경 분석

### 7.1 미국 -- GENIUS Act

| 항목 | 내용 |
|------|------|
| 서명일 | 2025.07.18 |
| 핵심 내용 | 결제용 스테이블코인에 대한 연방 규제 프레임워크 수립 |
| 준비금 요구 | 100% 유동 자산(USD, 단기 국채) 담보 필수 |
| 공시 의무 | 월간 준비금 구성 공개 |
| 증권 분류 | 결제 스테이블코인은 증권/상품이 아님 (SEC/CFTC 관할 제외) |
| 시행 시기 | 법 제정 후 18개월 또는 최종 규정 발표 후 120일 중 빠른 시점 |
| 코인베이스 영향 | USDC 중심 전략에 직접적 수혜, 규제 준수 비용은 증가 |

- 2026.04 현재: FDIC가 GENIUS Act 적용 절차안을 승인했으며, OCC도 시행 규칙을 연방관보에 게재(2026.03)
- Coinbase는 2026.04 초 핵심 규제 허들을 통과하여 스테이블코인 사업 강화 기반 확보 (CNBC 보도)

### 7.2 EU -- MiCA (Markets in Crypto-Assets Regulation)

| 항목 | 내용 |
|------|------|
| 발효일 | 2024.12.30 |
| 완전 시행 | 2026.06.30 (전환기간 종료) |
| 핵심 요구 | CASP 라이선스, Travel Rule(송수신인 정보 포함), AML/CFT 프로세스 |
| 과태료 현황 | EUR 5.4억 이상 부과 (2026.04 기준) |
| 국가별 차이 | 네덜란드(2025.07), 이탈리아(2025.12), 기타(~2026.07) |
| 이중 라이선스 | 2026.03부터 EMT(전자화폐토큰) 관련 MiCA + PSD2 동시 필요 가능 |

### 7.3 규제가 코인베이스 결제 서비스에 미치는 영향

**기회 요인**:
- 규제 명확화로 기관/기업 고객의 암호화폐 결제 채택 가속
- 이미 규제 준수 체계를 갖춘 코인베이스의 경쟁 우위 확대
- 스테이블코인 법제화로 USDC 기반 결제 수요 증가

**위험 요인**:
- MiCA의 이중 라이선스 요구로 유럽 운영 비용 증가
- Travel Rule 준수를 위한 기술 인프라 추가 투자 필요
- 국가별 규제 차이로 인한 글로벌 서비스 통일성 저하

---

## 8. 경쟁사 대비 차별점 및 강약점

### 8.1 강점

1. **Base 네트워크 소유**: 자체 L2 블록체인으로 거래 비용(약 $0.01)과 속도(약 200ms) 제어
2. **Shopify 파트너십**: 수백만 가맹점에 대한 네이티브 USDC 결제 접근
3. **원자적 결제**: 정확한 금액 보장, 잘못된 금액/주소 결제 불가능
4. **Commerce Payments Protocol**: 전통 결제의 인가-캡처-환불을 온체인으로 구현한 유일한 프로토콜
5. **Coinbase 생태계 연동**: 1억+ 사용자 기반, 거래소, 지갑, 커스터디 통합
6. **USDC 전략적 포지션**: Circle과의 파트너십, GENIUS Act 수혜

### 8.2 약점

1. **법정화폐 정산 제한**: Self-Managed 플랜에서 법정화폐 인출 불가 (BitPay 대비 열위)
2. **암호화폐 다양성 부족**: 100+ 코인 지원이나 NOWPayments(300+), BitPay(100+) 대비 한정적
3. **API 문서화**: NOWPayments, BTCPay Server 대비 API 문서가 상대적으로 제한적
4. **환불 프로세스 복잡성**: 비수탁형 특성상 자동 환불 불가, 가맹점 수동 처리 필요
5. **유럽 시장 입지**: CoinGate(14%) 대비 유럽 특화 기능(SEPA 등) 부족
6. **플랫폼 변화의 불확실성**: Commerce -> Business 통합 과도기에 따른 가맹점 혼란

### 8.3 경쟁사 수수료 비교

| 게이트웨이 | 거래 수수료 | 정산 통화 | 특이사항 |
|-----------|-----------|----------|---------|
| **Coinbase Commerce** | 1% | 암호화폐/USD | Coinbase 유저 간 무료 |
| BitPay | 1% | 법정화폐/암호화폐 | 법정화폐 정산 강점 |
| NOWPayments | 0.5% | 암호화폐 | 법정화폐 직접 정산 불가 |
| CoinGate | 1% | EUR/암호화폐 | 유럽 법정화폐 정산 |
| Stripe (암호화폐) | 1.5% | 법정화폐 | 기존 Stripe 가맹점 자연 전환 |
| BTCPay Server | **무료** | 암호화폐 | 자체 호스팅 필요 |

---

## 9. 결제-정산-환불 전체 라이프사이클 요약

```
[결제 단계]
소비자 -> 가맹점 체크아웃
  -> Coinbase Commerce 결제 요청 (Charge 생성)
  -> 소비자 지갑에서 암호화폐 전송
  -> 온체인 프로토콜: 원자적 결제 실행
  -> (선택) DEX를 통한 USDC 자동 환전
  -> 1% Commerce 수수료 차감
  수수료: 1% + 네트워크 가스비(약 $0.01 on Base)

[정산 단계]
결제 완료 -> 가맹점 지갑에 정산
  -> Self-Managed: 암호화폐로 즉시 정산
  -> Coinbase-Managed: USD 자동 환전 -> 은행 계좌 출금(1-3 영업일)
  -> Shopify 통합: 현지 법정화폐로 정산 또는 USDC 직접 수령
  수수료: 법정화폐 환전 시 추가 1-1.5% (Exchange 스프레드)

[환불 단계]
소비자 -> 가맹점에 환불 요청
  -> Self-Managed: 가맹점이 소비자 주소로 직접 전송
  -> Coinbase-Managed: Exchange 통해 환불 처리
  -> Commerce Payments Protocol: 에스크로에서 프로그래밍 방식 환불 (만료 전)
  수수료: 네트워크 가스비 (가맹점 부담), 기존 1% 수수료 비반환(업계 추산)
```

---

## 10. 최근 주요 변경사항 (2025-2026)

| 시기 | 변경사항 | 영향 |
|------|---------|------|
| 2025.06 | Shopify USDC 결제 출시 (Base 네트워크) | 수백만 가맹점에 스테이블코인 결제 접근 |
| 2025.07 | GENIUS Act 서명 | 스테이블코인 결제의 법적 기반 확립 |
| 2025.10 | Commerce Payments Protocol 출시 | 인가-캡처-환불의 온체인 구현 |
| 2026.01 | Commerce 무료 즉시결제 + 7개 신규 코인 | Coinbase 유저 간 무마찰 결제 |
| 2026 진행중 | Commerce -> Coinbase Business 통합 | 커스터디, 법정화폐 인출, 회계 통합 강화 |
| 2026.04 | Coinbase 스테이블코인 규제 허들 통과 | 사업 확장 기반 확보 |

---

## 11. 핵심 인사이트 및 시사점

### 11.1 코인베이스의 전략적 방향

코인베이스는 암호화폐 결제 시장에서 **"스테이블코인 결제 인프라 플랫폼"**으로의 전환을 가속화하고 있다. 단순 결제 게이트웨이를 넘어, Base 네트워크 + USDC + Commerce Payments Protocol + Shopify 파트너십이라는 수직 통합 전략을 추구한다.

### 11.2 가맹점 관점 평가

| 항목 | 평가 |
|------|------|
| 통합 난이도 | 중간 (API 기반), Shopify는 낮음 (네이티브) |
| 운영 편의성 | Coinbase-Managed 높음, Self-Managed 중간 |
| 비용 효율성 | 전통 결제 대비 우수 (1% vs 2.9%) |
| 법정화폐 정산 | Coinbase-Managed에서만 가능, BitPay 대비 불편 |
| 환불 처리 | 수동 처리 필요, 전통 결제 대비 복잡 |
| 소비자 보호 | 차지백 부재로 가맹점에 유리하나 소비자 보호 약함 |

### 11.3 향후 전망

1. **2026 하반기**: Coinbase Business 통합 완료로 원스톱 비즈니스 결제 솔루션 완성 예상
2. **2027**: GENIUS Act 완전 시행으로 스테이블코인 결제 주류화 가속
3. **중기**: Commerce Payments Protocol의 업계 표준화 가능성 -- Shopify 외 추가 플랫폼 채택 여부가 핵심
4. **장기**: 전통 결제 네트워크(Visa/Mastercard)와의 경쟁 및 협력 구도 형성

---

## 참조 소스

1. [Research Nester - Cryptocurrency Payment Apps Market Size 2026-2035](https://www.researchnester.com/reports/cryptocurrency-payment-apps-market/6523)
2. [CoinLaw - Crypto Payment Gateways Statistics 2026](https://coinlaw.io/crypto-payment-gateways-statistics/)
3. [CoinLaw - Crypto Payments Industry Statistics 2026](https://coinlaw.io/crypto-payments-industry-statistics/)
4. [Credence Research - Crypto Payment Gateways Market Size 2032](https://www.credenceresearch.com/report/crypto-payment-gateways-market)
5. [Fortune Business Insights - Cryptocurrency Market Size 2034](https://www.fortunebusinessinsights.com/industry-reports/cryptocurrency-market-100149)
6. [Grand View Research - Cryptocurrency Market Report 2033](https://www.grandviewresearch.com/industry-analysis/cryptocurrency-market-report)
7. [Coinbase Blog - Introducing Coinbase Payments](https://www.coinbase.com/blog/powering-the-future-of-ecommerce-introducing-coinbase-payments)
8. [Coinbase Blog - Commerce Onchain Payment Protocol Deep Dive](https://www.coinbase.com/blog/coinbase-commerce-onchain-payment-protocol-deep-dive)
9. [Coinbase Blog - Business Payment Tools](https://www.coinbase.com/blog/introducing-a-powerful-suite-of-business-payment-tools-on-coinbase-business)
10. [Coinbase Blog - Commerce Updates: Faster Payments, No Fees](https://www.coinbase.com/blog/coinbase-commerce-updates-faster-payments-no-fees-more-currency-options)
11. [Shopify Engineering - Commerce Payments Protocol (2025)](https://shopify.engineering/commerce-payments-protocol)
12. [CoinDesk - Shopify USDC Payments on Base](https://www.coindesk.com/business/2025/06/12/shopify-to-enable-usdc-payments-on-coinbase-s-base-for-merchants-worldwide)
13. [CNBC - Coinbase Clears Regulatory Hurdle for Stablecoin Business](https://www.cnbc.com/2026/04/02/coinbase-clears-key-regulatory-hurdle-in-bid-to-bolster-its-stablecoin-business.html)
14. [Finextra - Deep Dive: Coinbase Commerce Payments Protocol](https://www.finextra.com/blogposting/29130/deep-dive-coinbases-commerce-payments-protocol-how-to-use-it-integrate-it-and-win-with-it)
15. [FinTech Wrap Up - Programmable Payments with Coinbase Commerce Protocol](https://www.fintechwrapup.com/p/deep-dive-coinbases-commerce-payments)
16. [GitHub - coinbase/commerce-onchain-payment-protocol](https://github.com/coinbase/commerce-onchain-payment-protocol)
17. [Coinbase Help - Commerce Fees](https://help.coinbase.com/en/commerce/getting-started/fees)
18. [Coinbase Help - Refunds](https://help.coinbase.com/en/commerce/managing-account/refunds)
19. [Coinbase Commerce FAQ](https://www.coinbase.com/commerce/faq)
20. [White House - GENIUS Act Fact Sheet](https://www.whitehouse.gov/fact-sheets/2025/07/fact-sheet-president-donald-j-trump-signs-genius-act-into-law/)
21. [Latham & Watkins - GENIUS Act of 2025](https://www.lw.com/en/insights/the-genius-act-of-2025-stablecoin-legislation-adopted-in-the-us)
22. [ESMA - MiCA Regulation](https://www.esma.europa.eu/esmas-activities/digital-finance-and-innovation/markets-crypto-assets-regulation-mica)
23. [Sumsub - MiCA Regulation and EU Crypto Rules 2026](https://sumsub.com/blog/crypto-regulations-in-the-european-union-markets-in-crypto-assets-mica/)
24. [TRM Labs - Global Crypto Policy Review 2025/26](https://www.trmlabs.com/reports-and-whitepapers/global-crypto-policy-review-outlook-2025-26)
25. [Aurpay - Crypto Payment Gateway Comparison 2026](https://aurpay.net/aurspace/crypto-payment-gateway-comparison-2026/)
26. [CoinLaw - Cryptocurrency Payment Adoption by Merchants Statistics 2025](https://coinlaw.io/cryptocurrency-payment-adoption-by-merchants-statistics/)

---

*본 보고서의 일부 수치는 리서치 기관별 시장 정의 및 방법론 차이로 인해 편차가 존재합니다. "업계 추산"으로 표기된 항목은 공식 출처가 아닌 복수의 2차 소스를 종합한 추정치입니다.*
