# 비즈니스 모델 및 기술 프로파일 -- Coinbase Commerce / Coinbase Payment

## 분석 개요

- **분석 대상**: Coinbase Commerce (암호화폐 결제 게이트웨이) 및 Commerce Payments Protocol
- **분석 일시**: 2026-04-14
- **선행 분석 참조**: `01_Jr4DtyE94kyvJZ0stg_SY_output.md` (시장 현황 분석)
- **주요 조사 소스**: Coinbase 공식 블로그, GitHub 리포지토리, Shopify Engineering 블로그, Coinbase 투자자 보고서, Crunchbase, 채용공고, StackShare, Base Engineering 블로그, Finextra, FinTech Wrap Up

---

## 1. 비즈니스 모델 요약

### 1.1 수익 유형

| 구분 | 유형 | 설명 |
|------|------|------|
| 핵심 수익원 | **거래 수수료 (Transaction Fee)** | 모든 Commerce 결제에 1% 수수료 부과 |
| 2차 수익원 | **USDC 준비금 이자 수익 (Revenue Sharing)** | Circle과의 이익 분배 -- 플랫폼 보유 USDC 이자 100%, 외부 USDC 이자 50:50 |
| 3차 수익원 | **환전 스프레드 (Conversion Spread)** | 법정화폐 환전 시 0.5-2% 스프레드 적용 |
| 간접 수익원 | **생태계 락인 (Ecosystem Lock-in)** | Commerce 가맹점 -> Coinbase Exchange/Custody/Business 전환 유도 |
| 전략적 수익원 | **Base 네트워크 시퀀서 수수료** | Base L2에서 발생하는 가스비 수익 |

### 1.2 핵심 가치 제안

1. **비용 절감**: 전통 결제 2.9% + $0.30 대비 총비용 1-2.5%로 약 50% 절감
2. **즉시 정산**: Base 네트워크 기준 약 200ms, 전통 결제의 2-3 영업일 대비 압도적 우위
3. **글로벌 무국경 결제**: 국경/은행 인프라와 무관하게 전세계 어디서든 수령 가능
4. **원자적 결제 보장**: 정확한 금액이 가맹점에 도달하거나 전액 롤백 -- 부분 결제 불가
5. **비수탁형 자산 통제**: 가맹점이 자체 지갑으로 직접 수령, 카운터파티 리스크 최소화

### 1.3 주요 고객 세그먼트

| 세그먼트 | 특성 | 주요 니즈 |
|---------|------|----------|
| **Shopify 가맹점** | 수백만 규모, 네이티브 통합 | 쉬운 셋업, 법정화폐 정산, 낮은 수수료 |
| **글로벌 이커머스** | 국경 간 거래 빈번 | 외환 수수료 절감, 즉시 정산 |
| **디지털 콘텐츠/SaaS** | 소액 반복 결제 | 낮은 고정비, 자동화 |
| **암호화폐 네이티브 비즈니스** | DeFi, NFT, Web3 서비스 | 온체인 정산, USDC 직접 수령 |
| **고위험 산업** | 차지백 리스크 높은 업종 | 비가역적 결제로 차지백 부재 |

---

## 2. 가격 체계

### 2.1 수수료 구조 상세

| 수수료 항목 | 요율/금액 | 적용 조건 | 신뢰도 |
|------------|----------|----------|--------|
| Commerce 거래 수수료 | **1%** | 모든 외부 지갑 결제 | 확인됨 |
| Coinbase 유저 간 결제 | **무료** | Coinbase 앱/지갑 사용 시 | 확인됨 |
| 네트워크 가스비 (Base) | **약 $0.01** | Base L2 네트워크 사용 시 | 확인됨 |
| 네트워크 가스비 (Ethereum) | **$1-20+** | Ethereum 메인넷 사용 시 | 추정 (네트워크 상황 의존) |
| DEX 자동 스왑 수수료 | **약 0.3%** | Uniswap V3 경유 토큰 스왑 시 | 추정 (Uniswap 풀 수수료율 기준) |
| 법정화폐 환전 스프레드 | **1-1.5%** | Coinbase-Managed에서 USD 환전 시 | 추정 (업계 추산) |
| 월 구독료 | **$0** | - | 확인됨 |
| 셋업 비용 | **$0** | - | 확인됨 |
| 환불 수수료 | **$0** (별도 청구 없음) | 네트워크 가스비는 가맹점 부담 | 확인됨 |
| 기존 수수료 반환 | **비반환** | 환불 시 1% 수수료 미환급 | 추정 (업계 추산) |

### 2.2 총비용 시나리오 비교

| 시나리오 | 총비용 | 설명 |
|---------|--------|------|
| USDC on Base 수령, 암호화폐 보유 | **약 1% + $0.01** | 최소 비용 |
| 기타 토큰 수령 -> USDC 자동 스왑 | **약 1.3% + 가스비** | DEX 스왑 수수료 포함 |
| USDC 수령 -> USD 환전 -> 은행 출금 | **약 2-2.5%** | Exchange 스프레드 포함 |
| Coinbase 유저 간 USDC on Base | **약 $0.01** | Commerce 수수료 무료 |
| 참고: Stripe 카드 결제 | **2.9% + $0.30** | - |
| 참고: PayPal 결제 | **2.49% + $0.49** | - |

---

## 3. 수익 구조 심층 분석

### 3.1 Coinbase 전사 재무 현황

