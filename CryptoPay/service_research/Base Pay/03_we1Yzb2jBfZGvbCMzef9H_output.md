# 비즈니스 모델 및 기술 프로파일 -- Base Pay (Commerce Payments Protocol)

## 분석 개요

- **분석 대상**: Base Pay / Commerce Payments Protocol -- Coinbase L2 블록체인 Base 네트워크 기반 결제 인프라
- **분석 일시**: 2026-04-14
- **주요 참조 소스**:
  - [GitHub: coinbase/commerce-onchain-payment-protocol](https://github.com/coinbase/commerce-onchain-payment-protocol) -- Solidity, Apache 2.0
  - [GitHub: base/commerce-payments](https://github.com/base/commerce-payments) -- 차세대 Auth+Capture 에스크로 프로토콜
  - [GitHub: coinbase/x402](https://github.com/coinbase/x402) -- HTTP 기반 결제 프로토콜
  - [Coinbase Commerce Protocol Deep Dive](https://www.coinbase.com/blog/coinbase-commerce-onchain-payment-protocol-deep-dive)
  - [Shopify: Commerce Payments Protocol](https://shopify.engineering/commerce-payments-protocol)
  - [Base Blog: Commerce Payments Protocol](https://blog.base.dev/commerce-payments-protocol)
  - [Fintech Wrapup: Deep Dive Coinbase Commerce](https://www.fintechwrapup.com/p/deep-dive-coinbases-commerce-payments)
  - [x402 EVM Scheme Spec](https://github.com/coinbase/x402/blob/main/specs/schemes/exact/scheme_exact_evm.md)
  - [Coinbase Commerce Fees](https://help.coinbase.com/en/commerce/getting-started/fees)

---

## 1. 비즈니스 모델 요약

### 1.1 수익 유형 분류

| 구분 | 내용 | 신뢰도 |
|------|------|--------|
| **수익 모델** | 거래수수료 기반 SaaS (Payment Infrastructure as a Service) | 확인됨 |
| **핵심 수익원 1** | Commerce 결제 수수료 (1% per transaction) | 확인됨 |
| **핵심 수익원 2** | Base 네트워크 시퀀서 수수료 (sequencer fees) | 확인됨 |
| **핵심 수익원 3** | USDC 발행 수익 분배 (Circle과의 Revenue Share) | 확인됨 |
| **핵심 수익원 4** | x402 Facilitator 서비스 (월 1,000건 무료, 이후 과금) | 확인됨 |
| **부가 수익원** | Coinbase Business 플랫폼 커스터디/환전 수수료 | 추정 |

### 1.2 핵심 가치 제안

- **머천트 관점**: 1% 수수료, 차지백 제로, 서브초 정산, 글로벌 무국경 결제
- **구매자 관점**: 어떤 토큰으로든 결제 가능 (Uniswap V3 자동 스왑), 가스비 $0.01 수준
- **개발자 관점**: 오픈소스 프로토콜, 퍼미션리스 오퍼레이터 등록, 프로그래머블 결제 흐름

### 1.3 주요 고객 세그먼트

| 세그먼트 | 구체적 대상 | 접근 채널 |
|----------|-------------|-----------|
| **이커머스 머천트** | Shopify 스토어, 독립 온라인 몰 | Shopify 네이티브 플러그인, Coinbase Business |
| **API 서비스 제공자** | AI 에이전트 서비스, 유료 API | x402 프로토콜 통합 |
| **크로스보더 비즈니스** | 국제 거래 기업, 프리랜서 플랫폼 | USDC 정산, Base 네트워크 |
| **DApp 개발자** | 온체인 앱 내 결제 통합 | 오픈소스 컨트랙트 직접 통합 |

---

## 2. 가격 체계

### 2.1 Coinbase Commerce 수수료

| 항목 | 금액 | 비고 |
|------|------|------|
| **플랫폼 수수료** | 1% | 정산 통화에서 차감 |
| **네트워크 가스비 (Base)** | ~$0.01 | 구매자 부담 |
| **네트워크 가스비 (Ethereum)** | 변동 ($1~$50+) | 네트워크 혼잡도에 따라 |
| **토큰 스왑 수수료** | DEX 슬리피지 | 구매자-머천트 토큰이 다를 경우 |
| **월간 구독료** | 없음 | |
| **설정비** | 없음 | |
| **환불 수수료** | 가스비만 발생 | 플랫폼 수수료 미환불 가능성 |

### 2.2 x402 Facilitator 수수료

| 티어 | 조건 | 가격 |
|------|------|------|
| **Free Tier** | Coinbase CDP Facilitator | 월 1,000건 무료 |
| **유료 티어** | 1,000건 초과 | 미공개 (추정: 건당 소액 과금) |
| **프로토콜 수수료** | x402 프로토콜 자체 | 0% (무료) |

### 2.3 경쟁사 수수료 비교

| 서비스 | 수수료 | 비고 |
|--------|--------|------|
| **Coinbase Commerce** | 1% | 온체인 정산 |
| **Stripe Crypto** | 1.5% | USD 직접 정산 지원 |
| **BitPay** | 1% | 법정화폐 직접 정산 |
| **NOWPayments** | 0.5% (+0.5% 환전) | 350+ 토큰 지원 |
| **BTCPay Server** | 0% (자체호스팅) | 인프라 비용 자부담 |

---

## 3. 수익 구조 심층 분석

### 3.1 다층적 수익 구조 (Revenue Stack)

Coinbase의 Base Pay 관련 수익은 단일 수수료가 아니라 **수직 통합된 다층 수익 구조**로 이해해야 한다.

```
Layer 4: Coinbase Business (커스터디, 환전, 은행 출금 수수료)
Layer 3: Commerce 결제 수수료 (1%)
Layer 2: x402 Facilitator 수수료 (건당)
Layer 1: Base 시퀀서 수수료 (모든 온체인 트랜잭션)
Layer 0: USDC Revenue Share (Circle 파트너십)
```

### 3.2 Layer 1 -- Base 시퀀서 수수료 (확인됨)

- **Q4 2025**: 약 $19M 총 시퀀서 수익, 순수익 약 $15M (L1 데이터 비용 및 OP Collective 수익 분배 후)
- **2025년 연간**: $75.4M (L2 전체 수익의 62%)
- **구조**: Base에서 발생하는 모든 트랜잭션의 가스비가 시퀀서(Coinbase 운영)에게 지급
- **Commerce 결제 트랜잭션도 포함**: 결제, 에스크로, 캡처, 환불 등 모든 온체인 동작에서 가스비 수취

출처: [Coinbase Q4 2025 Earnings](https://www.fool.com/earnings/call-transcripts/2026/02/13/coinbase-coin-q4-2025-earnings-call-transcript/), [RootData](https://www.rootdata.com/news/480230)

### 3.3 Layer 0 -- USDC Revenue Share (확인됨)

- **Q2 2025**: 스테이블코인 수익 $332.5M (전체 매출의 22%)
- **메커니즘**: Circle이 USDC 준비금(미국 단기 국채 등)에서 발생하는 이자 수익을 Coinbase와 분배
- **Base Pay 연관**: Commerce 정산 기본 통화가 USDC이므로, Base 내 USDC 유통량 증가가 직접적 수익 증대
- **2025년 글로벌 스테이블코인 결제 규모**: $9T (전년 대비 87% 증가)

출처: [Coinbase Q4 2025 Earnings](https://finance.yahoo.com/news/coinbase-global-inc-coin-q4-010216008.html)

### 3.4 Layer 3 -- Commerce 결제 수수료 (확인됨)

- **수수료율**: 1% (고정)
- **수수료 수취 방식**: `TransferIntent.feeAmount` 필드로 정의, 스마트 컨트랙트가 자동으로 오퍼레이터의 `feeDestination` 주소로 전송
- **수수료 차감 시점**: 결제 실행과 동시에 원자적(atomic)으로 처리
- **수수료 통화**: 머천트 정산 토큰과 동일 (일반적으로 USDC)

### 3.5 수익 모델의 전략적 의미

Coinbase는 Commerce 수수료(1%)만으로 수익을 추구하지 않는다. Base Pay는 다음을 동시에 달성하는 전략적 인프라다:

1. **Base 네트워크 트랜잭션 볼륨 증대** -> 시퀀서 수수료 증가
2. **USDC 유통량 증대** -> Circle Revenue Share 증가
3. **머천트/사용자 온보딩** -> Coinbase 생태계 전체 활성화
4. **오픈소스 표준화** -> 네트워크 효과로 경쟁 우위 강화

---

## 4. 기술 스택 분석

### 4.1 기술 스택 개요

| 계층 | 기술 | 신뢰도 |
|------|------|--------|
| **블록체인 (L1)** | Ethereum | 확인됨 |
| **블록체인 (L2)** | Base (OP Stack 기반 Optimistic Rollup) | 확인됨 |
| **스마트 컨트랙트** | Solidity ^0.8.17 | 확인됨 |
| **개발 프레임워크** | Foundry (Forge) | 확인됨 |
| **DEX 통합** | Uniswap V3 Universal Router | 확인됨 |
| **토큰 승인** | Permit2 (Uniswap), EIP-3009, EIP-2612 | 확인됨 |
| **x402 SDK** | TypeScript (주언어), Python, Rust | 확인됨 |
| **라이선스** | Apache License 2.0 | 확인됨 |
| **컨트랙트 의존성** | OpenZeppelin (ERC20, Pausable, ReentrancyGuard, ECDSA, Ownable) | 확인됨 |

### 4.2 스마트 컨트랙트 리포지토리 구조

Coinbase의 Commerce 결제 관련 스마트 컨트랙트는 **두 개의 별도 리포지토리**로 관리된다:

**리포 1: `coinbase/commerce-onchain-payment-protocol`** (1세대)
- 즉시 결제(Direct Transfer) 중심
- Transfers.sol 단일 컨트랙트
- Base, Ethereum, Polygon 배포
- 최종 업데이트: 2026-04-11

**리포 2: `base/commerce-payments`** (2세대)
- Auth+Capture 에스크로 중심
- AuthCaptureEscrow + Token Collectors 모듈 아키텍처
- 배포 주소: `0xBdEA0D1bcC5966192B070Fdf62aB4EF5b4420cff`
- 최종 업데이트: 2026-03-07

---

## 5. Commerce Onchain Payment Protocol (1세대) -- 결제 기술 심층 분석

### 5.1 TransferIntent 데이터 구조

`TransferIntent`는 프로토콜의 핵심 데이터 구조로, 오퍼레이터가 서명하는 결제 원시자료(signed payment primitive)다.

```solidity
struct TransferIntent {
    uint256 recipientAmount;      // 머천트 수령 금액
    uint256 deadline;             // 결제 마감 타임스탬프
    address payable recipient;    // 머천트 주소
    address recipientCurrency;    // 정산 토큰 주소 (address(0) = 네이티브)
    address refundDestination;    // 환불 수신 주소 (비어있으면 msg.sender)
    uint256 feeAmount;            // 오퍼레이터 수수료 (토큰 단위)
    bytes16 id;                   // 결제 추적용 고유 ID
    address operator;             // 오퍼레이터 주소 (서명자)
    bytes signature;              // 오퍼레이터의 서명
    bytes prefix;                 // 대체 서명 프리픽스 (비어있으면 EIP-191 기본)
}
```

**보안 설계 특징**:
- `signature`는 모든 필드 + `chainId` + `sender` + `contractAddress`를 `keccak256` 해시한 후 ECDSA 서명
- 오퍼레이터만 서명 가능하므로, 금액/수신자/수수료 변조 불가
- `deadline`으로 만료된 인텐트 실행 방지
- `processedTransferIntents` 매핑으로 중복 실행(replay) 방지

### 5.2 Transfers.sol 컨트랙트 아키텍처

```
Transfers.sol
├── 상속: Context, Ownable, Pausable, ReentrancyGuard, Sweepable, ITransfers
├── 불변 상태:
│   ├── uniswap: IUniversalRouter (Uniswap V3)
│   ├── permit2: Permit2 (토큰 승인/전송)
│   └── wrappedNativeCurrency: IWrappedNativeCurrency (WETH 등)
├── 가변 상태:
│   ├── feeDestinations: mapping(operator => feeAddress)
│   └── processedTransferIntents: mapping(operator => mapping(id => bool))
├── 검증 모디파이어:
│   ├── validIntent: 서명 검증, 만료 확인, 중복 방지
│   ├── operatorIsRegistered: 오퍼레이터 등록 확인
│   └── exactValueSent: 네이티브 통화 정확한 금액 확인
└── 결제 함수 9종 (아래 상세)
```

### 5.3 9가지 결제 함수 상세

#### 함수 1: `transferNative`
```
용도: 네이티브 통화(ETH/MATIC) 직접 전송
흐름: 구매자 ETH → 컨트랙트 검증 → 머천트 ETH + 오퍼레이터 수수료
조건: recipientCurrency == address(0), msg.value == recipientAmount + feeAmount
```

#### 함수 2: `transferToken`
```
용도: ERC-20 토큰 전송 (Permit2 서명 방식)
흐름: 구매자 서명 → Permit2.permitTransferFrom → 컨트랙트 → 머천트
조건: 구매자가 Permit2에 토큰 승인 필요
보안: fee-on-transfer 토큰 감지 (balanceBefore 비교)
```

#### 함수 3: `transferTokenPreApproved`
```
용도: ERC-20 토큰 전송 (전통적 approve 방식)
흐름: 구매자 approve → safeTransferFrom → 컨트랙트 → 머천트
조건: 구매자가 Transfers 컨트랙트에 직접 approve 필요
```

#### 함수 4: `wrapAndTransfer`
```
용도: ETH를 WETH로 래핑 후 전송
흐름: 구매자 ETH → WETH.deposit() → 머천트 WETH
사용 사례: 머천트가 WETH를 정산 토큰으로 선호할 경우
```

#### 함수 5: `unwrapAndTransfer`
```
용도: WETH를 ETH로 언래핑 후 전송 (Permit2)
흐름: 구매자 WETH → Permit2 → WETH.withdraw() → 머천트 ETH
```

#### 함수 6: `unwrapAndTransferPreApproved`
```
용도: WETH를 ETH로 언래핑 후 전송 (PreApproved)
흐름: 구매자 WETH approve → transferFrom → WETH.withdraw() → 머천트 ETH
```

#### 함수 7: `swapAndTransferUniswapV3Native`
```
용도: 네이티브 통화를 머천트 토큰으로 스왑 후 전송
흐름: 구매자 ETH → WETH → Uniswap V3 스왑 → 머천트 USDC
매개변수: poolFeesTier (Uniswap V3 풀 수수료 티어)
```

#### 함수 8: `swapAndTransferUniswapV3Token`
```
용도: 임의 ERC-20을 머천트 토큰으로 스왑 후 전송 (Permit2)
흐름: 구매자 DAI → Permit2 → Uniswap V3 → 머천트 USDC
```

#### 함수 9: `swapAndTransferUniswapV3TokenPreApproved`
```
용도: 임의 ERC-20을 머천트 토큰으로 스왑 후 전송 (PreApproved)
흐름: 구매자 DAI approve → Uniswap V3 → 머천트 USDC
매개변수: _tokenIn, maxWillingToPay, poolFeesTier
```

### 5.4 결제 함수 선택 로직

```
결제 요청 수신
├── 구매자 토큰 == 머천트 토큰?
│   ├── YES → 네이티브 통화?
│   │   ├── YES → transferNative
│   │   └── NO → Permit2 사용? → transferToken / transferTokenPreApproved
│   └── NO → 래핑/언래핑 관계?
│       ├── ETH→WETH → wrapAndTransfer
│       ├── WETH→ETH → unwrapAndTransfer / unwrapAndTransferPreApproved
│       └── 그 외 → Uniswap 스왑 필요
│           ├── 네이티브 지불 → swapAndTransferUniswapV3Native
│           └── 토큰 지불 → swapAndTransferUniswapV3Token / ...PreApproved
```

### 5.5 배포 주소

| 체인 | 환경 | 주소 |
|------|------|------|
| **Base** | Mainnet | `0xeADE6bE02d043b3550bE19E960504dbA14A14971` |
| **Base** | Sepolia | `0x96A08D8e8631b6dB52Ea0cbd7232d9A85d239147` |
| **Ethereum** | Mainnet | `0x1DAe28D7007703196d6f456e810F67C33b51b25C` |
| **Ethereum** | Sepolia | `0x96A08D8e8631b6dB52Ea0cbd7232d9A85d239147` |
| **Polygon** | Mainnet | `0xc2252Ce3348B8dAf90583E53e07Be53d3aE728FB` |
| **Polygon** | Amoy | `0x1A8f790a10D26bAd97dB8Da887D212eA49461cCC` |

---

## 6. Commerce Payments Protocol (2세대) -- Auth+Capture 에스크로 심층 분석

### 6.1 아키텍처 개요

2세대 프로토콜(`base/commerce-payments`)은 전통 결제 시스템의 Authorize-Capture 모델을 온체인으로 완전히 재현한다.

```
┌─────────────────────────────────────────────────────────────┐
│                   AuthCaptureEscrow                          │
│  (메인 에스크로 컨트랙트 - 결제 라이프사이클 관리)            │
│                                                              │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐    │
│  │Authorize │→│ Capture  │  │  Void    │  │ Refund   │    │
│  │(에스크로) │  │(정산)    │  │(취소)    │  │(환불)    │    │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘    │
│       ↑              ↑                           ↑          │
│  Token Collectors    Token Stores          Refund Collectors │
│  (자금 수집 모듈)    (에스크로 보관소)      (환불 자금 모듈) │
└─────────────────────────────────────────────────────────────┘
```

배포 주소: `0xBdEA0D1bcC5966192B070Fdf62aB4EF5b4420cff`

### 6.2 PaymentInfo 구조체

```solidity
struct PaymentInfo {
    address operator;              // 오퍼레이터 주소
    address payer;                 // 결제자 주소
    address receiver;              // 머천트(수신자) 주소
    address token;                 // 결제 토큰 컨트랙트
    uint256 maxAmount;             // 최대 승인 금액
    uint256 preApprovalExpiry;     // 사전 승인 만료 시점
    uint256 authorizationExpiry;   // 승인 만료 시점
    uint256 refundExpiry;          // 환불 가능 기한
    uint256 minFeeBps;             // 최소 수수료율 (basis points)
    uint256 maxFeeBps;             // 최대 수수료율 (basis points)
    address feeReceiver;           // 수수료 수신자
    bytes32 salt;                  // 고유 식별자
}
```

**결제 고유 ID**: `keccak256(PaymentInfo) + chainId + contractAddress`로 생성

### 6.3 6가지 결제 연산 (Payment Operations)

#### Operation 1: Authorize (승인)
```
목적: 구매자 자금을 에스크로에 예치
흐름: 구매자 → Token Collector → AuthCaptureEscrow(Token Store)
효과: 자금이 에스크로에 잠김, 머천트에게 결제 보장
시간 제한: authorizationExpiry까지 Capture 해야 함
```

#### Operation 2: Capture (캡처/정산)
```
목적: 에스크로 자금을 머천트에게 전달
흐름: AuthCaptureEscrow(Token Store) → 머천트 + 수수료 수신자
특징:
  - 부분 캡처(partial capture) 지원 (다중 배송 등)
  - 총 캡처 금액 <= 승인 금액
  - authorizationExpiry 이전에만 실행 가능
```

#### Operation 3: Charge (즉시 결제)
```
목적: Authorize + Capture를 단일 트랜잭션으로 결합
흐름: 구매자 → Token Collector → 머천트 + 수수료 (에스크로 거치지 않음)
사용 사례: 즉시 정산이 필요한 디지털 상품 등
```

#### Operation 4: Void (취소)
```
목적: 승인된 결제를 취소하고 에스크로 자금을 구매자에게 반환
흐름: AuthCaptureEscrow(Token Store) → 구매자
제약: 결제당 1회만 실행 가능, 남은 전체 승인 금액 반환
수수료: 발생하지 않음
```

#### Operation 5: Reclaim (회수)
```
목적: 만료된 승인의 에스크로 자금을 구매자가 직접 회수
흐름: AuthCaptureEscrow(Token Store) → 구매자
조건: authorizationExpiry 경과 후에만 실행 가능
역할: 오퍼레이터 오작동 시 안전장치
```

#### Operation 6: Refund (환불)
```
목적: Capture 완료 후 구매자에게 자금 반환
흐름: Refund Collector(다양한 소스) → 구매자
특징:
  - 환불 자금 소스가 유연 (머천트, 다른 주소, 오퍼레이터)
  - refundExpiry 이내에 실행 필요
  - 부분 환불 지원
```

### 6.4 결제 상태 다이어그램

```
                    ┌──────────┐
                    │  Created │
                    └────┬─────┘
                         │ authorize()
                         v
                    ┌──────────┐
              ┌─────│Authorized│─────┐
              │     └────┬─────┘     │
              │          │           │
         void()    capture()    [만료 후]
              │     (부분 가능)   reclaim()
              v          │           v
        ┌─────────┐      v     ┌──────────┐
        │ Voided  │  ┌────────┐│ Reclaimed│
        │(구매자  │  │Captured││(구매자   │
        │ 환불)   │  └───┬────┘│ 회수)    │
        └─────────┘      │     └──────────┘
                         │
                    refund()
                    (부분 가능)
                         │
                         v
                    ┌──────────┐
                    │ Refunded │
                    └──────────┘
```

---

## 7. Token Collector 모듈 심층 분석

### 7.1 아키텍처 설계 원칙

Token Collector는 "다양한 토큰 승인 표준을 추상화하는 플러그인 모듈" 시스템이다. 핵심 설계 원칙:

- **모듈화**: 새로운 토큰 승인 표준이 등장해도 코어 프로토콜 수정 없이 Collector만 추가
- **보안 격리**: Payment Collector와 Refund Collector 반드시 분리 (잔여 승인 오용 방지)
- **접근 제어**: `collectTokens()` 메서드는 오직 AuthCaptureEscrow만 호출 가능

### 7.2 TokenCollector 기본 인터페이스

```solidity
abstract contract TokenCollector {
    enum CollectorType { PAYMENT, REFUND }

    // 컬렉터 유형 반환 (결제용/환불용)
    function collectorType() external virtual returns (CollectorType);

    // 토큰 수집 실행 (AuthCaptureEscrow만 호출 가능)
    function collectTokens(...) external virtual;

    // 결제 상세와 서명 간 암호학적 연결을 위한 해시 유틸리티
    function payerAgnosticHash(...) external virtual returns (bytes32);
}
```

### 7.3 ERC3009PaymentCollector

| 항목 | 내용 |
|------|------|
| **표준** | EIP-3009 (Transfer With Authorization) |
| **지원 토큰** | USDC, EURC 등 EIP-3009 구현 토큰 |
| **동작 방식** | `receiveWithAuthorization()` 호출로 가스리스 서명 기반 전송 |
| **UX** | 단일 서명으로 결제 완료 (최상의 사용자 경험) |
| **제한** | EIP-3009 구현 토큰에만 사용 가능 (대부분의 ERC-20은 미지원) |
| **스마트 지갑** | ERC-6492 서명 지원 |

**기술 흐름**:
```
구매자 서명(off-chain) → Operator가 collectTokens() 호출
→ ERC3009Collector가 token.receiveWithAuthorization(from, to, value, validAfter, validBefore, nonce, signature) 실행
→ 토큰이 에스크로(Token Store)로 직접 이동
```

### 7.4 Permit2PaymentCollector

| 항목 | 내용 |
|------|------|
| **표준** | Uniswap Permit2 |
| **지원 토큰** | 모든 ERC-20 토큰 |
| **동작 방식** | Permit2의 서명 기반 전송 메커니즘 활용 |
| **전제조건** | 토큰별 1회 Permit2 컨트랙트에 approve 필요 |
| **UX** | 초기 1회 approve 후 서명만으로 결제 |
| **스마트 지갑** | ERC-6492 서명 지원 |

**기술 흐름**:
```
[1회] 구매자가 ERC-20.approve(Permit2Contract, MAX) 실행
구매자 Permit2 서명(off-chain) → collectTokens() 호출
→ Permit2Collector가 permit2.permitTransferFrom() 실행
→ 토큰이 에스크로로 이동
```

### 7.5 PreApprovalPaymentCollector

| 항목 | 내용 |
|------|------|
| **표준** | 전통적 ERC-20 approve/transferFrom |
| **지원 토큰** | 모든 ERC-20 토큰 |
| **동작 방식** | 표준 `transferFrom` 호출 |
| **전제조건** | 구매자가 Collector에 직접 approve 필요 |
| **UX** | 2개 트랜잭션 필요 (approve + 결제) |
| **가스리스** | 불가 |

### 7.6 SpendPermissionPaymentCollector

| 항목 | 내용 |
|------|------|
| **표준** | Coinbase Spend Permission |
| **지원 대상** | Coinbase Smart Wallet 사용자 전용 |
| **동작 방식** | SpendPermissionManager를 통한 위임 기반 전송 |
| **UX** | 단일 서명으로 결제 (ERC-6492 네이티브) |
| **특수 기능** | 구독(subscription) 스타일 반복 결제 지원 |
| **제한** | Coinbase Smart Wallet에서만 작동 |

**기술 흐름**:
```
구매자(Coinbase Smart Wallet) → SpendPermissionManager에 권한 부여
→ Collector가 SpendPermissionManager를 통해 자금 이동
→ 에스크로로 입금
```

### 7.7 OperatorRefundCollector

| 항목 | 내용 |
|------|------|
| **유형** | Refund Collector (환불 전용) |
| **동작 방식** | 오퍼레이터가 사전 승인한 자금에서 환불 |
| **자금 소스** | 오퍼레이터 잔고 (ERC-20 approve 기반) |
| **유연성** | 머천트, 별도 주소, 오퍼레이터 등 다양한 소스에서 환불 자금 조달 가능 |

### 7.8 Collector 선택 매트릭스

| 지갑 유형 | 토큰 | 권장 Collector | UX 품질 |
|-----------|------|----------------|---------|
| EOA | USDC/EURC | ERC3009 | 최상 (1 서명) |
| EOA | 기타 ERC-20 | Permit2 | 양호 (1회 approve + 서명) |
| EOA | 기타 ERC-20 | PreApproval | 보통 (2 트랜잭션) |
| Coinbase Smart Wallet | 모든 토큰 | SpendPermission | 최상 (1 서명 + 구독) |
| 기타 Smart Wallet | USDC | ERC3009 (ERC-6492) | 최상 |
| 기타 Smart Wallet | 기타 ERC-20 | Permit2 (ERC-6492) | 양호 |

---

## 8. x402 프로토콜 기술 분석

### 8.1 개요

x402는 Coinbase와 Cloudflare가 공동 개발한 HTTP 네이티브 결제 프로토콜이다. HTTP 402 "Payment Required" 상태 코드를 활용하여 웹 요청에 결제를 내장한다.

| 항목 | 내용 |
|------|------|
| **출시일** | 2025년 9월 |
| **리포지토리** | [coinbase/x402](https://github.com/coinbase/x402) |
| **주 언어** | TypeScript |
| **라이선스** | Apache 2.0 |
| **프로토콜 수수료** | 0% |
| **주 사용 토큰** | USDC (98.7% 점유율) |
| **누적 트랜잭션** | Base에서 1.19억 건, Solana에서 3,500만 건 (2026.03 기준) |
| **연간화 거래량** | ~$600M |

### 8.2 x402 결제 흐름

```
┌─────────┐     GET /resource      ┌─────────────┐
│  Client │ ───────────────────→  │   Server    │
│(AI Agent│                       │(Resource)   │
│ /User)  │  ←──────────────────  │             │
│         │  HTTP 402 + Invoice   │             │
│         │                       │             │
│         │  서명 생성 (EIP-3009)  │             │
│         │                       │             │
│         │  GET /resource        │             │
│         │  + PAYMENT-SIGNATURE  │             │
│         │  header               │             │
│         │ ───────────────────→  │             │
│         │                       │   ┌─────────────┐
│         │                       │   │ Facilitator │
│         │                       │   │ (검증+정산) │
│         │                       │   └─────────────┘
│         │  ←──────────────────  │             │
│         │  200 OK + Resource    │             │
└─────────┘                       └─────────────┘
```

### 8.3 세 가지 자산 전송 방식

#### 방식 1: EIP-3009 (주력)
```
대상 토큰: USDC, EURC 등 EIP-3009 지원 토큰
동작: transferWithAuthorization() 직접 호출
장점: 가스리스, 단일 서명, 가장 효율적
PAYMENT-SIGNATURE 헤더:
  - signature: 65바이트 인증 서명
  - authorization: {from, to, value, validAfter, validBefore, nonce}
```

#### 방식 2: Permit2 (범용 폴백)
```
대상 토큰: 모든 ERC-20
동작: x402ExactPermit2Proxy(0x402085c248EeA27D92E8b30b2C58ed07f9E20001)를 통한 전송
장점: 모든 ERC-20 호환
제약: Permit2 컨트랙트에 1회 approve 필요 (없으면 HTTP 412 반환)
프록시 주소: CREATE2로 모든 EVM 체인에 동일 주소 배포
```

#### 방식 3: ERC-7710 (스마트 계정 위임)
```
대상: 모듈식 스마트 계정
동작: delegationManager.redeemDelegations() 호출
장점: 반복 결제 지원, 스마트 계정 네이티브
검증: 시뮬레이션 기반 전체 검증
```

### 8.4 Facilitator 검증 프로세스

**EIP-3009 검증 단계**:
1. 서명 복원하여 `authorization.from` 일치 확인
2. 클라이언트 잔고 충분 여부 확인
3. 금액이 요구사항과 일치 확인
4. 유효 기간 미만료 확인
5. `transferWithAuthorization()` 시뮬레이션 실행

**Permit2 검증 단계**:
1. 서명 복원하여 `permit2Authorization.from` 일치 확인
2. Permit2 allowance 확인 (부족 시 HTTP 412 + `PERMIT2_ALLOWANCE_REQUIRED` 반환)
3. 토큰 잔고 충분 여부 확인
4. deadline 및 witness validity window 검증
5. 정산 호출 시뮬레이션

### 8.5 보안 설계

| 보안 메커니즘 | 설명 |
|---------------|------|
| **Witness 패턴** | Facilitator가 수신자 주소를 변경할 수 없도록 방지 |
| **프록시 보호** | Permit2 프록시가 수신자 변조를 방지 |
| **가스 제한** | 악의적 delegation manager 악용 방지 |
| **프라이빗 멤풀** | ERC-7710 레이스 컨디션 취약점 완화 |

---

## 9. 정산 기술 상세

### 9.1 정산 모드 비교

| 모드 | 프로토콜 | 정산 시간 | 사용 사례 |
|------|----------|-----------|-----------|
| **즉시 정산** | Transfers.sol (1세대) | ~2초 (Base) | 디지털 상품, 즉시 배송 |
| **Charge** | AuthCaptureEscrow (2세대) | ~2초 (Base) | 단일 트랜잭션 즉시 결제 |
| **에스크로 정산** | AuthCaptureEscrow (2세대) | Authorize 후 Capture까지 지연 | 실물 상품, 서비스 |
| **x402 정산** | x402 Facilitator | ~2초 (Base) | API 과금, 마이크로페이먼트 |

### 9.2 에스크로 정산 흐름 상세

```
Step 1: Authorize (승인)
  구매자 → Token Collector → Token Store(에스크로)
  - Token Store는 오퍼레이터별 격리된 보관소 (CREATE2 배포)
  - Minimal Proxy 패턴으로 가스 효율 최적화
  - authorizationExpiry 타이머 시작

Step 2: [대기 기간]
  - 머천트가 주문 확인, 재고 확인, 배송 준비 등
  - 이 기간 동안 Void 가능

Step 3: Capture (캡처)
  Token Store → 머천트 + 수수료 수신자
  - 부분 캡처 가능 (다중 배송)
  - 수수료율: minFeeBps ~ maxFeeBps 범위 내에서 결정
  - authorizationExpiry 이전에만 실행 가능
```

### 9.3 온체인 정산의 보장 사항

| 보장 | 메커니즘 |
|------|----------|
| **정확한 금액** | 스마트 컨트랙트가 정확한 금액만 전송 (fee-on-transfer 토큰 감지 및 거부) |
| **단일 결제** | processedTransferIntents / payment hash로 중복 방지 |
| **원자적 실행** | 전부 성공 또는 전부 실패 (부분 결제 불가) |
| **비업그레이드** | 배포 후 컨트랙트 수정 불가 (보안 보장) |
| **리엔트런시 방지** | ReentrancyGuard (1세대), 내장 reentrancy protection (2세대) |

---

## 10. 환불 기술 상세

### 10.1 환불 시나리오별 처리

#### 시나리오 A: 에스크로 단계 취소 (Void)
```
조건: Authorize 완료, Capture 미실행
실행자: 오퍼레이터
결과: 에스크로 전체 잔여 금액 → 구매자 즉시 반환
수수료: 없음
트랜잭션 수: 1
```

#### 시나리오 B: 만료 후 회수 (Reclaim)
```
조건: authorizationExpiry 경과, Capture 미실행
실행자: 구매자 (직접)
결과: 에스크로 전체 금액 → 구매자
용도: 오퍼레이터/머천트 응답 없음 시 안전장치
```

#### 시나리오 C: 캡처 후 환불 (Refund)
```
조건: Capture 완료 후
실행자: 오퍼레이터 또는 머천트
자금 소스: OperatorRefundCollector (유연한 소스)
  - 머천트 잔고에서
  - 오퍼레이터 잔고에서
  - 별도 지정 주소에서
기한: refundExpiry 이내
부분 환불: 지원
```

### 10.2 환불 기술적 특징

| 특징 | 1세대 (Transfers.sol) | 2세대 (AuthCaptureEscrow) |
|------|----------------------|--------------------------|
| **Void** | 미지원 (즉시 정산) | 지원 (에스크로 반환) |
| **Reclaim** | 미지원 | 지원 (만료 후 안전장치) |
| **Post-capture 환불** | 프로토콜 외부 처리 | OperatorRefundCollector 모듈 |
| **부분 환불** | 미지원 | 지원 |
| **환불 토큰** | N/A | 원래 결제 토큰과 동일 |
| **수수료 환불** | N/A | 별도 정책 (오퍼레이터 재량) |

---

## 11. 파트너십 및 생태계

### 11.1 핵심 파트너

| 파트너 | 관계 | 통합 내용 |
|--------|------|-----------|
| **Shopify** | 전략적 파트너 | Commerce Payments Protocol 네이티브 통합, Shopify 체크아웃에서 암호화폐 결제 |
| **Stripe** | 생태계 파트너 | x402 프로토콜 기반 AI 에이전트 결제 지원 (Base + USDC) |
| **Cloudflare** | 기술 파트너 | x402 프로토콜 공동 개발 |
| **Circle** | 인프라 파트너 | USDC 공동 발행, Revenue Share |
| **Uniswap** | 기술 의존 | Permit2 + Universal Router 통합 (토큰 스왑) |

### 11.2 생태계 통합 현황

| 통합 유형 | 현황 |
|-----------|------|
| **이커머스** | Shopify 네이티브 플러그인 |
| **결제** | Stripe x402, Coinbase Business |
| **지갑** | Coinbase Wallet, Coinbase Smart Wallet, 범용 EOA |
| **DEX** | Uniswap V3 (자동 토큰 스왑) |
| **체인** | Base (주력), Ethereum, Polygon |
| **AI 에이전트** | x402를 통한 pay-per-request (예: CoinGecko $0.01/건) |

### 11.3 Coinbase Commerce -> Coinbase Business 전환 (2026.03)

중요한 비즈니스 전환이 2026년 3월 31일에 발생했다:

| 항목 | Coinbase Commerce (이전) | Coinbase Business (현재) |
|------|-------------------------|-------------------------|
| **커스터디 모델** | 비수탁 (Non-custodial) | 수탁 (Custodial) |
| **지역** | 글로벌 | 미국/싱가포르 법인만 |
| **법정화폐 전환** | 간접 (Coinbase 경유) | 직접 (Fiat off-ramp 내장) |
| **회계 통합** | 없음 | QuickBooks, Xero 연동 |
| **기반 기술** | Commerce Payments Protocol | Commerce Payments Protocol + 추가 레이어 |

출처: [Coinbase Help: Transitioning to Coinbase Business](https://help.coinbase.com/en/transitioning-from-coinbase-commerce-to-coinbase-business), [MoonPay Migration Guide](https://www.moonpay.com/newsroom/coinbase-commerce-shutdown-guide-for-merchants)

---

## 12. 확장성 평가

### 12.1 확장 강점

| 요인 | 평가 |
|------|------|
| **네트워크 효과** | Coinbase 6,000만+ 사용자 기반, Stripe/Shopify 파트너십으로 강력한 분배 채널 확보 |
| **기술적 확장성** | Base L2의 높은 처리량 + 저비용, 프로토콜 비업그레이드 설계로 안정성 확보 |
| **표준화 전략** | 오픈소스 + 퍼미션리스로 "안드로이드 전략" -- 생태계가 커질수록 Coinbase 이익 |
| **수익 다층화** | 단일 수수료 의존이 아닌 시퀀서비/USDC Revenue Share/커스터디 수수료 포트폴리오 |
| **AI 에이전트 시장** | x402로 M2M(Machine-to-Machine) 결제 시장 선점, 연간화 $600M 거래량 |

### 12.2 확장 병목 및 리스크

| 요인 | 평가 |
|------|------|
| **지역 제한** | Coinbase Business가 미국/싱가포르 법인만 지원 -- 글로벌 확장 제약 |
| **법정화폐 마찰** | 직접 은행 정산이 제한적 (BitPay/Stripe 대비 열위) |
| **토큰 제한** | x402의 98.7%가 USDC -- EIP-3009 지원 토큰 다양성 부족 |
| **구매자 보호** | 차지백 메커니즘 부재로 소비자 신뢰 구축 과제 |
| **컨트랙트 불변성** | 비업그레이드 설계는 보안 장점이지만, 버그 발견 시 수정 불가 (새 배포 필요) |
| **경쟁 심화** | Stripe(1.5%), PayPal의 암호화폐 결제 진출로 시장 파편화 |

### 12.3 2026년 전략 방향

Coinbase CEO Brian Armstrong이 발표한 2026년 전략 3대 축:

1. **Everything Exchange**: 글로벌 올인원 거래소 확장
2. **Stablecoins & Payments**: USDC 결제 확대, 프라이버시 기능, 스테이블코인 기반 거래 수수료
3. **Onchain Growth**: Base 개발자 생태계, 토큰화 시장 확대

Base 네트워크는 특히 **토큰화 시장(tokenized markets)**, **스테이블코인 결제**, **개발자 도구**에 집중한다.

출처: [CoinDesk: Base 2026 Strategy](https://www.coindesk.com/tech/2026/03/31/coinbase-s-base-to-focus-on-tokenized-markets-stablecoins-developers-this-year/), [Decrypt: Coinbase 2026 Strategy](https://decrypt.co/353503/coinbase-targeting-stablecoin-growth-onchain-adoption-in-2026-brian-armstrong)

---

## 13. 종합 기술-비즈니스 평가

### 13.1 기술적 성숙도

| 영역 | 성숙도 | 근거 |
|------|--------|------|
| **즉시 결제 (1세대)** | 높음 | Transfers.sol 프로덕션 운영 중, 3개 체인 배포, 814줄 Solidity |
| **Auth+Capture (2세대)** | 중간-높음 | AuthCaptureEscrow 배포 완료, 5개 Token Collector 구현 |
| **x402 프로토콜** | 중간 | 1.19억 건 처리, 3가지 전송 방식 지원, 그러나 USDC 편중 |
| **Shopify 통합** | 높음 | 네이티브 플러그인 운영 중 |
| **법정화폐 정산** | 낮음 | 직접 은행 정산 미지원, Coinbase 경유 필요 |

### 13.2 비즈니스 지속가능성 평가

**강점**:
- 다층적 수익 구조 (시퀀서비 + USDC Revenue Share + Commerce 수수료)로 단일 수익원 리스크 분산
- Coinbase 모회사의 강력한 재무 기반 (2025년 연매출 수십억 달러)
- 오픈소스 표준화 전략으로 락인(lock-in) 없이 생태계 확장 추구
- 규제 친화적 포지션 (미국 상장사, MSB 라이선스, GENIUS Act 준수 가능)

**약점**:
- Commerce 단독 수익은 1% 수수료로 마진 박함 -- Base 시퀀서비/USDC Revenue Share와 번들로 봐야 의미 있음
- 글로벌 확장이 규제에 의해 제한됨 (미국/싱가포르 외 Coinbase Business 미지원)
- 구매자 보호 메커니즘 부재로 메인스트림 채택에 장벽

### 13.3 핵심 모니터링 지표

| 지표 | 현재 수치 | 의미 |
|------|-----------|------|
| Base 시퀀서 순수익 | ~$15M/분기 (Q4 2025) | 네트워크 활성도 및 직접 수익 |
| USDC on Base 유통량 | 추적 필요 | Revenue Share 수익 잠재력 |
| x402 누적 트랜잭션 | 1.19억 건 (Base) | AI 에이전트 결제 시장 선점도 |
| x402 연간화 거래량 | ~$600M | 프로토콜 규모 |
| Coinbase Business 머천트 수 | 8,000+ (레거시 기준) | 머천트 채택률 |
| 스테이블코인 분기 수익 | $332.5M (Q2 2025) | USDC 생태계 수익 |

---

*본 보고서는 2026년 4월 14일 기준 공개된 정보를 바탕으로 작성되었습니다. GitHub 소스 코드(coinbase/commerce-onchain-payment-protocol, base/commerce-payments, coinbase/x402), Coinbase 공식 문서, 기술 블로그, 실적 보고서를 교차 검증하여 작성하였으며, 각 정보의 신뢰도를 "확인됨/추정/불명확"으로 표시하였습니다.*
