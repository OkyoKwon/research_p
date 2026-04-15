# 프론트엔드 개발 산출물 - 크립토 결제 서비스 플로우 시각화

- **작성 일시**: 2026-04-15
- **기반 문서**: 01_scenario-analyst_output.md, 02_flow-designer_output.md
- **산출물**: crypto-payment-flows.html

---

## 1. 기술 스택 결정

### 선택: Mermaid.js (CDN) + Vanilla JS + CSS Custom Properties

**선택 이유**:
- 46개 시나리오의 플로우차트를 단일 HTML 파일에서 렌더링해야 하므로 외부 빌드 도구 없이 동작하는 솔루션이 필요
- Mermaid.js는 텍스트 기반 다이어그램 정의를 지원하여 대량의 플로우차트를 선언적으로 관리 가능
- CDN 로딩으로 단일 파일 제약 충족
- 다크/라이트 모드 전환 시 Mermaid 테마도 동적으로 변경 가능

**대안 검토 및 기각 사유**:
| 대안 | 기각 사유 |
|------|----------|
| React Flow | 빌드 도구 필요, 단일 HTML 파일 불가 |
| D3.js | 46개 다이어그램의 수동 SVG 레이아웃 작업량 과다 |
| ELK.js | 스윔레인 레이아웃 구현 복잡도 높음 |
| 순수 SVG | 유지보수성 극히 낮음 |

---

## 2. 아키텍처 설계

### 데이터 구조

시나리오 데이터를 JavaScript 객체 배열로 구조화하여 관리한다. 각 시나리오 객체는 다음 필드를 포함:

```
{
  id: string,           // 시나리오 고유 식별자
  service: string,      // 서비스 ID (basePay, binancePay, coinbaseCommerce, stripeCrypto)
  category: string,     // 카테고리 (결제, 정산, 환불)
  title: string,        // 시나리오 한글 제목
  annotations: string[],// 수수료, 시간, 특이사항 등 주석 목록
  mermaid: string       // Mermaid.js 그래프 정의 문자열
}
```

### 렌더링 전략

1. **지연 렌더링 (Lazy Rendering)**: Mermaid 다이어그램은 사용자가 시나리오 카드를 펼칠 때만 렌더링한다. 46개를 동시에 렌더링하면 성능 저하가 심각하다.
2. **탭 기반 필터링**: 메인 탭(서비스) + 서브 탭(결제/정산/환불)으로 시나리오를 필터링하여 DOM 노드 최소화
3. **다크모드 전환 시 재초기화**: Mermaid 인스턴스를 테마에 맞게 재초기화하고 콘텐츠를 리렌더링

### CSS 설계

- CSS Custom Properties(변수)를 활용한 테마 시스템
- `[data-theme="dark"]` 셀렉터로 다크모드 변수 오버라이드
- 서비스별 브랜드 색상을 `--service-color`로 동적 적용

---

## 3. 구현된 시나리오 목록 (46개)

### Base Pay (11개)
| 카테고리 | 시나리오 |
|---------|---------|
| 결제 (3) | 즉시결제(Charge), 인가-캡처(Auth-Capture), x402 머신결제 |
| 정산 (3) | 온체인 즉시, 에스크로, 법정화폐 간접 |
| 환불 (5) | Void, Refund, Reclaim, Charge후 환불, 분쟁 |

### Binance Pay (12개)
| 카테고리 | 시나리오 |
|---------|---------|
| 결제 (6) | P2P, Hosted Checkout, C2B API, Payment Links, QR코드, Batch Payout |
| 정산 (2) | 오프체인 즉시, 법정화폐 간접 |
| 환불 (4) | 전액, 부분, 통화처리, 분쟁 |

### Coinbase Commerce (12개)
| 카테고리 | 시나리오 |
|---------|---------|
| 결제 (3) | Charge, Auth-Capture, Shopify 통합 |
| 정산 (3) | Self-Managed, Coinbase-Managed, Protocol 하이브리드 |
| 환불 (6) | Self-Managed, Coinbase-Managed, Void, Refund, Reclaim, 분쟁 |

### Stripe Crypto (11개)
| 카테고리 | 시나리오 |
|---------|---------|
| 결제 (6) | Stablecoin Payments, 구독결제, Pay with Crypto, x402, MPP, Crypto Onramp |
| 정산 (2) | USD 자동정산, USDC 직접수취 |
| 환불 (3) | Stablecoin 환불, Pay with Crypto 환불, 분쟁 |

---

## 4. UI/UX 구현 사항

### 탭 네비게이션
- **메인 탭**: 5개 (Base Pay, Binance Pay, Coinbase Commerce, Stripe Crypto, 서비스 비교)
- **서브 탭**: 서비스 탭 내 3개 (결제, 정산, 환불), 비교 탭 내 3개 (결제 비교, 정산 비교, 환불 비교)
- 서비스별 브랜드 색상이 탭 하단 인디케이터에 적용

### 시나리오 카드
- 접이식(accordion) 카드 형태로 구성
- 서비스 배지 + 시나리오 제목 표시
- 클릭 시 Mermaid 다이어그램 + 주석(annotations) 표시
- 주석은 칩(chip) 형태로 시각적 강조

### 서비스 비교 탭
- **서비스 개요 비교**: 4열 그리드 카드로 핵심 지표 비교
- **기능 매트릭스**: O/X 표로 시나리오별 지원 여부 비교
- **정산/환불 비교 테이블**: 항목별 상세 비교 (하이라이트, 경고 표시)
- **강점/약점 요약**: 4열 그리드로 서비스별 강점/약점 나열

### 다크/라이트 모드
- 헤더의 토글 버튼으로 전환
- CSS Custom Properties 기반 즉시 전환
- Mermaid 다이어그램도 테마에 맞춰 재렌더링

### 반응형
- 데스크톱: 4열 그리드, 전체 테이블
- 태블릿 (1024px 이하): 2열 그리드
- 모바일 (768px 이하): 1열 스택, 축소된 테이블

### 인쇄
- 인쇄 버튼 클릭 시 `window.print()` 호출
- `@media print`에서 네비게이션 숨기고 모든 탭/시나리오 표시

---

## 5. 성능 최적화

1. **Lazy Mermaid Rendering**: 시나리오 카드 펼침 시에만 다이어그램 렌더링
2. **DOM 최소화**: 현재 활성 탭의 시나리오만 DOM에 삽입
3. **CSS 전환**: `transition` 속성으로 부드러운 테마 전환
4. **CDN 캐싱**: Mermaid.js CDN 로딩으로 브라우저 캐시 활용

---

## 6. 제약 사항 및 향후 개선

### 현재 제약
- Mermaid.js의 스윔레인 지원 한계로 액터별 구분이 노드 레이블로 표현됨 (완전한 스윔레인 구분은 미구현)
- 원본 flow-designer 데이터의 노드 타입별 색상 코딩이 Mermaid 기본 테마에 의존
- 비교 탭의 차트/그래프 시각화는 테이블 형태로 대체

### 향후 개선 가능 사항
- ELK.js 또는 React Flow 기반 스윔레인 다이어그램으로 업그레이드
- 시나리오 검색 기능 추가
- 시나리오 간 크로스 레퍼런스 링크
- PDF 내보내기 기능
- 수수료 시뮬레이터 (금액 입력 시 서비스별 수수료 비교)