| 지표 | 수치 | 기준 | 출처 |
|------|------|------|------|
| 연간 매출 | **$7.181B** | 2025 FY | Coinbase IR |
| 구독/서비스 수익 | 전체의 약 19%가 USDC 관련 | 2025 FY | Bloomberg Intelligence |
| USDC 관련 수익 | **약 $1.35B** | 2025 FY 추정 | Bloomberg Intelligence |
| 조정 EBITDA (Q4) | **$566M** | 2025 Q4 | Coinbase IR |
| 시가총액 | **약 $46B** | 2026.04 | 시장 데이터 |
| 주가 | **$174.95** | 2026.04.13 | NASDAQ |
| P/E 비율 | **37.74** | 2026.04 | 시장 데이터 |
| Q1 2026 구독/서비스 수익 전망 | **$550-630M** | 2026 Q1 가이던스 | Coinbase IR |

### 3.2 Commerce 사업부 수익 구조 추정

Coinbase는 Commerce 사업부의 개별 매출을 공시하지 않는다. 아래는 공개 정보 기반 추정이다.

| 수익 채널 | 추정 기여도 | 근거 |
|----------|-----------|------|
| 거래 수수료 (1%) | 중간 | 시장 점유율 12%, 가맹점 수 약 8,000+ (과거 기준) |
| USDC 준비금 이자 | **핵심** | 전사 매출의 19%, 약 $1.35B (Commerce 외 거래소 포함) |
| 환전 스프레드 | 낮음-중간 | Coinbase-Managed 플랜 사용자에 한정 |
| 생태계 전환 가치 | 간접적이나 전략적 | Commerce -> Business/Exchange/Custody 유입 |

### 3.3 USDC 수익 분배 구조 (Coinbase-Circle 파트너십)

```
[USDC 준비금 이자 수익 흐름]

USDC 발행 -> Circle이 준비금(USD, 단기 국채)에 투자 -> 이자 수익 발생
                                                           |
                                    +----------------------+----------------------+
                                    |                                             |
                          Coinbase 플랫폼 보유 USDC              외부 보유 USDC
                          (전체의 약 20%)                        (전체의 약 80%)
                                    |                                             |
                          이자 수익 100% -> Coinbase             이자 수익 50:50 분배
                                                                  |           |
                                                              Coinbase    Circle
```

- 계약 갱신 주기: 3년 (차기 갱신 2026년)
- 전략적 함의: Coinbase는 자사 플랫폼의 USDC 보유량을 늘릴 인센티브가 극대화됨
- Commerce는 USDC 결제 촉진 -> 플랫폼 USDC 보유량 증가 -> 이자 수익 증가의 선순환 구조

---

## 4. 기술 스택 분석

### 4.1 전사 기술 스택

#### 프로그래밍 언어 및 프레임워크

| 기술 | 용도 | 신뢰도 |
|------|------|--------|
| **Go (Golang)** | 핵심 백엔드 서비스, 마이크로서비스 | 확인됨 (채용공고) |
| **Ruby / Rails** | 레거시 백엔드, 일부 서비스 | 확인됨 (채용공고) |
| **Python** | AI 에이전트, 데이터 파이프라인 | 확인됨 (엔지니어링 블로그) |
| **React / React Native** | 웹 프론트엔드, 모바일 앱 | 확인됨 (StackShare, 블로그) |
| **Solidity** | 스마트 컨트랙트 (Transfers.sol 등) | 확인됨 (GitHub) |
| **TypeScript/JavaScript** | 프론트엔드, Node.js 서비스 | 추정 (채용공고) |

#### 인프라 및 클라우드

| 기술 | 용도 | 신뢰도 |
|------|------|--------|
| **AWS** | 핵심 클라우드 인프라 | 확인됨 (AWS 파트너십 공식 발표) |
| **Amazon EKS** | 컨테이너 오케스트레이션 | 확인됨 (AWS 사례) |
| **Amazon EC2 (Graviton)** | 컴퓨팅 인스턴스 | 확인됨 (비용 62% 절감 사례) |
| **AWS Bedrock AgentCore** | AI 에이전트 호스팅 | 확인됨 (엔지니어링 블로그) |
| **Docker** | 컨테이너화 | 확인됨 (채용공고) |
| **Kafka (AWS MSK)** | 이벤트 스트리밍/메시징 | 확인됨 (엔지니어링 블로그) |
| **PostgreSQL** | 핵심 관계형 데이터베이스 | 확인됨 (채용공고) |
| **MongoDB** | 문서형 데이터베이스 | 추정 (채용공고) |
| **Redis** | 캐싱 | 추정 (일반 정보) |
| **Redshift** | 데이터 웨어하우스 | 추정 (채용공고) |

#### 데이터 플랫폼

| 기술 | 용도 | 신뢰도 |
|------|------|--------|
| **Databricks** | 데이터 엔지니어링/분석 | 확인됨 (데이터 스택 분석) |
| **Snowflake** | 데이터 웨어하우스 | 확인됨 (데이터 스택 분석) |
| **CelerData** | 실시간 분석 | 확인됨 (데이터 스택 분석) |

#### 내부 도구

| 기술 | 용도 | 신뢰도 |
|------|------|--------|
| **Codeflow** | 보안 배포 파이프라인 | 확인됨 (엔지니어링 블로그) |
| **GeoEngineer** | 인프라 코드화 도구 | 확인됨 (엔지니어링 블로그) |
| **Snapchain** | 블록체인 인프라 프로젝트 | 확인됨 (엔지니어링 블로그) |
| **LangGraph** | AI 에이전트 트레이싱/평가 | 확인됨 (엔지니어링 블로그) |

### 4.2 Commerce 전용 기술 스택

#### 스마트 컨트랙트 레이어

| 구성요소 | 기술 | 설명 | 신뢰도 |
|---------|------|------|--------|
| **Transfers.sol** | Solidity | 자금 이동 오케스트레이션 핵심 컨트랙트 | 확인됨 (GitHub) |
| **AuthCaptureEscrow** | Solidity | 인가-캡처 에스크로 메인 컨트랙트 | 확인됨 (GitHub) |
| **Token Collectors** | Solidity | 5가지 결제 수집 모듈 (ERC-3009, Permit2 등) | 확인됨 (GitHub) |
| **Token Stores** | Solidity (CREATE2) | 오퍼레이터별 결정적 배포 보관소 | 확인됨 (GitHub) |
| **Uniswap V3 Router** | 외부 의존성 | DEX 토큰 스왑 | 확인됨 (GitHub) |

#### API 및 SDK

| 구성요소 | 기술 | 신뢰도 |
|---------|------|--------|
| RESTful Commerce API | HTTPS/JSON | 확인됨 |
| Webhook 알림 시스템 | HMAC 서명 검증 | 확인됨 |
| Commerce SDK (Go) | Go | 확인됨 (GitHub 샘플) |
| Payment Acceptance API | REST | 확인됨 (공식 문서) |
| Rate Limit | 10,000 req/hr, 100 req/s burst | 확인됨 |

#### 배포 네트워크

| 네트워크 | 상태 | 특성 |
|---------|------|------|
| **Base** | 핵심 (Production) | Coinbase 운영 L2, 약 200ms, 가스비 약 $0.01 |
| **Ethereum** | Production | 메인넷, 높은 보안, 높은 가스비 |
| **Polygon** | Production | L2, 저비용 |

---

## 5. Commerce Payments Protocol 기술 심층 분석

### 5.1 아키텍처 개요

Commerce Payments Protocol은 Coinbase와 Shopify가 공동 개발한 오픈소스 온체인 결제 프로토콜이다. 전통 카드 결제의 인가-캡처 모델을 스마트 컨트랙트로 구현하여, 상거래에 필수적인 다단계 결제 흐름을 블록체인 위에서 처리한다.

```
[Commerce Payments Protocol 아키텍처]

+------------------+     +-------------------+     +------------------+
|    소비자 지갑     |     |   오퍼레이터       |     |   가맹점 지갑     |
|  (Any EVM Wallet) |     | (Coinbase/Shopify)|     |  (Self-Managed   |
|                  |     |                   |     |   or Managed)    |
+--------+---------+     +--------+----------+     +--------+---------+
         |                        |                         |
         |  1. 결제 서명          |                         |
         +----------------------->|                         |
         |                        |  2. 인가 TX 제출        |
         |                        +----------+              |
         |                        |          v              |
         |                +-------+----------+--------+     |
         |                |  AuthCaptureEscrow         |     |
         |                |  (에스크로 스마트 컨트랙트)   |     |
         |                |                            |     |
         |   자금 이동     |  +--- Token Collector ---+ |     |
         +--------------->|  | ERC-3009 / Permit2 /  | |     |
         |                |  | PreApproval / Spend   | |     |
         |                |  +----------------------+ |     |
         |                |                            |     |
         |                |  +--- Token Store -------+ |     |
         |                |  | (CREATE2 배포)         | |     |
         |                |  | 오퍼레이터별 격리 보관  | |     |
         |                |  +----------------------+ |     |
         |                |                            |     |
         |                +-------+--------------------+     |
         |                        |                         |
         |                        |  3. 캡처 -> 가맹점      |
         |                        +------------------------>|
         |                        |                         |
         |  6. 환불 (선택적)       |  4. Void/Reclaim        |
         |<-----------------------+                         |
         |                        |  5. Refund (선택적)      |
         |<-----------------------+-------------------------|
```

### 5.2 핵심 컨트랙트 구조

#### AuthCaptureEscrow (메인 컨트랙트)

중앙 에스크로 컨트랙트로, 결제 생명주기 전체를 관리한다.

**핵심 책임:**
- 결제 파라미터 및 타이밍 제약 검증
- 결제 상태 추적 (authorized / captured / refunded)
- 수수료 유연 분배
- 재진입 방지를 위한 원자적 연산 보장

#### PaymentInfo 구조체

모든 결제는 불변(immutable)한 구조체로 정의된다:

```solidity
struct PaymentInfo {
    address operator;        // 오퍼레이터 주소
    address payer;           // 결제자 주소
    address receiver;        // 수령자(가맹점) 주소
    address token;           // 결제 토큰 주소
    uint120 maxAmount;       // 최대 결제 금액
    uint48  authExpiry;      // 인가 만료 시점
    uint48  captureExpiry;   // 캡처 만료 시점
    uint48  refundExpiry;    // 환불 만료 시점
    uint16  minFeeBps;       // 최소 수수료 (basis points)
    uint16  maxFeeBps;       // 최대 수수료 (basis points)
    address feeReceiver;     // 수수료 수령자
    bytes32 salt;            // 고유 식별을 위한 솔트
}
```

**Payment ID 생성**: 구조체 해시 + 체인 ID + 컨트랙트 주소의 조합으로 결정론적 생성. 동일 결제가 다른 네트워크에서 중복 실행되는 것을 방지한다.

#### Token Collectors (5가지 결제 수집 모듈)

| 모듈 | 메커니즘 | 특성 |
|------|---------|------|
| **ERC3009PaymentCollector** | ERC-3009 `receiveWithAuthorization` 서명 | USDC 네이티브 메타 트랜잭션 |
| **Permit2PaymentCollector** | Uniswap Permit2 서명 기반 전송 | 가스리스 승인 |
| **PreApprovalPaymentCollector** | 전통 ERC-20 allowance 흐름 | 기존 승인 패턴 호환 |
| **SpendPermissionPaymentCollector** | Coinbase Spend Permission 통합 | Coinbase 지갑 네이티브 |
| **OperatorRefundCollector** | 오퍼레이터 자금 기반 환불 | 환불 유동성 공급 |

#### Token Stores (오퍼레이터별 보관소)

- **CREATE2 결정론적 배포**: 최소 프록시 패턴으로 가스 효율성 확보
- **유동성 격리**: 오퍼레이터별 독립 보관소로 자금 혼재 방지
- **보안 경계**: 한 오퍼레이터의 손상이 다른 오퍼레이터 자금에 영향 불가

### 5.3 6가지 결제 연산 (Payment Operations)

#### 결제 개시 연산

**1. Authorize (인가)**
```
소비자 지갑 -> Token Collector -> Token Store (에스크로)
```
- 소비자 자금을 에스크로에 예치
- 지연 정산을 가능하게 하면서도 가맹점 수령을 보장
- `authExpiry` 이후에는 소비자가 직접 `Reclaim` 가능

**2. Charge (즉시 결제)**
```
소비자 지갑 -> Token Collector -> 가맹점 지갑 (단일 트랜잭션)
```
- 인가 + 캡처를 단일 트랜잭션으로 합침
- 즉시 정산이 필요한 디지털 상품/서비스에 적합

#### 정산 및 취소 연산

**3. Capture (캡처/정산)**
```
Token Store (에스크로) -> 가맹점 지갑 + 수수료 수령자
```
- 부분 캡처 지원 (partial capture)
- 유연한 수수료 분배 (minFeeBps ~ maxFeeBps 범위)
- 오퍼레이터만 실행 가능

**4. Void (취소)**
```
Token Store (에스크로) -> 소비자 지갑 (전액 반환)
```
- 캡처 전 결제 인가를 취소
- 오퍼레이터만 실행 가능
- 아직 캡처되지 않은 모든 인가에 대해 언제든 호출 가능

**5. Reclaim (회수)**
```
Token Store (에스크로) -> 소비자 지갑 (만료 후)
```
- `authExpiry` 이후에만 소비자가 직접 호출 가능
- 오퍼레이터 응답 없는 경우의 안전장치
- 신뢰 최소화(trust-minimized) 자금 보호 메커니즘

#### 환불 연산

**6. Refund (환불)**
```
환불 자금 출처 (Refund Collector) -> 소비자 지갑
```
- 캡처된 결제에 대한 부분/전액 환불 지원
- 모듈러 Refund Collector를 통한 유연한 유동성 소싱
- `refundExpiry` 이전에만 가능

### 5.4 Transfers.sol 핵심 함수

Onchain Payment Protocol의 초기 버전(Legacy Commerce)에서 사용되는 Transfers.sol의 핵심 함수:

| 함수 | 기능 | 사용 시나리오 |
|------|------|-------------|
| `transferTokenPreApproved` | 사전 승인된 토큰 전송 | 표준 ERC-20 결제 |
| `wrapAndTransfer` | 네이티브 통화(ETH) -> 래핑(wETH) 후 전송 | ETH 직접 결제 |
| `unwrapAndTransferPreApproved` | 래핑 통화 언래핑 후 전송 | wETH -> ETH 변환 결제 |
| `swapAndTransferUniswapV3Native` | 네이티브 통화 -> Uniswap V3 스왑 후 전송 | ETH로 결제 -> 가맹점 USDC 수령 |

### 5.5 오퍼레이터 모델

프로토콜은 **퍼미션리스(permissionless)이면서 신뢰 최소화(trust-minimized)된 오퍼레이터** 모델을 채택한다.

**오퍼레이터의 역할:**
- 에스크로를 통한 결제 흐름 구동
- 트랜잭션 가스비 부담
- 백그라운드 자동화 활성화 (캡처 타이밍, 환불 처리 등)

**오퍼레이터가 할 수 없는 것 (보안 제약):**
- 원래 결제 의도(payment intent) 수정 불가
- 수령자 주소 변경 불가
- 결제 토큰 변경 불가
- 최대 결제 금액 초과 불가
- 만료 시점 변경 불가

**오퍼레이터 손상 시나리오 대비:**
- 자금은 항상 에스크로에 격리
- `authExpiry` 이후 소비자 직접 Reclaim 가능
- Token Store 간 유동성 격리로 피해 범위 제한

### 5.6 보안 모델

| 보안 계층 | 메커니즘 |
|----------|---------|
| **접근 제어** | 연산별 호출자 제한 (오퍼레이터/소비자) |
| **시간 기반 제약** | authExpiry, captureExpiry, refundExpiry 3중 만료 |
| **잔액 검증** | 에스크로 잔액 사전 검증 |
| **유동성 격리** | 오퍼레이터별 Token Store 분리 |
| **재진입 방지** | 원자적 연산 보장 |
| **토큰 거부 목록** | 악성 토큰 차단 고려 |
| **불변 결제 의도** | PaymentInfo 구조체 수정 불가 |

---

## 6. 결제-정산-환불 기술 아키텍처

### 6.1 결제 (Payment) 기술 플로우

```
[결제 기술 플로우 -- 상세]

1. 가맹점 -> Commerce API (REST)
   POST /charges
   {
     pricing_type: "fixed_price",
     local_price: { amount: "100.00", currency: "USD" },
     metadata: { order_id: "..." }
   }
   -> Charge 객체 생성 (charge_id, hosted_url, expires_at)

2. 소비자 -> hosted_url 접속 (Commerce Checkout UI)
   -> 지원 토큰/네트워크 선택
   -> 실시간 환율 기반 암호화폐 금액 계산
   -> QR 코드 또는 지갑 연결 (WalletConnect / Coinbase Wallet)

3. 소비자 지갑 -> 온체인 트랜잭션 실행
   [Commerce Payments Protocol 경로]
   -> AuthCaptureEscrow.authorize() 또는 charge()
   -> Token Collector가 자금 수집
   -> (DEX 스왑 필요 시) Uniswap V3 Router로 토큰 스왑
   -> 가맹점 지정 토큰(USDC)으로 변환
   -> 1% Commerce 수수료 자동 차감 (feeReceiver)
   -> 에스크로 또는 가맹점 지갑에 자금 도달

   [Legacy 경로]
   -> Transfers.sol의 해당 함수 호출
   -> transferTokenPreApproved / swapAndTransferUniswapV3Native
   -> 원자적 실행: 성공 시 정확한 금액 수령, 실패 시 전액 롤백

4. Commerce API -> Webhook 알림
   POST {merchant_webhook_url}
   X-CC-Webhook-Signature: {HMAC-SHA256}
   {
     event: { type: "charge:confirmed", data: {...} }
   }
```

### 6.2 정산 (Settlement) 기술 플로우

```
[정산 기술 플로우 -- Self-Managed]

1. 결제 완료 -> 가맹점 자체 지갑에 직접 정산
   (비수탁형: 12단어 시드 구문으로 관리)
   -> Base 네트워크: 약 200ms
   -> Ethereum: 블록 확인 시간 (약 12초 + 확정 대기)
   -> 정산 완료

[정산 기술 플로우 -- Coinbase-Managed]

1. 결제 완료 -> Coinbase Exchange 연동 계정에 수령
2. 자동 환전 활성화 시:
   -> 수령 즉시 Coinbase Exchange 내부 매칭 엔진에서 USD 환전
   -> 스프레드 적용 (약 1-1.5%)
3. 은행 출금 요청:
   -> ACH / Wire Transfer -> 가맹점 은행 계좌
   -> 소요 시간: 1-3 영업일

[정산 기술 플로우 -- Commerce Payments Protocol (Authorize-Capture)]

1. Authorize -> 자금이 에스크로에 보관
2. 가맹점이 상품 준비 완료 후:
   -> 오퍼레이터가 capture() 호출
   -> 에스크로에서 가맹점 지갑으로 자금 이동
   -> 수수료 자동 분배
3. 부분 캡처 지원:
   -> 주문의 일부만 이행 가능한 경우
   -> 남은 금액은 후속 캡처 또는 Void 처리
```

### 6.3 환불 (Refund) 기술 플로우

```
[환불 기술 플로우 -- Self-Managed]

1. 소비자 -> 가맹점에 환불 요청 (오프체인 커뮤니케이션)
2. 가맹점 -> 소비자 수령 주소 확인
3. 가맹점 -> 자체 지갑에서 직접 온체인 전송
   (Commerce API를 통한 자동 환불 불가)
4. 네트워크 가스비는 가맹점 부담

[환불 기술 플로우 -- Coinbase-Managed]

1. 소비자 -> 가맹점에 환불 요청
2. 가맹점 -> Coinbase Exchange 인터페이스에서 환불 처리
3. (법정화폐로 환전된 경우) 재환전 필요
4. Coinbase Exchange -> 소비자에게 자금 전송

[환불 기술 플로우 -- Commerce Payments Protocol]

1. 캡처 전 (Void):
   -> 오퍼레이터가 void() 호출
   -> 에스크로에서 소비자 지갑으로 전액 반환
   -> 수수료 미발생

2. 캡처 후, refundExpiry 이전 (Refund):
   -> 오퍼레이터가 refund() 호출
   -> Refund Collector (OperatorRefundCollector)에서 유동성 공급
   -> 소비자 지갑으로 부분/전액 환불
   -> 부분 환불 지원

3. authExpiry 이후, 미캡처 상태 (Reclaim):
   -> 소비자가 직접 reclaim() 호출
   -> 에스크로에서 소비자에게 자금 반환
   -> 오퍼레이터 개입 불필요 (신뢰 최소화 안전장치)

4. refundExpiry 이후:
   -> 환불 불가 (최종 확정 상태)
```

---

## 7. Base L2 네트워크 기술 분석

### 7.1 아키텍처 개요

| 항목 | 상세 |
|------|------|
| 유형 | Optimistic Rollup (L2) |
| 원래 기반 | OP Stack (Optimism 협력) |
| 2026 전환 | **독자 "Unified Stack"**으로 이전 중 |
| 정산 레이어 | Ethereum L1 |
| 데이터 가용성 | Ethereum Blobs (EIP-4844, Dencun 업그레이드) |
| 시퀀서 운영 | Coinbase (중앙화, 탈중앙화 로드맵 진행 중) |
| 블록 시간 | 약 2초 |
| 가스비 | 약 $0.01 이하 |
| TPS | 수십-수백 TPS (부하에 따라 변동) |

### 7.2 Unified Stack 전환 (2026)

2026년 2월, Base 팀은 Optimism OP Stack에서 독자 "Unified Stack"으로의 이전을 공식 발표했다.

**전환 배경:**
- 시퀀서를 포함한 핵심 인프라를 `base/base` 단일 GitHub 리포로 통합
- Optimism, Flashbots, Paradigm 등 외부 기여자 의존도 감소
- 주요 업그레이드 속도를 연 6회 수준으로 2배 가속 목표

**Commerce에 미치는 영향:**
- 시퀀서 직접 통제로 결제 트랜잭션의 우선순위 최적화 가능성
- 결제 전용 프리컴파일(precompile) 추가 가능성 (추정)
- Commerce Payments Protocol과의 더 깊은 프로토콜 레벨 통합 가능

### 7.3 Commerce와 Base의 시너지

```
[수직 통합 구조]

Coinbase (회사)
  |
  +-- Base L2 (자체 블록체인)
  |     |
  |     +-- 시퀀서 운영 (트랜잭션 순서 결정)
  |     +-- 가스비 수익 수취
  |     +-- EIP-4844 blob을 통한 L1 데이터 게시
  |
  +-- Commerce Payments Protocol (결제 스마트 컨트랙트)
  |     |
  |     +-- AuthCaptureEscrow (Base 위 배포)
  |     +-- Transfers.sol (Base/ETH/Polygon 배포)
  |
  +-- USDC (Circle 파트너십)
  |     |
  |     +-- Base 위 네이티브 USDC 발행
  |     +-- 준비금 이자 수익 분배
  |
  +-- Coinbase Wallet
  |     |
  |     +-- SpendPermissionPaymentCollector 네이티브 통합
  |
  +-- Coinbase Exchange
        |
        +-- 법정화폐 환전 (USD/EUR 등)
        +-- 은행 출금
```

이 수직 통합은 Coinbase가 결제의 모든 계층 -- 블록체인 인프라, 결제 프로토콜, 스테이블코인 유통, 지갑, 거래소 -- 을 통제한다는 것을 의미한다. 전통 금융에서 Visa가 네트워크 + 프로세서 + 결제 표준을 소유하는 것과 유사한 구조이다.

---

## 8. 비수탁형(Non-Custodial) vs 수탁형(Custodial) 모델 분석

### 8.1 모델 비교

| 항목 | Self-Managed (비수탁형) | Coinbase-Managed (수탁형) |
|------|----------------------|-------------------------|
| **자금 통제** | 가맹점이 12단어 시드로 직접 관리 | Coinbase가 수탁 |
| **키 관리** | 가맹점 책임 (분실 시 자금 영구 손실) | Coinbase가 관리 |
| **카운터파티 리스크** | 없음 | Coinbase 파산/해킹 시 리스크 존재 |
| **법정화폐 정산** | 불가 (암호화폐만) | 가능 (USD 등) |
| **환불 프로세스** | 수동 (가맹점 직접 전송) | Exchange 통해 체계적 처리 |
| **규제 준수** | 가맹점이 직접 관리 | Coinbase 인프라 활용 |
| **타깃 고객** | 암호화폐 네이티브 비즈니스 | 전통 이커머스, 규제 준수 필요 기업 |

### 8.2 Commerce Payments Protocol의 하이브리드 접근

Commerce Payments Protocol은 양쪽의 장점을 결합한다:
- **에스크로 기반**: 자금은 스마트 컨트랙트에 보관 (중앙화된 수탁자 없음)
- **오퍼레이터 관리**: Coinbase/Shopify가 결제 흐름을 운영하되, 자금 접근 불가
- **소비자 안전장치**: Reclaim 함수로 오퍼레이터 무응답 시 자금 회수
- **결과적으로**: 스마트 컨트랙트가 "프로그래밍 가능한 에스크로 에이전트" 역할

---

## 9. 투자 및 재무 현황

### 9.1 Coinbase Global 투자 이력

| 라운드 | 시기 | 금액 | 밸류에이션 | 주요 투자자 |
|--------|------|------|-----------|-----------|
| Seed | 2012.09 | $600K | - | Y Combinator |
| Series A | 2013.05 | 약 $6.1M | - | Andreessen Horowitz (a16z) |
| Series D | 2017.08 | $100M | $1.6B | IVP, Spark Capital |
| Series E | 2018.10 | $300M | $8B (Pre-money $7.7B) | Tiger Global, Y Combinator |
| Post-IPO | 2021.05 | $1.25B | - | ARK Investment 등 |
| **IPO (Direct Listing)** | **2021.04.14** | - | **약 $86B (시초가 기준)** | NASDAQ: COIN |

- **총 투자자 수**: 144 (기관 138, 엔젤 6)
- **현재 시가총액**: 약 $46B (2026.04)
- **52주 범위**: $139.36 - $444.65

### 9.2 재무 성과 요약 (2025)

| 지표 | 수치 |
|------|------|
| 연간 매출 | $7.181B (YoY +9.4%) |
| 구독/서비스 수익 | YoY +23% |
| USDC 관련 수익 | 약 $1.35B (전체의 약 19%) |
| 총 거래량 | 역대 최고 (YoY +156%) |
| 암호화폐 거래 시장 점유율 | YoY +103% |
| 플랫폼 자산 | $516B |
| Q4 조정 EBITDA | $566M |
| EBITDA 흑자 연속 분기 | 12분기 |

---

## 10. 파트너십 및 생태계

### 10.1 핵심 파트너십

| 파트너 | 관계 | 전략적 의미 |
|--------|------|-----------|
| **Shopify** | Commerce Payments Protocol 공동 개발, 네이티브 USDC 결제 통합 | 수백만 가맹점 접근, 결제 표준화 시도 |
| **Circle** | USDC 공동 발행/관리, 준비금 이자 수익 분배 | 핵심 수익원, 스테이블코인 생태계 장악 |
| **Optimism (과거)** | OP Stack 기반 Base L2 구축 | 이더리움 L2 생태계 진입 (현재 독자 스택 전환 중) |
| **Uniswap** | V3 Router를 통한 DEX 토큰 스왑 | 다중 토큰 결제 -> USDC 자동 변환 핵심 인프라 |
| **AWS** | 핵심 클라우드 인프라 파트너 | 비용 62% 절감, 스케일링 시간 50% 단축 |

### 10.2 이커머스 통합

| 플랫폼 | 통합 수준 | 특징 |
|--------|---------|------|
| **Shopify** | 네이티브 (Shopify Payments 내장) | 별도 게이트웨이 불필요, 체크아웃 네이티브 |
| WooCommerce | 플러그인 | WordPress 이커머스 |
| BigCommerce | 플러그인 | 엔터프라이즈 이커머스 |
| 커스텀 통합 | REST API + Webhook | 자체 개발 쇼핑몰 |

### 10.3 오픈소스 생태계

| 리포지토리 | 설명 |
|-----------|------|
| `coinbase/commerce-onchain-payment-protocol` | Onchain Payment Protocol 스마트 컨트랙트 |
| `base/commerce-payments` | Commerce Payments Protocol (Shopify 공동) |
| `coinbase-samples/commerce-sdk-go` | Go SDK 샘플 |

---

## 11. 확장성 평가

### 11.1 확장 가능 요인

| 요인 | 설명 | 영향도 |
|------|------|--------|
| **Shopify 가맹점 확장** | 수백만 가맹점에 대한 즉시 접근 가능 인프라 확보 | 높음 |
| **멀티체인 지원** | Base/Ethereum/Polygon 이미 지원, EVM 호환 네트워크 추가 용이 | 중간 |
| **USDC 규제 확립** | GENIUS Act로 스테이블코인 법적 기반 확보 | 높음 |
| **Unified Stack** | Base 독자 스택으로 업그레이드 속도 2배, 결제 최적화 가능 | 중간-높음 |
| **Coinbase Business 통합** | Commerce + Exchange + Custody 원스톱 솔루션 | 높음 |
| **프로토콜 표준화** | Commerce Payments Protocol의 업계 표준 채택 가능성 | 높음 (장기) |

### 11.2 병목 요인

| 병목 | 설명 | 심각도 |
|------|------|--------|
| **사용자 경험 격차** | 지갑 관리, 가스비 이해 등 진입장벽 | 높음 |
| **법정화폐 정산 제한** | Self-Managed에서 법정화폐 인출 불가 | 중간 |
| **시퀀서 중앙화** | Base 시퀀서를 Coinbase 단독 운영, 검열 리스크 | 중간 |
| **환불 복잡성** | 전통 결제 대비 환불 프로세스가 복잡 | 중간-높음 |
| **규제 지역 차이** | MiCA (EU), GENIUS Act (US) 등 국가별 상이한 준수 요구 | 중간 |
| **Commerce -> Business 전환 혼란** | 통합 과도기 가맹점 이탈 가능성 | 낮음-중간 |
| **오라클/환율 의존성** | 실시간 환율에 의존하는 가격 산정, DEX 유동성 의존 | 낮음 |

### 11.3 경쟁 우위 지속가능성 (Moat) 평가

| 해자(Moat) 요소 | 강도 | 근거 |
|----------------|------|------|
| **네트워크 효과** | 강함 | 1억+ Coinbase 사용자 -> 가맹점 유입 -> 사용자 결제 편의 증가 |
| **수직 통합** | 매우 강함 | 블록체인(Base) + 프로토콜 + 스테이블코인(USDC) + 지갑 + 거래소 |
| **전환 비용** | 중간 | API 통합 후 전환 비용 존재하나, 표준 REST API로 전환 장벽 높지 않음 |
| **규제 장벽** | 강함 | 미국 상장 기업, GENIUS Act 준수 인프라 선점 |
| **브랜드 신뢰** | 강함 | 미국 최대 규제 준수 암호화폐 거래소 브랜드 |
| **기술 표준화** | 잠재적 | Commerce Payments Protocol이 업계 표준이 되면 강력한 해자 |

---

## 12. 핵심 인사이트

### 12.1 비즈니스 모델의 핵심 특징

**"결제를 미끼로, USDC 생태계를 낚시하는 구조"**

Coinbase Commerce의 1% 거래 수수료는 그 자체로는 크지 않은 수익원이다. 진정한 수익 엔진은 Commerce를 통해 USDC 사용과 플랫폼 보유량을 증가시키고, 이를 통해 Circle과의 준비금 이자 수익 분배에서 극대화된 수익을 얻는 구조이다.

- Commerce 1% 수수료 수익 < USDC 준비금 이자 수익 ($1.35B, 2025)
- Commerce는 USDC 채택 가속기(adoption accelerator) 역할
- Shopify 파트너십은 USDC 유통량 증대 전략의 핵심 축

### 12.2 기술적 차별화 포인트

1. **유일한 수직 통합 결제 스택**: L2 블록체인 + 결제 프로토콜 + 스테이블코인 + 지갑 + 거래소를 단일 기업이 소유
2. **Commerce Payments Protocol**: 전통 카드 결제의 인가-캡처-환불을 온체인으로 구현한 최초이자 유일한 프로덕션 프로토콜
3. **원자적 결제 보장**: 부분 결제, 잘못된 금액, 잘못된 주소 결제가 구조적으로 불가능
4. **모듈러 아키텍처**: Token Collector / Token Store / Refund Collector의 플러그인 구조로 새로운 결제 수단/환불 방식 추가 용이

### 12.3 리스크 요인

1. **중앙화 역설**: 탈중앙화를 표방하면서도 Base 시퀀서, 오퍼레이터, USDC 생태계 모두 Coinbase가 통제
2. **규제 리스크**: GENIUS Act 완전 시행 전 불확실성, MiCA 이중 라이선스 부담
3. **플랫폼 전환 리스크**: Commerce -> Business 통합 과도기의 가맹점 혼란
4. **경쟁 심화**: Stripe (1.5% 암호화폐 결제), PayPal, 그리고 BTCPay Server (무료 오픈소스)의 양면 압박

### 12.4 전망

- **단기 (2026 H2)**: Coinbase Business 통합 완료, Commerce Payments Protocol Shopify 외 플랫폼 확장
- **중기 (2027-2028)**: GENIUS Act 완전 시행으로 스테이블코인 결제 주류화, Base Unified Stack 완성
- **장기**: Commerce Payments Protocol이 온체인 결제 표준으로 자리잡을 경우, Coinbase는 "블록체인의 Visa"로 포지셔닝

---

## 참조 소스

1. [Coinbase Developer Documentation](https://docs.cdp.coinbase.com/)
2. [Coinbase Commerce Onchain Payment Protocol Deep Dive](https://www.coinbase.com/blog/coinbase-commerce-onchain-payment-protocol-deep-dive)
3. [Shopify Engineering - Commerce Payments Protocol (2025)](https://shopify.engineering/commerce-payments-protocol)
4. [Base Engineering Blog - Commerce Payments Protocol](https://blog.base.dev/commerce-payments-protocol)
5. [GitHub - coinbase/commerce-onchain-payment-protocol](https://github.com/coinbase/commerce-onchain-payment-protocol)
6. [GitHub - base/commerce-payments](https://github.com/base/commerce-payments/blob/main/docs/README.md)
7. [Finextra - Deep Dive: Coinbase's Commerce Payments Protocol](https://www.finextra.com/blogposting/29130/deep-dive-coinbases-commerce-payments-protocol-how-to-use-it-integrate-it-and-win-with-it)
8. [FinTech Wrap Up - Programmable Payments with Coinbase Commerce Protocol](https://www.fintechwrapup.com/p/deep-dive-coinbases-commerce-payments)
9. [Coinbase Blog - Powering the Future of Ecommerce: Introducing Coinbase Payments](https://www.coinbase.com/blog/powering-the-future-of-ecommerce-introducing-coinbase-payments)
10. [Coinbase Blog - Blockchain Infrastructure at Coinbase](https://www.coinbase.com/blog/blockchain-infrastructure-at-coinbase)
11. [Coinbase Blog - Building Enterprise AI Agents at Coinbase](https://www.coinbase.com/blog/building-enterprise-AI-agents-at-Coinbase)
12. [Coinbase Data Tech Stack Analysis](https://www.junaideffendi.com/p/coinbase-data-tech-stack)
13. [Surf - What Tech Stack Did Coinbase Developer Use?](https://surf.dev/coinbase-tech-stack-technologies-that-power-the-cryptocurrency-platform/)
14. [StackShare - Coinbase Tech Stack](https://stackshare.io/coinbase/coinbase)
15. [Base Engineering Blog - Unified Stack Announcement](https://blog.base.dev/next-chapter-for-base-chain-1)
16. [Coinbase IR - Q4 2025 Earnings](https://investor.coinbase.com/news/news-details/2026/Coinbase-Delivers-on-Q4-Financial-Outlook-Doubles-Total-Trading-Volume-and-Crypto-Trading-Volume-Market-Share-in-2025/default.aspx)
17. [Decrypt - Coinbase Takes 50% Share of Circle's Residual USDC Reserve Revenue](https://decrypt.co/312757/coinbase-circles-residual-usdc-reserve-revenue-filing)
18. [Bloomberg Intelligence via Bitcoin Ethereum News - Coinbase USDC Revenues Hit 19% Record in 2025](https://bitcoinethereumnews.com/tech/coinbase-usdc-revenues-hit-19-record-in-2025/)
19. [Coinbase Help - Commerce Fees](https://help.coinbase.com/en/commerce/getting-started/fees)
20. [Coinbase Help - Using Commerce APIs](https://help.coinbase.com/en/cloud/api/commerce/using-apis)
21. [Coinbase Careers - Backend Engineer Positions](https://www.coinbase.com/careers/positions/6650914)
22. [Crunchbase - Coinbase Company Profile](https://www.crunchbase.com/organization/coinbase)
23. [Block Finances - Coinbase Commerce Review 2026](https://blockfinances.fr/en/coinbase-commerce-review-fees-guide)
24. [CoinDesk - Base Strategy for 2026](https://www.coindesk.com/tech/2026/03/31/coinbase-s-base-to-focus-on-tokenized-markets-stablecoins-developers-this-year)
25. [Payment Acceptance API Documentation](https://docs.cdp.coinbase.com/api-reference/payment-acceptance/overview)

---

*본 보고서의 기술 스택 정보 중 "추정"으로 표기된 항목은 채용공고, 기술 블로그, 서드파티 분석을 교차 검증한 결과이나 공식 확인되지 않은 내용입니다. "확인됨"은 공식 문서, GitHub 리포, 또는 공식 블로그에서 직접 확인된 내용입니다.*
