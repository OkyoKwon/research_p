# 크립토 결제 서비스 플로우차트 & 다이어그램 데이터 설계서

4개 크립토 결제 서비스의 결제/정산/환불 시나리오에 대한 플로우차트 데이터 구조를 정의한다. 프론트엔드 개발자가 HTML/SVG 다이어그램을 직접 렌더링할 수 있도록 JSON 형식의 노드/엣지 데이터와 스윔레인 정의를 포함한다.

- **작성 일시**: 2026-04-15
- **기반 문서**: 01_scenario-analyst_output.md
- **출력 대상**: HTML/SVG 기반 인터랙티브 다이어그램

---

## 디자인 시스템 (Design Tokens)

### 서비스별 색상 코드

```json
{
  "serviceColors": {
    "basePay": {
      "primary": "#0052FF",
      "light": "#E6EEFF",
      "dark": "#003ACC",
      "label": "Base Pay"
    },
    "binancePay": {
      "primary": "#F0B90B",
      "light": "#FFF8E1",
      "dark": "#C49800",
      "label": "Binance Pay"
    },
    "coinbaseCommerce": {
      "primary": "#0052FF",
      "light": "#E8F0FE",
      "dark": "#0040CC",
      "label": "Coinbase Commerce"
    },
    "stripeCrypto": {
      "primary": "#635BFF",
      "light": "#F0EFFF",
      "dark": "#4B44CC",
      "label": "Stripe Crypto"
    }
  }
}
```

### 액터(스윔레인) 색상

```json
{
  "actorColors": {
    "buyer": { "bg": "#E3F2FD", "border": "#1565C0", "icon": "person", "label": "구매자/소비자" },
    "merchant": { "bg": "#E8F5E9", "border": "#2E7D32", "icon": "store", "label": "가맹점/머천트" },
    "platform": { "bg": "#FFF3E0", "border": "#E65100", "icon": "cloud", "label": "플랫폼/시스템" },
    "blockchain": { "bg": "#F3E5F5", "border": "#6A1B9A", "icon": "link", "label": "블록체인/스마트컨트랙트" },
    "bank": { "bg": "#ECEFF1", "border": "#37474F", "icon": "account_balance", "label": "은행/법정화폐" }
  }
}
```

### 노드 타입별 스타일

```json
{
  "nodeStyles": {
    "start":      { "shape": "circle",       "fill": "#4CAF50", "stroke": "#2E7D32", "textColor": "#FFFFFF", "radius": 24 },
    "end":        { "shape": "circle",       "fill": "#F44336", "stroke": "#C62828", "textColor": "#FFFFFF", "radius": 24 },
    "action":     { "shape": "roundedRect",  "fill": "#FFFFFF", "stroke": "#90A4AE", "textColor": "#212121", "rx": 8, "minWidth": 160, "minHeight": 48 },
    "decision":   { "shape": "diamond",      "fill": "#FFF9C4", "stroke": "#F9A825", "textColor": "#212121", "size": 80 },
    "payment":    { "shape": "roundedRect",  "fill": "#E3F2FD", "stroke": "#1565C0", "textColor": "#0D47A1", "rx": 8, "minWidth": 160, "minHeight": 48, "icon": "payment" },
    "settlement": { "shape": "roundedRect",  "fill": "#E8F5E9", "stroke": "#2E7D32", "textColor": "#1B5E20", "rx": 8, "minWidth": 160, "minHeight": 48, "icon": "account_balance_wallet" },
    "refund":     { "shape": "roundedRect",  "fill": "#FBE9E7", "stroke": "#D84315", "textColor": "#BF360C", "rx": 8, "minWidth": 160, "minHeight": 48, "icon": "undo" },
    "error":      { "shape": "roundedRect",  "fill": "#FFEBEE", "stroke": "#C62828", "textColor": "#B71C1C", "rx": 8, "minWidth": 160, "minHeight": 48, "icon": "error" },
    "annotation":  { "shape": "note",        "fill": "#FFFDE7", "stroke": "#FBC02D", "textColor": "#F57F17", "rx": 4 }
  }
}
```

### 엣지 스타일

```json
{
  "edgeStyles": {
    "normal":     { "stroke": "#616161", "strokeWidth": 1.5, "markerEnd": "arrowClosed" },
    "conditional":{ "stroke": "#F9A825", "strokeWidth": 1.5, "markerEnd": "arrowClosed", "dashArray": "5,3" },
    "error":      { "stroke": "#C62828", "strokeWidth": 1.5, "markerEnd": "arrowClosed", "dashArray": "3,3" },
    "timing":     { "stroke": "#7E57C2", "strokeWidth": 1, "markerEnd": "arrowOpen", "dashArray": "8,4" }
  }
}
```

---

## 페이지 레이아웃 구조

```json
{
  "layout": {
    "type": "tabbed",
    "tabs": [
      { "id": "basePay",          "label": "Base Pay",          "color": "#0052FF", "subTabs": ["결제", "정산", "환불"] },
      { "id": "binancePay",       "label": "Binance Pay",       "color": "#F0B90B", "subTabs": ["결제", "정산", "환불"] },
      { "id": "coinbaseCommerce", "label": "Coinbase Commerce", "color": "#0052FF", "subTabs": ["결제", "정산", "환불"] },
      { "id": "stripeCrypto",     "label": "Stripe Crypto",     "color": "#635BFF", "subTabs": ["결제", "정산", "환불"] },
      { "id": "comparison",       "label": "서비스 비교",         "color": "#455A64", "subTabs": ["결제 비교", "정산 비교", "환불 비교"] }
    ],
    "diagramContainer": {
      "maxWidth": 1200,
      "padding": 32,
      "swimlaneGap": 16,
      "nodeSpacingX": 200,
      "nodeSpacingY": 80
    }
  }
}
```

---

---

# Tab 1: Base Pay

서비스 컬러: `#0052FF`

---

## 1.1 결제 (Payment) 시나리오

---

### 1.1.1 즉시 결제 (Charge / Direct Transfer)

**스윔레인 정의**

```json
{
  "id": "bp-pay-charge",
  "title": "Base Pay - 즉시 결제 (Charge)",
  "serviceColor": "#0052FF",
  "category": "결제",
  "lanes": [
    { "id": "buyer",      "actor": "buyer",      "label": "구매자" },
    { "id": "merchant",   "actor": "merchant",   "label": "머천트" },
    { "id": "operator",   "actor": "platform",   "label": "오퍼레이터 (Coinbase)" },
    { "id": "contract",   "actor": "blockchain", "label": "스마트 컨트랙트 (Transfers.sol)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",    "label": "결제 시작",                     "lane": "merchant" },
    { "id": "n2",  "type": "action",   "label": "결제 요청 생성\n(API / Shopify 플러그인)", "lane": "merchant" },
    { "id": "n3",  "type": "action",   "label": "TransferIntent 생성\n(금액, 머천트주소, 만료, 수수료)", "lane": "operator" },
    { "id": "n4",  "type": "action",   "label": "지갑 연결 + 결제 승인",         "lane": "buyer" },
    { "id": "n5",  "type": "decision", "label": "결제 토큰 =\n정산 토큰?",       "lane": "contract" },
    { "id": "n6",  "type": "action",   "label": "Uniswap V3 자동 스왑\n(Permit2/EIP-3009)", "lane": "contract" },
    { "id": "n7",  "type": "payment",  "label": "토큰 전송 실행\n(원자적 처리)",  "lane": "contract" },
    { "id": "n8",  "type": "settlement","label": "머천트 지갑 정산\n+ 오퍼레이터 수수료 차감", "lane": "contract" },
    { "id": "n9",  "type": "action",   "label": "Transferred 이벤트 발행\n(온체인 기록)", "lane": "contract" },
    { "id": "n10", "type": "end",      "label": "결제 완료",                     "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "normal" },
    { "id": "e3",  "source": "n3",  "target": "n4",  "style": "normal" },
    { "id": "e4",  "source": "n4",  "target": "n5",  "style": "normal" },
    { "id": "e5",  "source": "n5",  "target": "n6",  "style": "conditional", "label": "아니오 (토큰 불일치)" },
    { "id": "e6",  "source": "n5",  "target": "n7",  "style": "conditional", "label": "예 (동일 토큰)" },
    { "id": "e7",  "source": "n6",  "target": "n7",  "style": "normal" },
    { "id": "e8",  "source": "n7",  "target": "n8",  "style": "normal" },
    { "id": "e9",  "source": "n8",  "target": "n9",  "style": "normal" },
    { "id": "e10", "source": "n9",  "target": "n10", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n7",  "text": "수수료: 1% (머천트 부담)", "position": "right" },
    { "attachTo": "n6",  "text": "DEX 슬리피지: 변동 (구매자 부담)", "position": "right" },
    { "attachTo": "e4",  "text": "가스비: ~$0.01 (Base)", "position": "above" },
    { "attachTo": "n10", "text": "전체 소요: ~2초 (Base)", "position": "right" }
  ]
}
```

---

### 1.1.2 인가-캡처 결제 (Authorize-Capture)

**스윔레인 정의**

```json
{
  "id": "bp-pay-authcapture",
  "title": "Base Pay - 인가-캡처 결제 (Authorize-Capture)",
  "serviceColor": "#0052FF",
  "category": "결제",
  "lanes": [
    { "id": "buyer",    "actor": "buyer",      "label": "구매자" },
    { "id": "merchant", "actor": "merchant",   "label": "머천트" },
    { "id": "operator", "actor": "platform",   "label": "오퍼레이터 (Coinbase/Shopify)" },
    { "id": "escrow",   "actor": "blockchain", "label": "AuthCaptureEscrow / Token Store" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",     "label": "결제 시작",                          "lane": "merchant" },
    { "id": "n2",  "type": "action",    "label": "PaymentInfo 생성\n(maxAmount, authExpiry,\nrefundExpiry, feeBps)", "lane": "operator" },
    { "id": "n3",  "type": "action",    "label": "결제 승인 (지갑 서명)",               "lane": "buyer" },
    { "id": "n4",  "type": "payment",   "label": "AUTHORIZE\n구매자 자금 → 에스크로 예치", "lane": "escrow" },
    { "id": "n5",  "type": "action",    "label": "authorizationExpiry\n타이머 시작",     "lane": "escrow" },
    { "id": "n6",  "type": "action",    "label": "주문 확인 / 재고 확인\n/ 배송 준비",    "lane": "merchant" },
    { "id": "n7",  "type": "decision",  "label": "캡처 진행?",                         "lane": "operator" },
    { "id": "n8",  "type": "settlement","label": "CAPTURE\n에스크로 → 머천트 전송\n(부분 캡처 가능)", "lane": "escrow" },
    { "id": "n9",  "type": "refund",    "label": "VOID\n에스크로 → 구매자 전액 반환",    "lane": "escrow" },
    { "id": "n10", "type": "action",    "label": "미캡처 잔여분\n구매자 자동 반환 / reclaim()", "lane": "escrow" },
    { "id": "n11", "type": "end",       "label": "결제 완료",                          "lane": "merchant" },
    { "id": "n12", "type": "end",       "label": "취소 완료",                          "lane": "buyer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "normal" },
    { "id": "e3",  "source": "n3",  "target": "n4",  "style": "normal" },
    { "id": "e4",  "source": "n4",  "target": "n5",  "style": "normal" },
    { "id": "e5",  "source": "n5",  "target": "n6",  "style": "normal",      "label": "대기 기간" },
    { "id": "e6",  "source": "n6",  "target": "n7",  "style": "normal" },
    { "id": "e7",  "source": "n7",  "target": "n8",  "style": "conditional", "label": "캡처 실행" },
    { "id": "e8",  "source": "n7",  "target": "n9",  "style": "conditional", "label": "Void (취소)" },
    { "id": "e9",  "source": "n8",  "target": "n10", "style": "normal",      "label": "잔여분 처리" },
    { "id": "e10", "source": "n8",  "target": "n11", "style": "normal" },
    { "id": "e11", "source": "n9",  "target": "n12", "style": "normal" },
    { "id": "e12", "source": "n10", "target": "n11", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4",  "text": "가스비: ~$0.01 (Authorize)", "position": "right" },
    { "attachTo": "n8",  "text": "수수료: 1% (Capture 시 차감)\n가스비: ~$0.01", "position": "right" },
    { "attachTo": "n9",  "text": "수수료: 없음\nVoid 시 수수료 미발생", "position": "right" },
    { "attachTo": "n5",  "text": "authExpiry 이전에만\nCapture 가능", "position": "left" },
    { "attachTo": "n8",  "text": "부분 캡처 지원\n(총 캡처 <= maxAmount)", "position": "bottom" }
  ]
}
```

---

### 1.1.3 x402 머신 결제

**스윔레인 정의**

```json
{
  "id": "bp-pay-x402",
  "title": "Base Pay - x402 머신/AI 에이전트 결제",
  "serviceColor": "#0052FF",
  "category": "결제",
  "lanes": [
    { "id": "client",      "actor": "buyer",      "label": "클라이언트 (AI 에이전트)" },
    { "id": "server",      "actor": "merchant",   "label": "서버 (API 제공자)" },
    { "id": "facilitator", "actor": "platform",   "label": "Facilitator (Stripe)" },
    { "id": "chain",       "actor": "blockchain", "label": "블록체인 (Base/Solana)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",    "label": "리소스 요청",                         "lane": "client" },
    { "id": "n2",  "type": "action",   "label": "HTTP GET\n유료 리소스 요청",            "lane": "client" },
    { "id": "n3",  "type": "action",   "label": "HTTP 402 응답\n+ Invoice 반환\n(금액, 수신주소, 유효기간, 스킴)", "lane": "server" },
    { "id": "n4",  "type": "decision", "label": "결제 스킴?",                          "lane": "client" },
    { "id": "n5",  "type": "payment",  "label": "USDC 결제 서명 생성\n(EIP-3009/Permit2/ERC-7710)", "lane": "client" },
    { "id": "n6",  "type": "action",   "label": "PAYMENT-SIGNATURE\nHTTP 헤더에 서명 포함\n재요청", "lane": "client" },
    { "id": "n7",  "type": "action",   "label": "결제 검증\n(서명 복원, 잔고 확인,\n금액 일치, 시뮬레이션)", "lane": "facilitator" },
    { "id": "n8",  "type": "decision", "label": "검증 성공?",                          "lane": "facilitator" },
    { "id": "n9",  "type": "settlement","label": "온체인 정산\ntransferWithAuthorization()", "lane": "chain" },
    { "id": "n10", "type": "action",   "label": "HTTP 200\n리소스 제공",                "lane": "server" },
    { "id": "n11", "type": "error",    "label": "HTTP 402\n결제 실패 반환",              "lane": "server" },
    { "id": "n12", "type": "end",      "label": "완료",                                "lane": "client" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "normal" },
    { "id": "e3",  "source": "n3",  "target": "n4",  "style": "normal" },
    { "id": "e4",  "source": "n4",  "target": "n5",  "style": "conditional", "label": "exact (고정금액) /\nupto (사용량 기반)" },
    { "id": "e5",  "source": "n5",  "target": "n6",  "style": "normal" },
    { "id": "e6",  "source": "n6",  "target": "n7",  "style": "normal" },
    { "id": "e7",  "source": "n7",  "target": "n8",  "style": "normal" },
    { "id": "e8",  "source": "n8",  "target": "n9",  "style": "conditional", "label": "성공" },
    { "id": "e9",  "source": "n8",  "target": "n11", "style": "error",       "label": "실패" },
    { "id": "e10", "source": "n9",  "target": "n10", "style": "normal" },
    { "id": "e11", "source": "n10", "target": "n12", "style": "normal" },
    { "id": "e12", "source": "n11", "target": "n12", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5",  "text": "USDC 점유율 98.7%", "position": "right" },
    { "attachTo": "n7",  "text": "Stripe x402 수수료: 0%\n(월 1,000건 무료)", "position": "right" },
    { "attachTo": "n9",  "text": "가스비: ~$0.01 (Base)\n소요시간: ~2초", "position": "right" },
    { "attachTo": "n3",  "text": "x402 Foundation:\nGoogle, AWS, Visa,\nCircle, Anthropic", "position": "left" }
  ]
}
```

---

## 1.2 정산 (Settlement) 시나리오

---

### 1.2.1 온체인 즉시 정산 (Charge)

**스윔레인 정의**

```json
{
  "id": "bp-set-charge",
  "title": "Base Pay - 온체인 즉시 정산",
  "serviceColor": "#0052FF",
  "category": "정산",
  "lanes": [
    { "id": "buyer",    "actor": "buyer",      "label": "구매자" },
    { "id": "contract", "actor": "blockchain", "label": "스마트 컨트랙트" },
    { "id": "dex",      "actor": "blockchain", "label": "Uniswap V3 DEX" },
    { "id": "merchant", "actor": "merchant",   "label": "머천트 지갑" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "결제 실행",              "lane": "buyer" },
    { "id": "n2", "type": "decision",   "label": "결제 토큰 =\n정산 토큰?", "lane": "contract" },
    { "id": "n3", "type": "action",     "label": "자동 스왑\n(결제토큰 → 정산토큰)", "lane": "dex" },
    { "id": "n4", "type": "settlement", "label": "원자적 토큰 전송\n머천트 지갑 입금",  "lane": "contract" },
    { "id": "n5", "type": "action",     "label": "오퍼레이터 수수료 차감\n(1%)", "lane": "contract" },
    { "id": "n6", "type": "end",        "label": "정산 완료",              "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "conditional", "label": "아니오" },
    { "id": "e3", "source": "n2", "target": "n4", "style": "conditional", "label": "예" },
    { "id": "e4", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e5", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e6", "source": "n5", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "정산 속도: ~2초 (Base)", "position": "right" },
    { "attachTo": "n5", "text": "정산 수수료: 1% (결제 수수료에 포함)", "position": "right" },
    { "attachTo": "n6", "text": "정산 통화: USDC(기본), ETH 등", "position": "bottom" }
  ]
}
```

---

### 1.2.2 에스크로 정산 (Authorize-Capture)

**스윔레인 정의**

```json
{
  "id": "bp-set-escrow",
  "title": "Base Pay - 에스크로 캡처 후 정산",
  "serviceColor": "#0052FF",
  "category": "정산",
  "lanes": [
    { "id": "operator", "actor": "platform",   "label": "오퍼레이터" },
    { "id": "escrow",   "actor": "blockchain", "label": "Token Store (에스크로)" },
    { "id": "merchant", "actor": "merchant",   "label": "머천트" },
    { "id": "buyer",    "actor": "buyer",      "label": "구매자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "Authorize 완료",                "lane": "escrow" },
    { "id": "n2", "type": "action",     "label": "자금 Token Store에 보관",         "lane": "escrow" },
    { "id": "n3", "type": "action",     "label": "머천트 확인 후\nCapture 요청",     "lane": "operator" },
    { "id": "n4", "type": "decision",   "label": "전액 캡처?\n부분 캡처?",           "lane": "operator" },
    { "id": "n5", "type": "settlement", "label": "전액 캡처\n에스크로 → 머천트 전송", "lane": "escrow" },
    { "id": "n6", "type": "settlement", "label": "부분 캡처\n일부 → 머천트 전송",    "lane": "escrow" },
    { "id": "n7", "type": "refund",     "label": "잔여분 구매자 반환\n(reclaim 가능)", "lane": "escrow" },
    { "id": "n8", "type": "end",        "label": "정산 완료",                      "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "conditional", "label": "전액" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "conditional", "label": "부분" },
    { "id": "e6", "source": "n5", "target": "n8", "style": "normal" },
    { "id": "e7", "source": "n6", "target": "n7", "style": "normal" },
    { "id": "e8", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n3", "text": "authExpiry 이전에만 가능", "position": "right" },
    { "attachTo": "n5", "text": "Capture 시 즉시 정산", "position": "right" },
    { "attachTo": "n7", "text": "미캡처분은 reclaim()으로 회수", "position": "right" }
  ]
}
```

---

### 1.2.3 법정화폐 정산 (간접 경로)

**스윔레인 정의**

```json
{
  "id": "bp-set-fiat",
  "title": "Base Pay - 법정화폐 전환 정산",
  "serviceColor": "#0052FF",
  "category": "정산",
  "lanes": [
    { "id": "merchant",  "actor": "merchant",   "label": "머천트" },
    { "id": "coinbase",  "actor": "platform",   "label": "Coinbase Business/Exchange" },
    { "id": "bank",      "actor": "bank",       "label": "은행" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",      "label": "USDC 수령 완료",                   "lane": "merchant" },
    { "id": "n2",  "type": "decision",   "label": "정산 경로 선택?",                   "lane": "merchant" },
    { "id": "n3",  "type": "action",     "label": "Coinbase Business 경유\n(미국/싱가포르 법인)", "lane": "coinbase" },
    { "id": "n4",  "type": "action",     "label": "Coinbase 거래소 경유\n(글로벌)",      "lane": "coinbase" },
    { "id": "n5",  "type": "action",     "label": "Shopify 통합 경유\n(Stripe 인프라)", "lane": "coinbase" },
    { "id": "n6",  "type": "action",     "label": "USDC → fiat off-ramp",            "lane": "coinbase" },
    { "id": "n7",  "type": "action",     "label": "USDC → USD 전환",                  "lane": "coinbase" },
    { "id": "n8",  "type": "action",     "label": "현지 통화 정산",                    "lane": "coinbase" },
    { "id": "n9",  "type": "settlement", "label": "은행 출금",                         "lane": "bank" },
    { "id": "n10", "type": "end",        "label": "법정화폐 정산 완료",                 "lane": "bank" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "conditional", "label": "Coinbase Business" },
    { "id": "e3",  "source": "n2",  "target": "n4",  "style": "conditional", "label": "Coinbase Exchange" },
    { "id": "e4",  "source": "n2",  "target": "n5",  "style": "conditional", "label": "Shopify" },
    { "id": "e5",  "source": "n3",  "target": "n6",  "style": "normal" },
    { "id": "e6",  "source": "n4",  "target": "n7",  "style": "normal" },
    { "id": "e7",  "source": "n5",  "target": "n8",  "style": "normal" },
    { "id": "e8",  "source": "n6",  "target": "n9",  "style": "normal" },
    { "id": "e9",  "source": "n7",  "target": "n9",  "style": "normal" },
    { "id": "e10", "source": "n8",  "target": "n9",  "style": "normal" },
    { "id": "e11", "source": "n9",  "target": "n10", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n9",  "text": "추가 1-5 영업일 소요", "position": "right" },
    { "attachTo": "n5",  "text": "Shopify 정산 수수료: 0%", "position": "right" },
    { "attachTo": "n2",  "text": "법정화폐 직접 은행 정산 미지원\n(구조적 약점)", "position": "left" }
  ]
}
```

---

## 1.3 환불 (Refund) 시나리오

---

### 1.3.1 캡처 전 취소 (Void)

**스윔레인 정의**

```json
{
  "id": "bp-ref-void",
  "title": "Base Pay - 캡처 전 취소 (Void)",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "merchant", "actor": "merchant",   "label": "머천트" },
    { "id": "operator", "actor": "platform",   "label": "오퍼레이터" },
    { "id": "escrow",   "actor": "blockchain", "label": "AuthCaptureEscrow / Token Store" },
    { "id": "buyer",    "actor": "buyer",      "label": "구매자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "환불 사유 발생\n(재고 부족, 주문 취소)", "lane": "merchant" },
    { "id": "n2", "type": "action",  "label": "void() 함수 호출",                    "lane": "operator" },
    { "id": "n3", "type": "refund",  "label": "Token Store에서\n전체 승인 금액 반환",   "lane": "escrow" },
    { "id": "n4", "type": "action",  "label": "구매자 지갑 입금",                     "lane": "buyer" },
    { "id": "n5", "type": "action",  "label": "상태: Authorized → Voided",          "lane": "escrow" },
    { "id": "n6", "type": "end",     "label": "취소 완료",                           "lane": "buyer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n3", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "수수료: 없음 (Capture 미실행)", "position": "right" },
    { "attachTo": "n3", "text": "가스비: ~$0.01\n소요: ~2초 (Base)", "position": "right" },
    { "attachTo": "n3", "text": "결제당 1회만 실행 가능\n부분 Void 불가", "position": "left" }
  ]
}
```

---

### 1.3.2 캡처 후 환불 (Refund)

**스윔레인 정의**

```json
{
  "id": "bp-ref-postCapture",
  "title": "Base Pay - 캡처 후 환불",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "operator",  "actor": "platform",   "label": "오퍼레이터/머천트" },
    { "id": "collector", "actor": "blockchain", "label": "OperatorRefundCollector" },
    { "id": "escrow",    "actor": "blockchain", "label": "AuthCaptureEscrow" },
    { "id": "buyer",     "actor": "buyer",      "label": "구매자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "환불 사유 발생\n(반품, 불만족)",      "lane": "operator" },
    { "id": "n2", "type": "action",   "label": "refund() 함수 호출",               "lane": "operator" },
    { "id": "n3", "type": "action",   "label": "환불 자금 조달\n(머천트/오퍼레이터 잔고,\n별도 지정 주소)", "lane": "collector" },
    { "id": "n4", "type": "decision", "label": "전액?\n부분?",                     "lane": "collector" },
    { "id": "n5", "type": "refund",   "label": "전액 환불\n구매자에게 전송",          "lane": "collector" },
    { "id": "n6", "type": "refund",   "label": "부분 환불\n일부 금액 전송",           "lane": "collector" },
    { "id": "n7", "type": "action",   "label": "구매자 지갑 입금",                  "lane": "buyer" },
    { "id": "n8", "type": "end",      "label": "환불 완료",                        "lane": "buyer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "conditional", "label": "전액" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "conditional", "label": "부분" },
    { "id": "e6", "source": "n5", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n6", "target": "n7", "style": "normal" },
    { "id": "e8", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "가스비: ~$0.01\n소요: ~2초 (Base)", "position": "right" },
    { "attachTo": "n5", "text": "플랫폼 수수료(1%) 환불:\n오퍼레이터 재량", "position": "right" },
    { "attachTo": "n7", "text": "환불 토큰 = 원래 결제 토큰", "position": "right" },
    { "attachTo": "n2", "text": "refundExpiry 이후 환불 불가", "position": "left" }
  ]
}
```

---

### 1.3.3 인가 만료 후 소비자 회수 (Reclaim)

**스윔레인 정의**

```json
{
  "id": "bp-ref-reclaim",
  "title": "Base Pay - 소비자 직접 회수 (Reclaim)",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "buyer",  "actor": "buyer",      "label": "구매자" },
    { "id": "escrow", "actor": "blockchain", "label": "AuthCaptureEscrow / Token Store" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "Authorize 완료 상태",          "lane": "escrow" },
    { "id": "n2", "type": "action",  "label": "authorizationExpiry 경과\n(머천트 미캡처)", "lane": "escrow" },
    { "id": "n3", "type": "action",  "label": "구매자 직접\nreclaim() 호출",    "lane": "buyer" },
    { "id": "n4", "type": "refund",  "label": "전체 에스크로 금액\n구매자에게 반환", "lane": "escrow" },
    { "id": "n5", "type": "action",  "label": "상태: Authorized → Reclaimed", "lane": "escrow" },
    { "id": "n6", "type": "end",     "label": "회수 완료",                    "lane": "buyer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "timing", "label": "authExpiry 대기" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n3", "text": "가스비: ~$0.01", "position": "right" },
    { "attachTo": "n3", "text": "중앙 중재 기관 불필요\n온체인 안전장치", "position": "left" },
    { "attachTo": "n2", "text": "authExpiry는 PaymentInfo에\n사전 정의됨", "position": "right" }
  ]
}
```

---

### 1.3.4 즉시 결제(Charge) 후 환불

**스윔레인 정의**

```json
{
  "id": "bp-ref-charge",
  "title": "Base Pay - Charge 후 환불",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "merchant",  "actor": "merchant",   "label": "머천트" },
    { "id": "collector", "actor": "blockchain", "label": "OperatorRefundCollector (2세대)" },
    { "id": "buyer",     "actor": "buyer",      "label": "구매자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "Charge 완료\n(자금 머천트 전송됨)",     "lane": "merchant" },
    { "id": "n2", "type": "action",   "label": "환불 사유 발생",                      "lane": "merchant" },
    { "id": "n3", "type": "decision", "label": "프로토콜 버전?",                      "lane": "merchant" },
    { "id": "n4", "type": "action",   "label": "1세대 (Transfers.sol)\n머천트가 직접 온체인 전송", "lane": "merchant" },
    { "id": "n5", "type": "refund",   "label": "2세대 (AuthCaptureEscrow)\nrefund() 호출\n부분 환불 지원", "lane": "collector" },
    { "id": "n6", "type": "action",   "label": "구매자 지갑 입금",                    "lane": "buyer" },
    { "id": "n7", "type": "end",      "label": "환불 완료",                          "lane": "buyer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "conditional", "label": "1세대" },
    { "id": "e4", "source": "n3", "target": "n5", "style": "conditional", "label": "2세대" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e7", "source": "n6", "target": "n7", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "가스비: 머천트 부담\n자동화 미지원", "position": "right" },
    { "attachTo": "n5", "text": "가스비: ~$0.01\nrefundExpiry 이후 환불 불가", "position": "right" }
  ]
}
```

---

### 1.3.5 분쟁 해결

**스윔레인 정의**

```json
{
  "id": "bp-ref-dispute",
  "title": "Base Pay - 온체인 결제 분쟁 해결",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "buyer",    "actor": "buyer",      "label": "구매자" },
    { "id": "merchant", "actor": "merchant",   "label": "머천트" },
    { "id": "operator", "actor": "platform",   "label": "오퍼레이터 (Coinbase)" },
    { "id": "escrow",   "actor": "blockchain", "label": "스마트 컨트랙트" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",    "label": "분쟁 발생",                        "lane": "buyer" },
    { "id": "n2",  "type": "decision", "label": "캡처 전?\n캡처 후?",                "lane": "operator" },
    { "id": "n3",  "type": "decision", "label": "Void 가능?",                      "lane": "operator" },
    { "id": "n4",  "type": "refund",   "label": "Void 실행\n전액 반환",              "lane": "escrow" },
    { "id": "n5",  "type": "action",   "label": "authExpiry 경과 후\nReclaim 실행",  "lane": "buyer" },
    { "id": "n6",  "type": "decision", "label": "머천트 환불 동의?",                 "lane": "merchant" },
    { "id": "n7",  "type": "refund",   "label": "Refund 실행\n(OperatorRefundCollector)", "lane": "escrow" },
    { "id": "n8",  "type": "action",   "label": "Coinbase 정책적 중재\n(프로토콜 외부)", "lane": "operator" },
    { "id": "n9",  "type": "error",    "label": "강제 중재 불가\n(차지백 없음)",       "lane": "buyer" },
    { "id": "n10", "type": "end",      "label": "분쟁 종료",                        "lane": "operator" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "conditional", "label": "캡처 전" },
    { "id": "e3",  "source": "n2",  "target": "n6",  "style": "conditional", "label": "캡처 후" },
    { "id": "e4",  "source": "n3",  "target": "n4",  "style": "conditional", "label": "예" },
    { "id": "e5",  "source": "n3",  "target": "n5",  "style": "conditional", "label": "아니오 (만료 대기)" },
    { "id": "e6",  "source": "n4",  "target": "n10", "style": "normal" },
    { "id": "e7",  "source": "n5",  "target": "n10", "style": "normal" },
    { "id": "e8",  "source": "n6",  "target": "n7",  "style": "conditional", "label": "동의" },
    { "id": "e9",  "source": "n6",  "target": "n8",  "style": "conditional", "label": "거부" },
    { "id": "e10", "source": "n7",  "target": "n10", "style": "normal" },
    { "id": "e11", "source": "n8",  "target": "n9",  "style": "error" },
    { "id": "e12", "source": "n9",  "target": "n10", "style": "error" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n9", "text": "차지백 메커니즘 없음\n머천트에게 유리", "position": "right" },
    { "attachTo": "n5", "text": "에스크로가 부분적 보호 제공", "position": "left" },
    { "attachTo": "n8", "text": "프로토콜 외부 처리\n강제력 제한", "position": "right" }
  ]
}
```

---

---

# Tab 2: Binance Pay

서비스 컬러: `#F0B90B`

---

## 2.1 결제 (Payment) 시나리오

---

### 2.1.1 P2P 개인 간 결제

**스윔레인 정의**

```json
{
  "id": "bn-pay-p2p",
  "title": "Binance Pay - P2P 개인 간 결제",
  "serviceColor": "#F0B90B",
  "category": "결제",
  "lanes": [
    { "id": "sender",   "actor": "buyer",    "label": "송금자 (Binance 사용자)" },
    { "id": "binance",  "actor": "platform", "label": "Binance 내부 원장" },
    { "id": "receiver", "actor": "buyer",    "label": "수신자 (Binance 사용자)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "P2P 송금 시작",                     "lane": "sender" },
    { "id": "n2", "type": "action",     "label": "Binance 앱 > Pay 메뉴",             "lane": "sender" },
    { "id": "n3", "type": "action",     "label": "상대방 식별\n(Pay ID / 이메일 / 전화 / QR)", "lane": "sender" },
    { "id": "n4", "type": "action",     "label": "암호화폐 종류 선택\n(300종+ 지원)",     "lane": "sender" },
    { "id": "n5", "type": "action",     "label": "전송 금액 입력",                     "lane": "sender" },
    { "id": "n6", "type": "payment",    "label": "내부 원장 이체 처리",                 "lane": "binance" },
    { "id": "n7", "type": "settlement", "label": "Funding Wallet 즉시 입금",           "lane": "receiver" },
    { "id": "n8", "type": "end",        "label": "송금 완료",                          "lane": "receiver" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n6", "text": "수수료: 0% (무료)\n가스비: 0% (오프체인)\n처리: 즉시", "position": "right" },
    { "attachTo": "n3", "text": "양측 모두 Binance KYC 필수", "position": "left" }
  ]
}
```

---

### 2.1.2 Merchant 결제 (Hosted Checkout)

**스윔레인 정의**

```json
{
  "id": "bn-pay-hosted",
  "title": "Binance Pay - Merchant 결제 (Hosted Checkout)",
  "serviceColor": "#F0B90B",
  "category": "결제",
  "lanes": [
    { "id": "merchant", "actor": "merchant",  "label": "가맹점 서버" },
    { "id": "binance",  "actor": "platform",  "label": "Binance Pay API / FX Engine" },
    { "id": "customer", "actor": "buyer",     "label": "고객 (Binance 사용자)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",      "label": "주문 생성",                               "lane": "merchant" },
    { "id": "n2",  "type": "action",     "label": "Create Order V2 API 호출\n(POST /v2/order)", "lane": "merchant" },
    { "id": "n3",  "type": "action",     "label": "응답: checkoutUrl,\nqrcodeLink, deeplink,\nuniversalUrl", "lane": "binance" },
    { "id": "n4",  "type": "action",     "label": "Binance Web Checkout\n리다이렉트",          "lane": "customer" },
    { "id": "n5",  "type": "decision",   "label": "결제 방법?",                              "lane": "customer" },
    { "id": "n6",  "type": "action",     "label": "QR 코드 스캔",                            "lane": "customer" },
    { "id": "n7",  "type": "action",     "label": "딥링크 (앱 열기)",                         "lane": "customer" },
    { "id": "n8",  "type": "action",     "label": "웹 로그인",                               "lane": "customer" },
    { "id": "n9",  "type": "action",     "label": "암호화폐 선택\n(50종+ 지원)",               "lane": "customer" },
    { "id": "n10", "type": "payment",    "label": "결제 확인",                               "lane": "customer" },
    { "id": "n11", "type": "action",     "label": "결제 처리\n+ 자동 환전 (FX Engine)",        "lane": "binance" },
    { "id": "n12", "type": "settlement", "label": "가맹점 Funding Wallet\n정산 통화 즉시 입금", "lane": "binance" },
    { "id": "n13", "type": "action",     "label": "Webhook 콜백\nbizStatus: PAY_SUCCESS",    "lane": "binance" },
    { "id": "n14", "type": "action",     "label": "returnUrl 리다이렉트",                    "lane": "customer" },
    { "id": "n15", "type": "end",        "label": "결제 완료",                               "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "normal" },
    { "id": "e3",  "source": "n3",  "target": "n4",  "style": "normal" },
    { "id": "e4",  "source": "n4",  "target": "n5",  "style": "normal" },
    { "id": "e5",  "source": "n5",  "target": "n6",  "style": "conditional", "label": "QR" },
    { "id": "e6",  "source": "n5",  "target": "n7",  "style": "conditional", "label": "딥링크" },
    { "id": "e7",  "source": "n5",  "target": "n8",  "style": "conditional", "label": "웹" },
    { "id": "e8",  "source": "n6",  "target": "n9",  "style": "normal" },
    { "id": "e9",  "source": "n7",  "target": "n9",  "style": "normal" },
    { "id": "e10", "source": "n8",  "target": "n9",  "style": "normal" },
    { "id": "e11", "source": "n9",  "target": "n10", "style": "normal" },
    { "id": "e12", "source": "n10", "target": "n11", "style": "normal" },
    { "id": "e13", "source": "n11", "target": "n12", "style": "normal" },
    { "id": "e14", "source": "n12", "target": "n13", "style": "normal" },
    { "id": "e15", "source": "n13", "target": "n14", "style": "normal" },
    { "id": "e16", "source": "n14", "target": "n15", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n11", "text": "MDR: 1.0%\nFX 스프레드: 0.1~0.5%\n가스비: 0% (오프체인)\n처리: 즉시", "position": "right" },
    { "attachTo": "n4",  "text": "Binance 계정 필수", "position": "left" },
    { "attachTo": "n12", "text": "기본 정산 통화: USDT", "position": "right" }
  ]
}
```

---

### 2.1.3 Merchant 결제 (C2B Native API)

**스윔레인 정의**

```json
{
  "id": "bn-pay-c2b",
  "title": "Binance Pay - C2B Native API 결제",
  "serviceColor": "#F0B90B",
  "category": "결제",
  "lanes": [
    { "id": "merchant", "actor": "merchant",  "label": "가맹점 서버" },
    { "id": "binance",  "actor": "platform",  "label": "Binance Pay API" },
    { "id": "customer", "actor": "buyer",     "label": "고객 (Binance 사용자)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "주문 생성",                          "lane": "merchant" },
    { "id": "n2", "type": "action",     "label": "Create Order V2 API 호출",          "lane": "merchant" },
    { "id": "n3", "type": "action",     "label": "qrContent / deeplink 수신",         "lane": "binance" },
    { "id": "n4", "type": "action",     "label": "자체 UI에서 QR 렌더링\n또는 인앱 딥링크 구현", "lane": "merchant" },
    { "id": "n5", "type": "action",     "label": "Binance 앱에서\n결제 수단 선택",      "lane": "customer" },
    { "id": "n6", "type": "payment",    "label": "결제 확인",                          "lane": "customer" },
    { "id": "n7", "type": "action",     "label": "Webhook 결제 결과 수신",             "lane": "binance" },
    { "id": "n8", "type": "end",        "label": "결제 완료",                          "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n6", "text": "MDR: 1.0%\n가스비: 0%", "position": "right" },
    { "attachTo": "n4", "text": "개발 난이도 높음\n대규모 이커머스/앱에 적합", "position": "left" }
  ]
}
```

---

### 2.1.4 Payment Links 결제

**스윔레인 정의**

```json
{
  "id": "bn-pay-links",
  "title": "Binance Pay - Payment Links 결제",
  "serviceColor": "#F0B90B",
  "category": "결제",
  "lanes": [
    { "id": "merchant", "actor": "merchant",  "label": "가맹점" },
    { "id": "binance",  "actor": "platform",  "label": "Merchant Management Platform" },
    { "id": "customer", "actor": "buyer",     "label": "고객 (Binance 사용자)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "결제 링크 생성",              "lane": "merchant" },
    { "id": "n2", "type": "action",  "label": "대시보드에서 링크 생성\n(코딩 불필요)", "lane": "binance" },
    { "id": "n3", "type": "action",  "label": "링크 공유\n(이메일/SNS/웹사이트)", "lane": "merchant" },
    { "id": "n4", "type": "action",  "label": "링크 클릭\nBinance 결제 플로우 진행", "lane": "customer" },
    { "id": "n5", "type": "payment", "label": "결제 완료",                   "lane": "customer" },
    { "id": "n6", "type": "action",  "label": "대시보드에서 확인",             "lane": "binance" },
    { "id": "n7", "type": "end",     "label": "완료",                       "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5", "text": "MDR: 1.0%", "position": "right" },
    { "attachTo": "n2", "text": "개발 난이도 제로\n소규모 사업자/프리랜서 적합", "position": "left" }
  ]
}
```

---

### 2.1.5 QR 코드 오프라인 결제

**스윔레인 정의**

```json
{
  "id": "bn-pay-qr",
  "title": "Binance Pay - QR 코드 오프라인 결제",
  "serviceColor": "#F0B90B",
  "category": "결제",
  "lanes": [
    { "id": "merchant", "actor": "merchant",  "label": "가맹점 (매장)" },
    { "id": "binance",  "actor": "platform",  "label": "Binance Pay" },
    { "id": "customer", "actor": "buyer",     "label": "고객 (Binance 사용자)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "오프라인 결제 시작",            "lane": "merchant" },
    { "id": "n2", "type": "action",     "label": "API로 주문 생성\nQR 코드 디스플레이 표시", "lane": "merchant" },
    { "id": "n3", "type": "action",     "label": "Binance 앱 스캐너로\nQR 코드 스캔", "lane": "customer" },
    { "id": "n4", "type": "action",     "label": "금액/결제 대상 자동 인식",       "lane": "customer" },
    { "id": "n5", "type": "action",     "label": "암호화폐 선택 후 확인",         "lane": "customer" },
    { "id": "n6", "type": "payment",    "label": "즉시 처리",                    "lane": "binance" },
    { "id": "n7", "type": "action",     "label": "Webhook 알림",               "lane": "binance" },
    { "id": "n8", "type": "end",        "label": "결제 완료",                    "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n6", "text": "MDR: 1.0%\n처리: 즉시", "position": "right" },
    { "attachTo": "n2", "text": "오프라인 리테일 적합", "position": "left" }
  ]
}
```

---

### 2.1.6 Batch Payout (일괄 출금)

**스윔레인 정의**

```json
{
  "id": "bn-pay-payout",
  "title": "Binance Pay - Batch Payout (일괄 출금)",
  "serviceColor": "#F0B90B",
  "category": "결제",
  "lanes": [
    { "id": "merchant",  "actor": "merchant",  "label": "가맹점" },
    { "id": "binance",   "actor": "platform",  "label": "Binance Pay Payout API" },
    { "id": "receiver",  "actor": "buyer",     "label": "수신자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",      "label": "일괄 출금 시작",                   "lane": "merchant" },
    { "id": "n2",  "type": "action",     "label": "Payout API 호출\n또는 CSV 업로드\n(최대 500명/배치)", "lane": "merchant" },
    { "id": "n3",  "type": "decision",   "label": "수신자 유형?",                    "lane": "binance" },
    { "id": "n4",  "type": "settlement", "label": "Binance 사용자\nFunding Wallet 즉시 입금", "lane": "receiver" },
    { "id": "n5",  "type": "action",     "label": "비 Binance 사용자\n이메일 초대 발송",  "lane": "binance" },
    { "id": "n6",  "type": "decision",   "label": "72시간 내\nKYC 완료?",             "lane": "receiver" },
    { "id": "n7",  "type": "settlement", "label": "수신 확인",                       "lane": "receiver" },
    { "id": "n8",  "type": "refund",     "label": "자동 환불\n(가맹점에 반환)",         "lane": "binance" },
    { "id": "n9",  "type": "end",        "label": "처리 완료",                       "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "conditional", "label": "Binance 사용자" },
    { "id": "e4", "source": "n3", "target": "n5", "style": "conditional", "label": "비 Binance 사용자" },
    { "id": "e5", "source": "n4", "target": "n9", "style": "normal" },
    { "id": "e6", "source": "n5", "target": "n6", "style": "timing",      "label": "72시간 대기" },
    { "id": "e7", "source": "n6", "target": "n7", "style": "conditional", "label": "완료" },
    { "id": "e8", "source": "n6", "target": "n8", "style": "error",       "label": "미완료" },
    { "id": "e9", "source": "n7", "target": "n9", "style": "normal" },
    { "id": "e10","source": "n8", "target": "n9", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "Payout 수수료: 0.80%\n(건당 최대 USD 5)", "position": "right" },
    { "attachTo": "n2", "text": "2024.12부터 유료 전환", "position": "left" }
  ]
}
```

---

## 2.2 정산 (Settlement) 시나리오

---

### 2.2.1 오프체인 즉시 정산

**스윔레인 정의**

```json
{
  "id": "bn-set-offchain",
  "title": "Binance Pay - 오프체인 즉시 정산",
  "serviceColor": "#F0B90B",
  "category": "정산",
  "lanes": [
    { "id": "customer", "actor": "buyer",    "label": "고객" },
    { "id": "binance",  "actor": "platform", "label": "Binance Internal Ledger / FX Engine" },
    { "id": "merchant", "actor": "merchant", "label": "가맹점" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "결제 실행",                       "lane": "customer" },
    { "id": "n2", "type": "action",     "label": "고객 잔고에서\n결제 암호화폐 차감",  "lane": "binance" },
    { "id": "n3", "type": "action",     "label": "FX Engine\n결제 코인 → 정산 통화\n(내부 유동성 풀)", "lane": "binance" },
    { "id": "n4", "type": "action",     "label": "MDR 1% 차감\n(Binance 수수료 계정)", "lane": "binance" },
    { "id": "n5", "type": "settlement", "label": "가맹점 잔고에\n정산 통화 가산",      "lane": "binance" },
    { "id": "n6", "type": "action",     "label": "Funding Wallet 즉시 입금",        "lane": "merchant" },
    { "id": "n7", "type": "end",        "label": "정산 완료",                       "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5", "text": "정산 속도: 즉시 (T+0)\nLedger 성능: 10,000+ TPS, 10ms 이내", "position": "right" },
    { "attachTo": "n3", "text": "FX 스프레드: 0.1~0.5%\n(숨겨진 비용)", "position": "left" },
    { "attachTo": "n6", "text": "기본 정산 통화: USDT", "position": "right" }
  ]
}
```

---

### 2.2.2 법정화폐 전환 경로 (간접)

**스윔레인 정의**

```json
{
  "id": "bn-set-fiat",
  "title": "Binance Pay - 법정화폐 전환 및 은행 출금",
  "serviceColor": "#F0B90B",
  "category": "정산",
  "lanes": [
    { "id": "merchant", "actor": "merchant",  "label": "가맹점" },
    { "id": "binance",  "actor": "platform",  "label": "Binance 거래소" },
    { "id": "partner",  "actor": "platform",  "label": "채널 파트너 (Alchemy Pay 등)" },
    { "id": "bank",     "actor": "bank",      "label": "은행" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "USDT 수취 완료",                  "lane": "merchant" },
    { "id": "n2", "type": "action",     "label": "Binance 거래소에서\n수동 환전 (USDT → 법정화폐)", "lane": "binance" },
    { "id": "n3", "type": "action",     "label": "법정화폐 출금 신청",               "lane": "binance" },
    { "id": "n4", "type": "settlement", "label": "은행 계좌 입금",                  "lane": "bank" },
    { "id": "n5", "type": "end",        "label": "법정화폐 정산 완료",               "lane": "bank" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "거래소 환전 수수료: 0.1%", "position": "right" },
    { "attachTo": "n3", "text": "출금 수수료: ~$5~15", "position": "right" },
    { "attachTo": "n1", "text": "법정화폐 직접 은행 입금 불가\n(최대 구조적 약점)\n총 실효 수수료: ~1.4~1.5%", "position": "left" },
    { "attachTo": "n2", "text": "수동 처리 필요\n우회: Alchemy Pay 등 경유 가능", "position": "bottom" }
  ]
}
```

---

## 2.3 환불 (Refund) 시나리오

---

### 2.3.1 전액 환불

**스윔레인 정의**

```json
{
  "id": "bn-ref-full",
  "title": "Binance Pay - 전액 환불",
  "serviceColor": "#F0B90B",
  "category": "환불",
  "lanes": [
    { "id": "merchant", "actor": "merchant",  "label": "가맹점" },
    { "id": "binance",  "actor": "platform",  "label": "Binance Pay 시스템" },
    { "id": "customer", "actor": "buyer",     "label": "고객" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",   "label": "환불 요청",                           "lane": "merchant" },
    { "id": "n2",  "type": "decision","label": "환불 경로?",                           "lane": "merchant" },
    { "id": "n3",  "type": "action",  "label": "대시보드\nTransaction Tab 확인",        "lane": "merchant" },
    { "id": "n4",  "type": "action",  "label": "Refund Order API 호출\n(POST /order/refund)\nprepayId + 금액", "lane": "merchant" },
    { "id": "n5",  "type": "action",  "label": "주문 검증\n+ 환불 금액 검증\n+ 중복 요청 확인", "lane": "binance" },
    { "id": "n6",  "type": "refund",  "label": "가맹점 Funding Wallet\n환불금 차감",     "lane": "binance" },
    { "id": "n7",  "type": "settlement","label": "고객 Funding Wallet\n환불금 즉시 입금", "lane": "binance" },
    { "id": "n8",  "type": "action",  "label": "MDR 수수료 비례 환불\nrefundCommission 계산", "lane": "binance" },
    { "id": "n9",  "type": "action",  "label": "Webhook: REFUND_SUCCESS",            "lane": "binance" },
    { "id": "n10", "type": "action",  "label": "주문 상태: FULL_REFUNDED",             "lane": "binance" },
    { "id": "n11", "type": "end",     "label": "환불 완료",                            "lane": "customer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "conditional", "label": "대시보드" },
    { "id": "e3",  "source": "n2",  "target": "n4",  "style": "conditional", "label": "API" },
    { "id": "e4",  "source": "n3",  "target": "n5",  "style": "normal" },
    { "id": "e5",  "source": "n4",  "target": "n5",  "style": "normal" },
    { "id": "e6",  "source": "n5",  "target": "n6",  "style": "normal" },
    { "id": "e7",  "source": "n6",  "target": "n7",  "style": "normal" },
    { "id": "e8",  "source": "n7",  "target": "n8",  "style": "normal" },
    { "id": "e9",  "source": "n8",  "target": "n9",  "style": "normal" },
    { "id": "e10", "source": "n9",  "target": "n10", "style": "normal" },
    { "id": "e11", "source": "n10", "target": "n11", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n7",  "text": "처리 속도: 즉시 (오프체인)", "position": "right" },
    { "attachTo": "n8",  "text": "수수료 환불 공식:\nrefundCommission =\n(refundAmt / orderAmt)\n* originalCommission", "position": "right" }
  ]
}
```

---

### 2.3.2 부분 환불

**스윔레인 정의**

```json
{
  "id": "bn-ref-partial",
  "title": "Binance Pay - 부분 환불",
  "serviceColor": "#F0B90B",
  "category": "환불",
  "lanes": [
    { "id": "merchant", "actor": "merchant",  "label": "가맹점" },
    { "id": "binance",  "actor": "platform",  "label": "Binance Pay 시스템" },
    { "id": "customer", "actor": "buyer",     "label": "고객" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "부분 환불 요청",                           "lane": "merchant" },
    { "id": "n2", "type": "action",   "label": "Refund Order API 호출\n(refundAmount < orderAmount)", "lane": "merchant" },
    { "id": "n3", "type": "action",   "label": "검증 후 부분 환불 처리",                    "lane": "binance" },
    { "id": "n4", "type": "refund",   "label": "부분 금액 고객에게 전송",                   "lane": "binance" },
    { "id": "n5", "type": "decision", "label": "remainingAttempts\n= 1?",                "lane": "binance" },
    { "id": "n6", "type": "action",   "label": "추가 부분 환불 가능\n(누적 <= 원래 주문)",    "lane": "binance" },
    { "id": "n7", "type": "action",   "label": "다음 환불 시\n자동 전액 환불 처리",           "lane": "binance" },
    { "id": "n8", "type": "end",      "label": "환불 완료",                                "lane": "customer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "conditional", "label": "아니오 (잔여 횟수 있음)" },
    { "id": "e6", "source": "n5", "target": "n7", "style": "conditional", "label": "예 (마지막 1회)" },
    { "id": "e7", "source": "n6", "target": "n8", "style": "normal" },
    { "id": "e8", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "처리 속도: 즉시", "position": "right" },
    { "attachTo": "n5", "text": "duplicateRequest 플래그로\n중복 감지", "position": "left" },
    { "attachTo": "n3", "text": "에러 코드:\n400607 (횟수 초과)\n400608 (잘못된 금액)\n400611 (잔액 부족)", "position": "right" }
  ]
}
```

---

### 2.3.3 환불 통화 처리

**스윔레인 정의**

```json
{
  "id": "bn-ref-currency",
  "title": "Binance Pay - 환불 통화 변환 규칙",
  "serviceColor": "#F0B90B",
  "category": "환불",
  "lanes": [
    { "id": "customer",  "actor": "buyer",    "label": "고객" },
    { "id": "binance",   "actor": "platform", "label": "Binance Pay" },
    { "id": "merchant",  "actor": "merchant", "label": "가맹점" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "결제 시점",                         "lane": "customer" },
    { "id": "n2", "type": "payment",  "label": "고객이 BTC로 결제",                 "lane": "customer" },
    { "id": "n3", "type": "action",   "label": "FX Engine 변환\nBTC → USDT",       "lane": "binance" },
    { "id": "n4", "type": "settlement","label": "가맹점 USDT 수취",                "lane": "merchant" },
    { "id": "n5", "type": "action",   "label": "환불 시점\n(가격 변동 가능)",         "lane": "binance" },
    { "id": "n6", "type": "refund",   "label": "가맹점 정산 통화로 환불\n(USDT로 환불, 역환전 없음)", "lane": "binance" },
    { "id": "n7", "type": "action",   "label": "고객 USDT 수신\n(BTC 가격 상승 시 손실 가능)", "lane": "customer" },
    { "id": "n8", "type": "end",      "label": "환불 완료",                         "lane": "customer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "timing",   "label": "시간 경과" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n6", "text": "핵심 규칙: 역환전 미수행\n정산 통화로 환불", "position": "right" },
    { "attachTo": "n7", "text": "사용자 불만 요소:\nBTC 결제 → USDT 환불\n가격 변동 리스크", "position": "right" }
  ]
}
```

---

### 2.3.4 분쟁 해결

**스윔레인 정의**

```json
{
  "id": "bn-ref-dispute",
  "title": "Binance Pay - 분쟁 해결 절차",
  "serviceColor": "#F0B90B",
  "category": "환불",
  "lanes": [
    { "id": "customer", "actor": "buyer",    "label": "고객" },
    { "id": "merchant", "actor": "merchant", "label": "가맹점" },
    { "id": "binance",  "actor": "platform", "label": "Binance 고객지원팀" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",    "label": "분쟁 발생",                        "lane": "customer" },
    { "id": "n2",  "type": "decision", "label": "거래 유형?",                       "lane": "binance" },
    { "id": "n3",  "type": "action",   "label": "Merchant 결제 분쟁\n환불 여부 가맹점 재량", "lane": "merchant" },
    { "id": "n4",  "type": "action",   "label": "P2P 거래 분쟁\nAppeal 개시",        "lane": "customer" },
    { "id": "n5",  "type": "action",   "label": "10분간 채팅 협의",                  "lane": "customer" },
    { "id": "n6",  "type": "decision", "label": "합의 달성?",                       "lane": "binance" },
    { "id": "n7",  "type": "action",   "label": "합의에 따라 처리",                  "lane": "binance" },
    { "id": "n8",  "type": "action",   "label": "Binance 고객지원 중재\n(24~48시간 내 응답)", "lane": "binance" },
    { "id": "n9",  "type": "error",    "label": "차지백 없음\n구매자 보호 프로그램 없음", "lane": "customer" },
    { "id": "n10", "type": "end",      "label": "분쟁 종료",                        "lane": "binance" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "conditional", "label": "Merchant 결제" },
    { "id": "e3",  "source": "n2",  "target": "n4",  "style": "conditional", "label": "P2P 거래" },
    { "id": "e4",  "source": "n3",  "target": "n9",  "style": "normal" },
    { "id": "e5",  "source": "n4",  "target": "n5",  "style": "normal" },
    { "id": "e6",  "source": "n5",  "target": "n6",  "style": "timing",      "label": "10분" },
    { "id": "e7",  "source": "n6",  "target": "n7",  "style": "conditional", "label": "합의" },
    { "id": "e8",  "source": "n6",  "target": "n8",  "style": "conditional", "label": "미합의" },
    { "id": "e9",  "source": "n7",  "target": "n10", "style": "normal" },
    { "id": "e10", "source": "n8",  "target": "n10", "style": "normal" },
    { "id": "e11", "source": "n9",  "target": "n10", "style": "error" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n3", "text": "Binance 중개 가능\n강제력 제한", "position": "right" },
    { "attachTo": "n8", "text": "P2P 분쟁 수수료:\n4번째부터 부과 (처음 3회 무료)", "position": "right" }
  ]
}
```

---

---

# Tab 3: Coinbase Commerce

서비스 컬러: `#0052FF` (lighter variant)

---

## 3.1 결제 (Payment) 시나리오

---

### 3.1.1 기본 결제 (Commerce Charge)

**스윔레인 정의**

```json
{
  "id": "cc-pay-charge",
  "title": "Coinbase Commerce - 기본 결제 (Charge)",
  "serviceColor": "#0052FF",
  "category": "결제",
  "lanes": [
    { "id": "merchant", "actor": "merchant",   "label": "가맹점" },
    { "id": "commerce", "actor": "platform",   "label": "Commerce API" },
    { "id": "consumer", "actor": "buyer",      "label": "소비자" },
    { "id": "chain",    "actor": "blockchain", "label": "온체인 / DEX (Uniswap V3)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",      "label": "결제 시작",                     "lane": "merchant" },
    { "id": "n2",  "type": "action",     "label": "POST /charges\nCharge 객체 생성", "lane": "merchant" },
    { "id": "n3",  "type": "action",     "label": "hosted_url 접속",               "lane": "consumer" },
    { "id": "n4",  "type": "action",     "label": "토큰/네트워크 선택",              "lane": "consumer" },
    { "id": "n5",  "type": "payment",    "label": "지갑에서 온체인\n트랜잭션 실행",    "lane": "consumer" },
    { "id": "n6",  "type": "decision",   "label": "USDC 자동 환전\n필요?",           "lane": "chain" },
    { "id": "n7",  "type": "action",     "label": "Uniswap V3\nDEX 스왑",           "lane": "chain" },
    { "id": "n8",  "type": "action",     "label": "1% Commerce 수수료\n자동 차감",    "lane": "commerce" },
    { "id": "n9",  "type": "settlement", "label": "가맹점 지갑 정산",               "lane": "merchant" },
    { "id": "n10", "type": "end",        "label": "결제 완료",                     "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "normal" },
    { "id": "e3",  "source": "n3",  "target": "n4",  "style": "normal" },
    { "id": "e4",  "source": "n4",  "target": "n5",  "style": "normal" },
    { "id": "e5",  "source": "n5",  "target": "n6",  "style": "normal" },
    { "id": "e6",  "source": "n6",  "target": "n7",  "style": "conditional", "label": "예" },
    { "id": "e7",  "source": "n6",  "target": "n8",  "style": "conditional", "label": "아니오 (USDC)" },
    { "id": "e8",  "source": "n7",  "target": "n8",  "style": "normal" },
    { "id": "e9",  "source": "n8",  "target": "n9",  "style": "normal" },
    { "id": "e10", "source": "n9",  "target": "n10", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5", "text": "Coinbase 유저 → 무료, 즉시\n외부 지갑 → 1% + 가스비", "position": "right" },
    { "attachTo": "n7", "text": "DEX 스왑 포함 시: ~1.3% + 가스비\n(Uniswap 0.3% 추가)", "position": "right" },
    { "attachTo": "n9", "text": "정산 속도: ~200ms~2초 (Base)\n100+ 종 암호화폐 지원", "position": "right" },
    { "attachTo": "n2", "text": "Rate Limit:\n10,000 req/hr, 100 req/s", "position": "left" }
  ]
}
```

---

### 3.1.2 Commerce Payments Protocol (Authorize-Capture)

**스윔레인 정의**

```json
{
  "id": "cc-pay-authcapture",
  "title": "Coinbase Commerce - Authorize-Capture 결제",
  "serviceColor": "#0052FF",
  "category": "결제",
  "lanes": [
    { "id": "consumer", "actor": "buyer",      "label": "소비자" },
    { "id": "operator", "actor": "platform",   "label": "오퍼레이터 (Coinbase/Shopify)" },
    { "id": "merchant", "actor": "merchant",   "label": "가맹점" },
    { "id": "escrow",   "actor": "blockchain", "label": "에스크로 스마트 컨트랙트" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",     "label": "결제 시작",                           "lane": "consumer" },
    { "id": "n2",  "type": "action",    "label": "결제 서명",                           "lane": "consumer" },
    { "id": "n3",  "type": "payment",   "label": "AUTHORIZE\n자금 에스크로 예치",         "lane": "escrow" },
    { "id": "n4",  "type": "action",    "label": "상품 준비 완료",                       "lane": "merchant" },
    { "id": "n5",  "type": "decision",  "label": "진행?",                              "lane": "operator" },
    { "id": "n6",  "type": "settlement","label": "CAPTURE\n에스크로 → 가맹점 이동\n(부분 캡처 가능)", "lane": "escrow" },
    { "id": "n7",  "type": "refund",    "label": "VOID\n소비자 전액 반환",               "lane": "escrow" },
    { "id": "n8",  "type": "refund",    "label": "RECLAIM\n소비자 직접 회수\n(인가 만료 후)", "lane": "escrow" },
    { "id": "n9",  "type": "end",       "label": "완료",                               "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "conditional", "label": "Capture" },
    { "id": "e6", "source": "n5", "target": "n7", "style": "conditional", "label": "Void" },
    { "id": "e7", "source": "n5", "target": "n8", "style": "timing",      "label": "authExpiry 경과" },
    { "id": "e8", "source": "n6", "target": "n9", "style": "normal" },
    { "id": "e9", "source": "n7", "target": "n9", "style": "normal" },
    { "id": "e10","source": "n8", "target": "n9", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n6", "text": "수수료: 1%\n가스비: ~$0.01 (Base)", "position": "right" },
    { "attachTo": "n3", "text": "Shopify와 공동 개발 (오픈소스)\n실 채택률: $1.2M / 5,700 가맹점", "position": "left" },
    { "attachTo": "n8", "text": "신뢰 최소화 안전장치", "position": "right" }
  ]
}
```

---

### 3.1.3 Shopify 네이티브 통합 결제

**스윔레인 정의**

```json
{
  "id": "cc-pay-shopify",
  "title": "Coinbase Commerce - Shopify USDC 결제",
  "serviceColor": "#0052FF",
  "category": "결제",
  "lanes": [
    { "id": "merchant", "actor": "merchant",   "label": "Shopify 가맹점" },
    { "id": "consumer", "actor": "buyer",      "label": "소비자" },
    { "id": "chain",    "actor": "blockchain", "label": "Base 네트워크" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "결제 시작",                     "lane": "merchant" },
    { "id": "n2", "type": "action",     "label": "Shopify 플러그인 활성화\n(15분 내, 별도 게이트웨이 불필요)", "lane": "merchant" },
    { "id": "n3", "type": "action",     "label": "USDC로 결제\n(Base 네트워크)",    "lane": "consumer" },
    { "id": "n4", "type": "payment",    "label": "Base 기반 결제 실행",            "lane": "chain" },
    { "id": "n5", "type": "settlement", "label": "즉시 정산",                     "lane": "merchant" },
    { "id": "n6", "type": "end",        "label": "결제 완료",                     "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "수수료: 1% (Base)\n외환 수수료: 없음", "position": "right" },
    { "attachTo": "n2", "text": "34개국 550만 가맹점 접근 가능\nUSDC 직접 수령 또는\n법정화폐 수령 선택", "position": "left" }
  ]
}
```

---

## 3.2 정산 (Settlement) 시나리오

---

### 3.2.1 Self-Managed (비수탁형) 정산

**스윔레인 정의**

```json
{
  "id": "cc-set-self",
  "title": "Coinbase Commerce - Self-Managed 정산",
  "serviceColor": "#0052FF",
  "category": "정산",
  "lanes": [
    { "id": "chain",    "actor": "blockchain", "label": "온체인 (Base)" },
    { "id": "dex",      "actor": "blockchain", "label": "DEX (Uniswap V3)" },
    { "id": "merchant", "actor": "merchant",   "label": "가맹점 자체 지갑 (12단어 시드)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "결제 완료",                   "lane": "chain" },
    { "id": "n2", "type": "decision",   "label": "USDC 자동 스왑?",             "lane": "dex" },
    { "id": "n3", "type": "action",     "label": "DEX 스왑 실행",               "lane": "dex" },
    { "id": "n4", "type": "settlement", "label": "가맹점 자체 지갑\n직접 정산",   "lane": "merchant" },
    { "id": "n5", "type": "action",     "label": "1% 수수료 차감",              "lane": "chain" },
    { "id": "n6", "type": "end",        "label": "정산 완료",                   "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "conditional", "label": "예" },
    { "id": "e3", "source": "n2", "target": "n5", "style": "conditional", "label": "아니오" },
    { "id": "e4", "source": "n3", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n4", "style": "normal" },
    { "id": "e6", "source": "n4", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "Coinbase 유저: 즉시\nBase: ~200ms~2초\n법정화폐 인출: 불가", "position": "right" },
    { "attachTo": "n4", "text": "키 관리: 가맹점 책임\n분실 시 영구 손실\n카운터파티 리스크 없음", "position": "left" }
  ]
}
```

---

### 3.2.2 Coinbase-Managed (수탁형) 정산

**스윔레인 정의**

```json
{
  "id": "cc-set-managed",
  "title": "Coinbase Commerce - Coinbase-Managed 정산",
  "serviceColor": "#0052FF",
  "category": "정산",
  "lanes": [
    { "id": "chain",    "actor": "blockchain", "label": "온체인" },
    { "id": "coinbase", "actor": "platform",   "label": "Coinbase Exchange" },
    { "id": "bank",     "actor": "bank",       "label": "은행" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "결제 완료",                       "lane": "chain" },
    { "id": "n2", "type": "settlement", "label": "Coinbase Exchange\n계정에 정산",    "lane": "coinbase" },
    { "id": "n3", "type": "action",     "label": "1% 수수료 차감",                  "lane": "coinbase" },
    { "id": "n4", "type": "decision",   "label": "USD 자동 환전?",                  "lane": "coinbase" },
    { "id": "n5", "type": "action",     "label": "USD 자동 환전",                   "lane": "coinbase" },
    { "id": "n6", "type": "action",     "label": "크립토 보유 유지",                 "lane": "coinbase" },
    { "id": "n7", "type": "settlement", "label": "ACH/Wire 출금",                  "lane": "bank" },
    { "id": "n8", "type": "end",        "label": "법정화폐 정산 완료",               "lane": "bank" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "conditional", "label": "예" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "conditional", "label": "아니오" },
    { "id": "e6", "source": "n5", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n7", "text": "법정화폐 인출: 1-3 영업일\n환전 스프레드: 1-1.5%", "position": "right" },
    { "attachTo": "n2", "text": "Coinbase가 키 관리\nCoinbase 리스크 존재", "position": "left" }
  ]
}
```

---

### 3.2.3 Commerce Payments Protocol (하이브리드) 정산

**스윔레인 정의**

```json
{
  "id": "cc-set-protocol",
  "title": "Coinbase Commerce - Protocol 에스크로 정산",
  "serviceColor": "#0052FF",
  "category": "정산",
  "lanes": [
    { "id": "escrow",   "actor": "blockchain", "label": "스마트 컨트랙트 (에스크로)" },
    { "id": "operator", "actor": "platform",   "label": "오퍼레이터 (Coinbase/Shopify)" },
    { "id": "merchant", "actor": "merchant",   "label": "가맹점" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "자금 에스크로 보관",               "lane": "escrow" },
    { "id": "n2", "type": "action",     "label": "오퍼레이터가 결제 흐름 운영\n(자금 접근 불가)", "lane": "operator" },
    { "id": "n3", "type": "action",     "label": "가맹점 캡처 요청",                "lane": "merchant" },
    { "id": "n4", "type": "settlement", "label": "에스크로 → 가맹점\n즉시 정산",      "lane": "escrow" },
    { "id": "n5", "type": "end",        "label": "정산 완료",                       "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "캡처 시 즉시 정산\n부분 캡처 지원", "position": "right" },
    { "attachTo": "n2", "text": "오퍼레이터: 자금 접근 불가\n결제 흐름만 운영", "position": "left" }
  ]
}
```

---

## 3.3 환불 (Refund) 시나리오

---

### 3.3.1 Self-Managed 플랜 환불

**스윔레인 정의**

```json
{
  "id": "cc-ref-self",
  "title": "Coinbase Commerce - Self-Managed 수동 환불",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "consumer", "actor": "buyer",      "label": "소비자" },
    { "id": "merchant", "actor": "merchant",   "label": "가맹점" },
    { "id": "chain",    "actor": "blockchain", "label": "온체인" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "환불 요청",                      "lane": "consumer" },
    { "id": "n2", "type": "action",  "label": "오프체인 커뮤니케이션\n(이메일 등)", "lane": "consumer" },
    { "id": "n3", "type": "action",  "label": "소비자 수령 주소 확인",            "lane": "merchant" },
    { "id": "n4", "type": "refund",  "label": "자체 지갑에서\n직접 온체인 전송",    "lane": "merchant" },
    { "id": "n5", "type": "action",  "label": "소비자 지갑 수신",                "lane": "consumer" },
    { "id": "n6", "type": "end",     "label": "환불 완료",                      "lane": "consumer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "가스비: 가맹점 부담\n1% Commerce 수수료: 반환 안 됨", "position": "right" },
    { "attachTo": "n4", "text": "API 자동 환불 불가\n대시보드 환불 버튼 없음\n업계 최하위 자동화", "position": "left" }
  ]
}
```

---

### 3.3.2 Coinbase-Managed 플랜 환불

**스윔레인 정의**

```json
{
  "id": "cc-ref-managed",
  "title": "Coinbase Commerce - Managed 환불",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "consumer", "actor": "buyer",    "label": "소비자" },
    { "id": "merchant", "actor": "merchant", "label": "가맹점" },
    { "id": "coinbase", "actor": "platform", "label": "Coinbase Exchange" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "환불 요청",                        "lane": "consumer" },
    { "id": "n2", "type": "action",   "label": "Coinbase Exchange에서\n환불 처리",   "lane": "merchant" },
    { "id": "n3", "type": "decision", "label": "법정화폐 환전\n되었는가?",            "lane": "coinbase" },
    { "id": "n4", "type": "action",   "label": "재환전 필요\n(USD → 크립토)",        "lane": "coinbase" },
    { "id": "n5", "type": "refund",   "label": "Coinbase 경유\n소비자에게 전송",     "lane": "coinbase" },
    { "id": "n6", "type": "end",      "label": "환불 완료",                        "lane": "consumer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "conditional", "label": "예 (환전됨)" },
    { "id": "e4", "source": "n3", "target": "n5", "style": "conditional", "label": "아니오 (크립토 보유)" },
    { "id": "e5", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e6", "source": "n5", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "환전 손실:\n결제 시점 대비 환율 차이", "position": "right" }
  ]
}
```

---

### 3.3.3 Commerce Payments Protocol -- Void

**스윔레인 정의**

```json
{
  "id": "cc-ref-void",
  "title": "Coinbase Commerce - Protocol Void (캡처 전 취소)",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "operator", "actor": "platform",   "label": "오퍼레이터" },
    { "id": "escrow",   "actor": "blockchain", "label": "에스크로 컨트랙트" },
    { "id": "consumer", "actor": "buyer",      "label": "소비자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",  "label": "취소 요청",                    "lane": "operator" },
    { "id": "n2", "type": "action", "label": "void() 호출",                 "lane": "operator" },
    { "id": "n3", "type": "refund", "label": "에스크로 → 소비자 지갑\n전액 반환", "lane": "escrow" },
    { "id": "n4", "type": "end",    "label": "Void 완료",                   "lane": "consumer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n3", "text": "수수료: 없음\n가스비 외 비용 없음\n캡처 전에만 가능", "position": "right" }
  ]
}
```

---

### 3.3.4 Commerce Payments Protocol -- Refund

**스윔레인 정의**

```json
{
  "id": "cc-ref-protocol",
  "title": "Coinbase Commerce - Protocol Refund (캡처 후 환불)",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "operator",  "actor": "platform",   "label": "오퍼레이터" },
    { "id": "collector", "actor": "blockchain", "label": "OperatorRefundCollector" },
    { "id": "consumer",  "actor": "buyer",      "label": "소비자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "환불 요청",                       "lane": "operator" },
    { "id": "n2", "type": "action",   "label": "refund() 호출\n(refundExpiry 이전)", "lane": "operator" },
    { "id": "n3", "type": "action",   "label": "유동성 공급",                      "lane": "collector" },
    { "id": "n4", "type": "decision", "label": "전액?\n부분?",                    "lane": "collector" },
    { "id": "n5", "type": "refund",   "label": "전액/부분 환불 실행",              "lane": "collector" },
    { "id": "n6", "type": "end",      "label": "환불 완료",                       "lane": "consumer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "conditional", "label": "전액/부분" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5", "text": "가스비: 가맹점 부담", "position": "right" },
    { "attachTo": "n2", "text": "refundExpiry 이후 환불 불가\n(최종 확정 상태)", "position": "left" },
    { "attachTo": "n3", "text": "환불 유동성:\n오퍼레이터 별도 공급 필요", "position": "right" }
  ]
}
```

---

### 3.3.5 Commerce Payments Protocol -- Reclaim

**스윔레인 정의**

```json
{
  "id": "cc-ref-reclaim",
  "title": "Coinbase Commerce - Protocol Reclaim (소비자 직접 회수)",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "consumer", "actor": "buyer",      "label": "소비자" },
    { "id": "escrow",   "actor": "blockchain", "label": "에스크로 컨트랙트" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",  "label": "authExpiry 경과\n미캡처 상태",    "lane": "escrow" },
    { "id": "n2", "type": "action", "label": "소비자 직접\nreclaim() 호출",     "lane": "consumer" },
    { "id": "n3", "type": "refund", "label": "에스크로 전액\n소비자에게 반환",    "lane": "escrow" },
    { "id": "n4", "type": "end",    "label": "회수 완료",                      "lane": "consumer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "오퍼레이터 개입 불필요\n신뢰 최소화 안전장치\n소비자의 최후의 보호 수단", "position": "right" }
  ]
}
```

---

### 3.3.6 분쟁 해결

**스윔레인 정의**

```json
{
  "id": "cc-ref-dispute",
  "title": "Coinbase Commerce - 분쟁 해결 절차",
  "serviceColor": "#0052FF",
  "category": "환불",
  "lanes": [
    { "id": "consumer", "actor": "buyer",    "label": "소비자" },
    { "id": "merchant", "actor": "merchant", "label": "가맹점" },
    { "id": "coinbase", "actor": "platform", "label": "Coinbase" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "분쟁 발생",                         "lane": "consumer" },
    { "id": "n2", "type": "action",  "label": "가맹점에 직접 연락\n환불 협의",        "lane": "consumer" },
    { "id": "n3", "type": "action",  "label": "증빙 제출\n(거래ID, 고객정보, 기록)",  "lane": "consumer" },
    { "id": "n4", "type": "decision","label": "가맹점 환불 동의?",                  "lane": "merchant" },
    { "id": "n5", "type": "refund",  "label": "환불 처리",                         "lane": "merchant" },
    { "id": "n6", "type": "action",  "label": "Coinbase 공식 불만 접수",            "lane": "coinbase" },
    { "id": "n7", "type": "action",  "label": "45 영업일 이내 응답",                "lane": "coinbase" },
    { "id": "n8", "type": "error",   "label": "차지백 없음\n비가역적 거래\n소비자 보호 제한", "lane": "consumer" },
    { "id": "n9", "type": "end",     "label": "분쟁 종료",                         "lane": "coinbase" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "conditional", "label": "동의" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "conditional", "label": "거부" },
    { "id": "e6", "source": "n5", "target": "n9", "style": "normal" },
    { "id": "e7", "source": "n6", "target": "n7", "style": "timing",      "label": "최대 45 영업일" },
    { "id": "e8", "source": "n7", "target": "n8", "style": "error" },
    { "id": "e9", "source": "n8", "target": "n9", "style": "error" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n8", "text": "환불 자동화:\n경쟁사 대비 가장 뒤처진 영역", "position": "right" }
  ]
}
```

---

---

# Tab 4: Stripe Crypto

서비스 컬러: `#635BFF`

---

## 4.1 결제 (Payment) 시나리오

---

### 4.1.1 Stablecoin Payments (가맹점 USDC 수취)

**스윔레인 정의**

```json
{
  "id": "sc-pay-stablecoin",
  "title": "Stripe Crypto - Stablecoin Payments",
  "serviceColor": "#635BFF",
  "category": "결제",
  "lanes": [
    { "id": "merchant", "actor": "merchant",   "label": "가맹점" },
    { "id": "stripe",   "actor": "platform",   "label": "Stripe (crypto.stripe.com)" },
    { "id": "customer", "actor": "buyer",      "label": "고객 (월렛 보유)" },
    { "id": "chain",    "actor": "blockchain", "label": "블록체인" },
    { "id": "bridge",   "actor": "platform",   "label": "Bridge 엔진" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1",  "type": "start",      "label": "결제 시작",                              "lane": "merchant" },
    { "id": "n2",  "type": "action",     "label": "POST /v1/payment_intents\n(method: crypto)", "lane": "merchant" },
    { "id": "n3",  "type": "action",     "label": "client_secret 반환",                     "lane": "stripe" },
    { "id": "n4",  "type": "action",     "label": "confirmPayment()\ncrypto.stripe.com 리디렉션", "lane": "merchant" },
    { "id": "n5",  "type": "action",     "label": "월렛 연결\n토큰/체인 선택",                 "lane": "customer" },
    { "id": "n6",  "type": "payment",    "label": "트랜잭션 서명",                           "lane": "customer" },
    { "id": "n7",  "type": "action",     "label": "온체인 제출\n+ 블록 확인 모니터링",          "lane": "chain" },
    { "id": "n8",  "type": "action",     "label": "USDC → USD 자동 전환",                   "lane": "bridge" },
    { "id": "n9",  "type": "action",     "label": "payment_intent.succeeded\nWebhook 발송",  "lane": "stripe" },
    { "id": "n10", "type": "settlement", "label": "가맹점 Stripe 잔고\nUSD 반영",             "lane": "stripe" },
    { "id": "n11", "type": "end",        "label": "결제 완료",                              "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1",  "source": "n1",  "target": "n2",  "style": "normal" },
    { "id": "e2",  "source": "n2",  "target": "n3",  "style": "normal" },
    { "id": "e3",  "source": "n3",  "target": "n4",  "style": "normal" },
    { "id": "e4",  "source": "n4",  "target": "n5",  "style": "normal" },
    { "id": "e5",  "source": "n5",  "target": "n6",  "style": "normal" },
    { "id": "e6",  "source": "n6",  "target": "n7",  "style": "normal" },
    { "id": "e7",  "source": "n7",  "target": "n8",  "style": "normal" },
    { "id": "e8",  "source": "n8",  "target": "n9",  "style": "normal" },
    { "id": "e9",  "source": "n9",  "target": "n10", "style": "normal" },
    { "id": "e10", "source": "n10", "target": "n11", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n7",  "text": "온체인 확인:\nETH ~12초, SOL ~0.4초\nBase ~2초, Polygon ~2초", "position": "right" },
    { "attachTo": "n10", "text": "수수료: 1.5% (가스비 포함)\n정산: T+2 영업일 (USD)", "position": "right" },
    { "attachTo": "n5",  "text": "400+ 월렛 지원\n미국 기반 가맹점만 수취 가능\n고객: 글로벌", "position": "left" }
  ]
}
```

---

### 4.1.2 구독 결제 (Stablecoin Subscription)

**스윔레인 정의**

```json
{
  "id": "sc-pay-subscription",
  "title": "Stripe Crypto - 구독 결제",
  "serviceColor": "#635BFF",
  "category": "결제",
  "lanes": [
    { "id": "customer",  "actor": "buyer",      "label": "고객 (월렛)" },
    { "id": "stripe",    "actor": "platform",   "label": "Stripe" },
    { "id": "contract",  "actor": "blockchain", "label": "전용 스마트 컨트랙트" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "구독 시작",                          "lane": "customer" },
    { "id": "n2", "type": "action",  "label": "최초 1회 사전 승인\n(pre-approval) 서명", "lane": "customer" },
    { "id": "n3", "type": "action",  "label": "스마트 컨트랙트에\n반복 인출 권한 부여",   "lane": "contract" },
    { "id": "n4", "type": "payment", "label": "자동 정기 결제 실행\n(재서명 불필요)",     "lane": "contract" },
    { "id": "n5", "type": "settlement","label": "Stripe 잔고 반영",                  "lane": "stripe" },
    { "id": "n6", "type": "end",     "label": "반복 결제 완료",                      "lane": "stripe" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n4", "target": "n4", "style": "timing",  "label": "반복 주기 (매월 등)" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "업계 최초 크립토 구독 구현\n블록체인 '매 TX 서명' 한계 해결", "position": "left" },
    { "attachTo": "n4", "text": "수수료: 1.5%", "position": "right" }
  ]
}
```

---

### 4.1.3 Pay with Crypto (Crypto.com 연동)

**스윔레인 정의**

```json
{
  "id": "sc-pay-cryptodotcom",
  "title": "Stripe Crypto - Pay with Crypto (Crypto.com 연동)",
  "serviceColor": "#635BFF",
  "category": "결제",
  "lanes": [
    { "id": "consumer", "actor": "buyer",    "label": "소비자 (Crypto.com)" },
    { "id": "stripe",   "actor": "platform", "label": "Stripe" },
    { "id": "merchant", "actor": "merchant", "label": "가맹점" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "결제 시작",                        "lane": "consumer" },
    { "id": "n2", "type": "action",     "label": "Crypto.com 앱 내\n크립토 잔고로 결제", "lane": "consumer" },
    { "id": "n3", "type": "action",     "label": "법정화폐 자동 전환",                 "lane": "stripe" },
    { "id": "n4", "type": "settlement", "label": "가맹점 정산",                       "lane": "merchant" },
    { "id": "n5", "type": "end",        "label": "결제 완료",                        "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "사전 환전 불필요\n차지백 없음 (가맹점 유리)", "position": "left" },
    { "attachTo": "n3", "text": "수수료: 표준 Stripe 수수료 추정\n미국 우선, 글로벌 확대 예정", "position": "right" }
  ]
}
```

---

### 4.1.4 x402 머신/AI 에이전트 결제

**스윔레인 정의**

```json
{
  "id": "sc-pay-x402",
  "title": "Stripe Crypto - x402 머신/AI 에이전트 결제",
  "serviceColor": "#635BFF",
  "category": "결제",
  "lanes": [
    { "id": "client",      "actor": "buyer",      "label": "클라이언트 (AI 에이전트)" },
    { "id": "server",      "actor": "merchant",   "label": "서버 (API 제공자)" },
    { "id": "facilitator", "actor": "platform",   "label": "Stripe Facilitator" },
    { "id": "chain",       "actor": "blockchain", "label": "Base L2" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "유료 리소스 요청",                      "lane": "client" },
    { "id": "n2", "type": "action",     "label": "HTTP 402\n+ 결제 상세 반환",             "lane": "server" },
    { "id": "n3", "type": "payment",    "label": "결제 서명 생성",                        "lane": "client" },
    { "id": "n4", "type": "action",     "label": "PAYMENT-SIGNATURE\n헤더 포함 재요청",    "lane": "client" },
    { "id": "n5", "type": "action",     "label": "Stripe deposit address\n블록체인 모니터링", "lane": "facilitator" },
    { "id": "n6", "type": "settlement", "label": "Stripe 잔고 반영",                     "lane": "facilitator" },
    { "id": "n7", "type": "action",     "label": "리소스 제공",                          "lane": "server" },
    { "id": "n8", "type": "end",        "label": "완료",                                "lane": "client" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n7", "target": "n8", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5", "text": "프로토콜 수수료: 0% 주장\nStripe 정산 수수료 별도", "position": "right" },
    { "attachTo": "n2", "text": "3대 HTTP 헤더:\nPAYMENT-REQUIRED\nPAYMENT-SIGNATURE\nPAYMENT-RESPONSE", "position": "left" },
    { "attachTo": "n1", "text": "최근 30일:\n7,500만+ TX, $2,400만+ 볼륨\nUSDC on Base만 지원", "position": "left" }
  ]
}
```

---

### 4.1.5 MPP (Machine Payments Protocol)

**스윔레인 정의**

```json
{
  "id": "sc-pay-mpp",
  "title": "Stripe Crypto - MPP (Machine Payments Protocol)",
  "serviceColor": "#635BFF",
  "category": "결제",
  "lanes": [
    { "id": "agent",    "actor": "buyer",      "label": "AI 에이전트" },
    { "id": "stripe",   "actor": "platform",   "label": "Stripe / Tempo L1" },
    { "id": "provider", "actor": "merchant",   "label": "서비스 제공자" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "에이전트 결제 요청",                "lane": "agent" },
    { "id": "n2", "type": "action",     "label": "PaymentIntents API\n기반 결제",     "lane": "agent" },
    { "id": "n3", "type": "action",     "label": "SPTs를 통한\n에이전트 간 결제 권한 위임", "lane": "stripe" },
    { "id": "n4", "type": "payment",    "label": "결제 실행",                       "lane": "stripe" },
    { "id": "n5", "type": "settlement", "label": "배치 정산 처리",                   "lane": "stripe" },
    { "id": "n6", "type": "end",        "label": "완료",                           "lane": "provider" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "수수료: 거의 제로\n지연: 서브-100ms", "position": "right" },
    { "attachTo": "n3", "text": "SPTs: Shared Payment Tokens\n에이전트 간 권한 위임", "position": "left" },
    { "attachTo": "n5", "text": "결제 수단: 스테이블코인(Tempo)\n+ 카드(Stripe/Visa)\n+ BTC Lightning\n2026.03 론칭", "position": "right" }
  ]
}
```

---

### 4.1.6 Crypto Onramp (법정화폐 → 크립토)

**스윔레인 정의**

```json
{
  "id": "sc-pay-onramp",
  "title": "Stripe Crypto - Crypto Onramp",
  "serviceColor": "#635BFF",
  "category": "결제",
  "lanes": [
    { "id": "user",   "actor": "buyer",    "label": "사용자" },
    { "id": "dapp",   "actor": "merchant", "label": "DApp" },
    { "id": "stripe", "actor": "platform", "label": "Stripe Onramp 위젯" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "크립토 구매 시작",                    "lane": "user" },
    { "id": "n2", "type": "action",   "label": "임베디드 위젯\n또는 Stripe-hosted 리디렉션", "lane": "dapp" },
    { "id": "n3", "type": "action",   "label": "결제 수단 선택\n(카드, Apple Pay, ACH)", "lane": "user" },
    { "id": "n4", "type": "action",   "label": "내장 KYC\n+ Stripe Radar 사기 방지",  "lane": "stripe" },
    { "id": "n5", "type": "payment",  "label": "법정화폐 → 크립토 전환",              "lane": "stripe" },
    { "id": "n6", "type": "settlement","label": "크립토 사용자 지갑 입금",             "lane": "user" },
    { "id": "n7", "type": "end",      "label": "구매 완료",                          "lane": "user" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5", "text": "수수료: ~5% (카드), ~1.5% (ACH)\n예: $100 USDC = $4.99", "position": "right" },
    { "attachTo": "n2", "text": "Onramp만 지원\nOfframp 미제공", "position": "left" },
    { "attachTo": "n6", "text": "지원 크립토:\nUSDC(5개 체인), ETH,\nMATIC, AVAX, XLM\n지원 국가: 미국 + EU", "position": "right" }
  ]
}
```

---

## 4.2 정산 (Settlement) 시나리오

---

### 4.2.1 USDC → USD 자동 정산 (Full Shielding)

**스윔레인 정의**

```json
{
  "id": "sc-set-usd",
  "title": "Stripe Crypto - USDC → USD 자동 정산 (Full Shielding)",
  "serviceColor": "#635BFF",
  "category": "정산",
  "lanes": [
    { "id": "customer", "actor": "buyer",    "label": "고객 (월렛)" },
    { "id": "chain",    "actor": "blockchain","label": "블록체인" },
    { "id": "bridge",   "actor": "platform", "label": "Bridge 오케스트레이션 엔진" },
    { "id": "stripe",   "actor": "platform", "label": "Stripe 잔고" },
    { "id": "bank",     "actor": "bank",     "label": "가맹점 은행" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "스테이블코인 전송",                   "lane": "customer" },
    { "id": "n2", "type": "action",     "label": "블록체인 트랜잭션 확인",               "lane": "chain" },
    { "id": "n3", "type": "action",     "label": "스테이블코인 → USD 자동 전환\n(1:1 페깅, OTC/유동성 풀)", "lane": "bridge" },
    { "id": "n4", "type": "settlement", "label": "가맹점 Stripe 잔고 반영\n(카드 결제와 통합 관리)", "lane": "stripe" },
    { "id": "n5", "type": "settlement", "label": "ACH/SEPA 출금\n가맹점 은행 입금",      "lane": "bank" },
    { "id": "n6", "type": "end",        "label": "정산 완료",                          "lane": "bank" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "ETH ~12초, SOL ~0.4초\nBase ~2초, Polygon ~2초", "position": "right" },
    { "attachTo": "n4", "text": "정산 수수료: 1.5%에 포함\n(별도 없음)", "position": "right" },
    { "attachTo": "n5", "text": "정산 주기: T+2 영업일", "position": "right" },
    { "attachTo": "n3", "text": "가맹점 크립토 노출 제로\nSettlement Services Provider\n별도 계약 필요", "position": "left" }
  ]
}
```

---

### 4.2.2 USDC 직접 수취 (Stablecoin Financial Accounts)

**스윔레인 정의**

```json
{
  "id": "sc-set-usdc",
  "title": "Stripe Crypto - USDC 직접 수취",
  "serviceColor": "#635BFF",
  "category": "정산",
  "lanes": [
    { "id": "merchant", "actor": "merchant", "label": "가맹점" },
    { "id": "stripe",   "actor": "platform", "label": "Stripe Stablecoin Financial Accounts" },
    { "id": "bank",     "actor": "bank",     "label": "법정화폐 레일 (ACH/SEPA)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",      "label": "결제 수취",                         "lane": "merchant" },
    { "id": "n2", "type": "action",     "label": "USD 전환 없이\n스테이블코인 직접 보유", "lane": "stripe" },
    { "id": "n3", "type": "action",     "label": "다중 통화 잔고 관리",                "lane": "stripe" },
    { "id": "n4", "type": "decision",   "label": "법정화폐 전환?",                    "lane": "merchant" },
    { "id": "n5", "type": "settlement", "label": "ACH/SEPA 전환\n(USD, EUR)",         "lane": "bank" },
    { "id": "n6", "type": "action",     "label": "스테이블코인 유지",                  "lane": "stripe" },
    { "id": "n7", "type": "end",        "label": "정산 완료",                         "lane": "merchant" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "conditional", "label": "전환" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "conditional", "label": "유지" },
    { "id": "e6", "source": "n5", "target": "n7", "style": "normal" },
    { "id": "e7", "source": "n6", "target": "n7", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "지원 국가: 101개국\nUSDC (Circle), USDB (Bridge)", "position": "right" },
    { "attachTo": "n3", "text": "가상/실물 카드 발급 가능", "position": "left" },
    { "attachTo": "n5", "text": "전환 수수료: 발생", "position": "right" }
  ]
}
```

---

## 4.3 환불 (Refund) 시나리오

---

### 4.3.1 Stablecoin Payments 환불

**스윔레인 정의**

```json
{
  "id": "sc-ref-stablecoin",
  "title": "Stripe Crypto - Stablecoin Payments 환불",
  "serviceColor": "#635BFF",
  "category": "환불",
  "lanes": [
    { "id": "merchant", "actor": "merchant",   "label": "가맹점" },
    { "id": "stripe",   "actor": "platform",   "label": "Stripe" },
    { "id": "chain",    "actor": "blockchain", "label": "블록체인" },
    { "id": "customer", "actor": "buyer",      "label": "고객 (월렛)" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "환불 요청",                                  "lane": "merchant" },
    { "id": "n2", "type": "action",  "label": "POST /v1/refunds\n(charge=ch_xxx)\n또는 대시보드", "lane": "merchant" },
    { "id": "n3", "type": "action",  "label": "가맹점 잔고에서 차감 (USD)",                    "lane": "stripe" },
    { "id": "n4", "type": "action",  "label": "USD → 원래 스테이블코인 구매\n(역전환)",          "lane": "stripe" },
    { "id": "n5", "type": "refund",  "label": "고객 원래 월렛으로\n온체인 전송\n(새 블록체인 TX)", "lane": "chain" },
    { "id": "n6", "type": "action",  "label": "고객 월렛 수신 확인",                          "lane": "customer" },
    { "id": "n7", "type": "end",     "label": "환불 완료",                                   "lane": "customer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" },
    { "id": "e4", "source": "n4", "target": "n5", "style": "normal" },
    { "id": "e5", "source": "n5", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n6", "target": "n7", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n4", "text": "환불 통화: 원래 결제 스테이블코인", "position": "right" },
    { "attachTo": "n3", "text": "환불 수수료: 별도 명시 없음\n(Stripe 부담 추정)", "position": "left" },
    { "attachTo": "n5", "text": "Disputes 시스템 미적용\n차지백 없음\nTX 취소/역전 불가\n잘못된 주소 복구 불가", "position": "right" }
  ]
}
```

---

### 4.3.2 Pay with Crypto 환불

**스윔레인 정의**

```json
{
  "id": "sc-ref-crypto",
  "title": "Stripe Crypto - Pay with Crypto 환불",
  "serviceColor": "#635BFF",
  "category": "환불",
  "lanes": [
    { "id": "merchant", "actor": "merchant",   "label": "가맹점" },
    { "id": "chain",    "actor": "blockchain", "label": "블록체인" },
    { "id": "customer", "actor": "buyer",      "label": "고객" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",   "label": "환불 요청",                           "lane": "customer" },
    { "id": "n2", "type": "action",  "label": "가맹점 직접 환불 처리",                "lane": "merchant" },
    { "id": "n3", "type": "refund",  "label": "고객 원래 월렛으로\n스테이블코인 반환",  "lane": "chain" },
    { "id": "n4", "type": "end",     "label": "환불 완료",                           "lane": "customer" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "normal" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n2", "text": "수수료: 미공개\n차지백 없음", "position": "right" },
    { "attachTo": "n3", "text": "크립토 가치 수동 추적 필요", "position": "left" }
  ]
}
```

---

### 4.3.3 분쟁(Dispute) 처리

**스윔레인 정의**

```json
{
  "id": "sc-ref-dispute",
  "title": "Stripe Crypto - 분쟁 처리",
  "serviceColor": "#635BFF",
  "category": "환불",
  "lanes": [
    { "id": "customer", "actor": "buyer",    "label": "고객" },
    { "id": "merchant", "actor": "merchant", "label": "가맹점" },
    { "id": "stripe",   "actor": "platform", "label": "Stripe" }
  ]
}
```

**노드 정의**

```json
{
  "nodes": [
    { "id": "n1", "type": "start",    "label": "분쟁 발생",                         "lane": "customer" },
    { "id": "n2", "type": "action",   "label": "가맹점에 직접 연락",                 "lane": "customer" },
    { "id": "n3", "type": "decision", "label": "가맹점 환불 결정?",                  "lane": "merchant" },
    { "id": "n4", "type": "refund",   "label": "환불 처리\n(POST /v1/refunds)",     "lane": "merchant" },
    { "id": "n5", "type": "error",    "label": "Disputes 시스템 미적용\n차지백 없음\n소비자 구제 수단 없음", "lane": "stripe" },
    { "id": "n6", "type": "end",      "label": "분쟁 종료",                         "lane": "stripe" }
  ]
}
```

**엣지 정의**

```json
{
  "edges": [
    { "id": "e1", "source": "n1", "target": "n2", "style": "normal" },
    { "id": "e2", "source": "n2", "target": "n3", "style": "normal" },
    { "id": "e3", "source": "n3", "target": "n4", "style": "conditional", "label": "환불 결정" },
    { "id": "e4", "source": "n3", "target": "n5", "style": "error",       "label": "거부" },
    { "id": "e5", "source": "n4", "target": "n6", "style": "normal" },
    { "id": "e6", "source": "n5", "target": "n6", "style": "error" }
  ]
}
```

**주석 (Annotations)**

```json
{
  "annotations": [
    { "attachTo": "n5", "text": "기존 Stripe 카드의\n강력한 Disputes 시스템이\n크립토에는 미적용", "position": "right" },
    { "attachTo": "n3", "text": "사기성 분쟁에서\n가맹점 자유\n소비자 보호 부재", "position": "left" }
  ]
}
```

---

---

# Tab 5: 서비스 비교 (Cross-Service Comparison)

---

## 5.1 결제 비교 다이어그램

이 비교 뷰는 4개 서비스의 기본 결제 플로우를 병렬로 표시하는 비교 다이어그램이다.

```json
{
  "id": "comparison-payment",
  "title": "크립토 결제 서비스 비교 - 결제 플로우",
  "type": "comparisonGrid",
  "layout": {
    "columns": 4,
    "columnWidth": 280,
    "rowHeight": "auto"
  },
  "services": [
    {
      "id": "basePay",
      "label": "Base Pay",
      "color": "#0052FF",
      "architecture": "온체인 (스마트 컨트랙트)",
      "keyMetrics": {
        "baseFee": "1%",
        "gasFee": "~$0.01 (구매자)",
        "speed": "~2초 (Base)",
        "escrow": "온체인 지원",
        "accountRequired": "불필요 (지갑만)",
        "openSource": true,
        "supportedCrypto": "Uniswap V3 전체",
        "integrationDifficulty": "중간"
      },
      "simplifiedFlow": [
        { "step": 1, "label": "머천트: 결제 요청", "type": "action" },
        { "step": 2, "label": "오퍼레이터: TransferIntent 생성", "type": "action" },
        { "step": 3, "label": "구매자: 지갑 연결 + 승인", "type": "action" },
        { "step": 4, "label": "컨트랙트: 토큰 전송 (자동 스왑)", "type": "payment" },
        { "step": 5, "label": "머천트 지갑 즉시 정산", "type": "settlement" }
      ]
    },
    {
      "id": "binancePay",
      "label": "Binance Pay",
      "color": "#F0B90B",
      "architecture": "오프체인 (내부 원장)",
      "keyMetrics": {
        "baseFee": "1%",
        "gasFee": "0%",
        "speed": "즉시 (10ms)",
        "escrow": "미지원",
        "accountRequired": "Binance 계정 필수",
        "openSource": false,
        "supportedCrypto": "300종+ (P2P) / 50종+ (가맹점)",
        "integrationDifficulty": "낮음~높음"
      },
      "simplifiedFlow": [
        { "step": 1, "label": "가맹점: Create Order API", "type": "action" },
        { "step": 2, "label": "고객: Binance 결제 페이지", "type": "action" },
        { "step": 3, "label": "고객: 암호화폐 선택 + 결제", "type": "payment" },
        { "step": 4, "label": "FX Engine: 자동 환전", "type": "action" },
        { "step": 5, "label": "가맹점 Funding Wallet 즉시 입금", "type": "settlement" }
      ]
    },
    {
      "id": "coinbaseCommerce",
      "label": "Coinbase Commerce",
      "color": "#0052FF",
      "architecture": "온체인 (스마트 컨트랙트)",
      "keyMetrics": {
        "baseFee": "1% (Coinbase 유저 무료)",
        "gasFee": "~$0.01 (구매자)",
        "speed": "~200ms~2초 (Base)",
        "escrow": "온체인 지원",
        "accountRequired": "불필요 (지갑만)",
        "openSource": true,
        "supportedCrypto": "100+ 종",
        "integrationDifficulty": "중간"
      },
      "simplifiedFlow": [
        { "step": 1, "label": "가맹점: POST /charges", "type": "action" },
        { "step": 2, "label": "소비자: hosted_url 접속", "type": "action" },
        { "step": 3, "label": "소비자: 토큰 선택 + 온체인 TX", "type": "payment" },
        { "step": 4, "label": "DEX: USDC 자동 환전 (선택)", "type": "action" },
        { "step": 5, "label": "가맹점 지갑 직접 정산", "type": "settlement" }
      ]
    },
    {
      "id": "stripeCrypto",
      "label": "Stripe Crypto",
      "color": "#635BFF",
      "architecture": "온체인 수취 + 오프체인 정산",
      "keyMetrics": {
        "baseFee": "1.5%",
        "gasFee": "포함 (Stripe 부담)",
        "speed": "0.4~12초 (체인별)",
        "escrow": "오프체인 (구독만)",
        "accountRequired": "불필요 (월렛만)",
        "openSource": false,
        "supportedCrypto": "스테이블코인 3종",
        "integrationDifficulty": "매우 낮음"
      },
      "simplifiedFlow": [
        { "step": 1, "label": "가맹점: PaymentIntents API", "type": "action" },
        { "step": 2, "label": "고객: crypto.stripe.com 결제", "type": "action" },
        { "step": 3, "label": "고객: 월렛 서명 + 온체인 전송", "type": "payment" },
        { "step": 4, "label": "Bridge: USDC → USD 자동 전환", "type": "action" },
        { "step": 5, "label": "가맹점 Stripe 잔고 USD 반영", "type": "settlement" }
      ]
    }
  ]
}
```

---

## 5.2 정산 비교 다이어그램

```json
{
  "id": "comparison-settlement",
  "title": "크립토 결제 서비스 비교 - 정산 플로우",
  "type": "comparisonTable",
  "headers": ["항목", "Base Pay", "Binance Pay", "Coinbase Commerce", "Stripe Crypto"],
  "rows": [
    {
      "label": "크립토 정산 속도",
      "values": [
        { "text": "~2초 (온체인)", "color": "#0052FF" },
        { "text": "즉시 (오프체인)", "color": "#F0B90B", "highlight": true },
        { "text": "~200ms~2초 (온체인)", "color": "#0052FF" },
        { "text": "0.4~12초 (체인별)", "color": "#635BFF" }
      ]
    },
    {
      "label": "법정화폐 정산 속도",
      "values": [
        { "text": "1-5 영업일 (간접)", "color": "#0052FF" },
        { "text": "수동 처리 필요", "color": "#F0B90B", "warning": true },
        { "text": "1-3 영업일 (Managed)", "color": "#0052FF" },
        { "text": "T+2 영업일", "color": "#635BFF", "highlight": true }
      ]
    },
    {
      "label": "법정화폐 직접 정산",
      "values": [
        { "text": "간접 (Coinbase 경유)", "color": "#0052FF" },
        { "text": "불가", "color": "#F0B90B", "warning": true },
        { "text": "가능 (Managed, USD만)", "color": "#0052FF" },
        { "text": "자동 지원 (USD)", "color": "#635BFF", "highlight": true }
      ]
    },
    {
      "label": "기본 정산 통화",
      "values": [
        { "text": "USDC", "color": "#0052FF" },
        { "text": "USDT", "color": "#F0B90B" },
        { "text": "USDC", "color": "#0052FF" },
        { "text": "USD", "color": "#635BFF" }
      ]
    },
    {
      "label": "가맹점 크립토 노출",
      "values": [
        { "text": "있음", "color": "#0052FF" },
        { "text": "있음", "color": "#F0B90B" },
        { "text": "있음 (Self-Managed)", "color": "#0052FF" },
        { "text": "없음 (완전 차폐)", "color": "#635BFF", "highlight": true }
      ]
    },
    {
      "label": "총비용 (USD 정산)",
      "values": [
        { "text": "~1% + 간접 비용", "color": "#0052FF" },
        { "text": "~1.4~1.5%", "color": "#F0B90B" },
        { "text": "~2~2.5%", "color": "#0052FF", "warning": true },
        { "text": "1.5% (all-in)", "color": "#635BFF" }
      ]
    }
  ]
}
```

---

## 5.3 환불 비교 다이어그램

```json
{
  "id": "comparison-refund",
  "title": "크립토 결제 서비스 비교 - 환불 플로우",
  "type": "comparisonTable",
  "headers": ["항목", "Base Pay", "Binance Pay", "Coinbase Commerce", "Stripe Crypto"],
  "rows": [
    {
      "label": "환불 방식",
      "values": [
        { "text": "온체인 (스마트 컨트랙트)", "color": "#0052FF" },
        { "text": "오프체인 (API/대시보드)", "color": "#F0B90B" },
        { "text": "수동 온체인 / Protocol", "color": "#0052FF" },
        { "text": "온체인 (Stripe 대행)", "color": "#635BFF" }
      ]
    },
    {
      "label": "자동 환불",
      "values": [
        { "text": "지원 (2세대)", "color": "#0052FF" },
        { "text": "API + 대시보드", "color": "#F0B90B", "highlight": true },
        { "text": "제한적 (Protocol만)", "color": "#0052FF", "warning": true },
        { "text": "API + 대시보드", "color": "#635BFF", "highlight": true }
      ]
    },
    {
      "label": "부분 환불",
      "values": [
        { "text": "지원 (2세대)", "color": "#0052FF" },
        { "text": "지원 (다회 반복)", "color": "#F0B90B" },
        { "text": "지원 (Protocol)", "color": "#0052FF" },
        { "text": "지원", "color": "#635BFF" }
      ]
    },
    {
      "label": "Void (캡처 전 취소)",
      "values": [
        { "text": "지원 (수수료 미발생)", "color": "#0052FF", "highlight": true },
        { "text": "미지원", "color": "#F0B90B", "warning": true },
        { "text": "지원 (수수료 미발생)", "color": "#0052FF", "highlight": true },
        { "text": "미지원", "color": "#635BFF", "warning": true }
      ]
    },
    {
      "label": "Reclaim (자금 회수)",
      "values": [
        { "text": "지원 (소비자 직접)", "color": "#0052FF", "highlight": true },
        { "text": "미지원", "color": "#F0B90B", "warning": true },
        { "text": "지원 (소비자 직접)", "color": "#0052FF", "highlight": true },
        { "text": "미지원", "color": "#635BFF", "warning": true }
      ]
    },
    {
      "label": "환불 통화",
      "values": [
        { "text": "원래 결제 토큰", "color": "#0052FF" },
        { "text": "정산 통화 (USDT)", "color": "#F0B90B", "warning": true },
        { "text": "USDC (온체인)", "color": "#0052FF" },
        { "text": "원래 스테이블코인", "color": "#635BFF" }
      ]
    },
    {
      "label": "수수료 환불",
      "values": [
        { "text": "오퍼레이터 재량", "color": "#0052FF" },
        { "text": "비례 환불됨", "color": "#F0B90B", "highlight": true },
        { "text": "반환 안 됨", "color": "#0052FF", "warning": true },
        { "text": "미공개", "color": "#635BFF" }
      ]
    },
    {
      "label": "환불 속도",
      "values": [
        { "text": "~2초 (Base)", "color": "#0052FF" },
        { "text": "즉시 (오프체인)", "color": "#F0B90B", "highlight": true },
        { "text": "블록 확인 시간", "color": "#0052FF" },
        { "text": "블록 확인 시간", "color": "#635BFF" }
      ]
    },
    {
      "label": "차지백",
      "values": [
        { "text": "없음", "color": "#0052FF" },
        { "text": "없음", "color": "#F0B90B" },
        { "text": "없음", "color": "#0052FF" },
        { "text": "없음", "color": "#635BFF" }
      ]
    }
  ]
}
```

---

## 렌더링 가이드 (프론트엔드 구현 참고)

### 다이어그램 렌더링 권장 라이브러리

| 라이브러리 | 용도 | 비고 |
|-----------|------|------|
| **React Flow** / **Svelte Flow** | 노드-엣지 기반 다이어그램 | 스윔레인 + 자유 배치 |
| **Mermaid.js** | 빠른 프로토타입 | 마크다운 내 인라인 |
| **D3.js** | 커스텀 SVG 다이어그램 | 최대 유연성 |
| **ELK.js** | 자동 레이아웃 엔진 | 스윔레인 레이아웃에 적합 |

### 스윔레인 렌더링 방법

1. 각 `lane`을 수평 또는 수직 밴드로 구분
2. `actorColors`에서 배경색, 테두리색 적용
3. 노드를 해당 `lane` 영역 내에 배치
4. 엣지는 `edgeStyles`에 따라 선 스타일 적용
5. `annotations`는 해당 노드 근처에 말풍선/노트로 표시

### 탭 네비게이션 구현

```
[Base Pay] [Binance Pay] [Coinbase Commerce] [Stripe Crypto] [서비스 비교]
     |
     +-- [결제] [정산] [환불]  ← 서브탭
              |
              +-- 시나리오 목록 (사이드바 또는 드롭다운)
                      |
                      +-- 개별 다이어그램 렌더링 영역
```

### 반응형 고려사항

- 모바일: 스윔레인을 수직 스택으로 전환, 노드 크기 축소
- 태블릿: 2열 스윔레인, 줌/팬 지원
- 데스크톱: 전체 스윔레인 수평 표시, 비교 뷰 그리드

---

## 시나리오 인덱스 (전체 목록)

| # | 서비스 | 카테고리 | 시나리오 ID | 시나리오 이름 |
|---|--------|---------|------------|-------------|
| 1 | Base Pay | 결제 | bp-pay-charge | 즉시 결제 (Charge) |
| 2 | Base Pay | 결제 | bp-pay-authcapture | 인가-캡처 결제 |
| 3 | Base Pay | 결제 | bp-pay-x402 | x402 머신/AI 에이전트 결제 |
| 4 | Base Pay | 정산 | bp-set-charge | 온체인 즉시 정산 |
| 5 | Base Pay | 정산 | bp-set-escrow | 에스크로 캡처 후 정산 |
| 6 | Base Pay | 정산 | bp-set-fiat | 법정화폐 전환 정산 |
| 7 | Base Pay | 환불 | bp-ref-void | 캡처 전 취소 (Void) |
| 8 | Base Pay | 환불 | bp-ref-postCapture | 캡처 후 환불 |
| 9 | Base Pay | 환불 | bp-ref-reclaim | 소비자 직접 회수 (Reclaim) |
| 10 | Base Pay | 환불 | bp-ref-charge | Charge 후 환불 |
| 11 | Base Pay | 환불 | bp-ref-dispute | 분쟁 해결 |
| 12 | Binance Pay | 결제 | bn-pay-p2p | P2P 개인 간 결제 |
| 13 | Binance Pay | 결제 | bn-pay-hosted | Merchant 결제 (Hosted Checkout) |
| 14 | Binance Pay | 결제 | bn-pay-c2b | C2B Native API 결제 |
| 15 | Binance Pay | 결제 | bn-pay-links | Payment Links 결제 |
| 16 | Binance Pay | 결제 | bn-pay-qr | QR 코드 오프라인 결제 |
| 17 | Binance Pay | 결제 | bn-pay-payout | Batch Payout (일괄 출금) |
| 18 | Binance Pay | 정산 | bn-set-offchain | 오프체인 즉시 정산 |
| 19 | Binance Pay | 정산 | bn-set-fiat | 법정화폐 전환 경로 |
| 20 | Binance Pay | 환불 | bn-ref-full | 전액 환불 |
| 21 | Binance Pay | 환불 | bn-ref-partial | 부분 환불 |
| 22 | Binance Pay | 환불 | bn-ref-currency | 환불 통화 처리 |
| 23 | Binance Pay | 환불 | bn-ref-dispute | 분쟁 해결 |
| 24 | Coinbase Commerce | 결제 | cc-pay-charge | 기본 결제 (Charge) |
| 25 | Coinbase Commerce | 결제 | cc-pay-authcapture | Authorize-Capture 결제 |
| 26 | Coinbase Commerce | 결제 | cc-pay-shopify | Shopify USDC 결제 |
| 27 | Coinbase Commerce | 정산 | cc-set-self | Self-Managed 정산 |
| 28 | Coinbase Commerce | 정산 | cc-set-managed | Coinbase-Managed 정산 |
| 29 | Coinbase Commerce | 정산 | cc-set-protocol | Protocol 에스크로 정산 |
| 30 | Coinbase Commerce | 환불 | cc-ref-self | Self-Managed 수동 환불 |
| 31 | Coinbase Commerce | 환불 | cc-ref-managed | Managed 환불 |
| 32 | Coinbase Commerce | 환불 | cc-ref-void | Protocol Void |
| 33 | Coinbase Commerce | 환불 | cc-ref-protocol | Protocol Refund |
| 34 | Coinbase Commerce | 환불 | cc-ref-reclaim | Protocol Reclaim |
| 35 | Coinbase Commerce | 환불 | cc-ref-dispute | 분쟁 해결 |
| 36 | Stripe Crypto | 결제 | sc-pay-stablecoin | Stablecoin Payments |
| 37 | Stripe Crypto | 결제 | sc-pay-subscription | 구독 결제 |
| 38 | Stripe Crypto | 결제 | sc-pay-cryptodotcom | Pay with Crypto |
| 39 | Stripe Crypto | 결제 | sc-pay-x402 | x402 머신/AI 결제 |
| 40 | Stripe Crypto | 결제 | sc-pay-mpp | MPP (Machine Payments) |
| 41 | Stripe Crypto | 결제 | sc-pay-onramp | Crypto Onramp |
| 42 | Stripe Crypto | 정산 | sc-set-usd | USDC → USD 자동 정산 |
| 43 | Stripe Crypto | 정산 | sc-set-usdc | USDC 직접 수취 |
| 44 | Stripe Crypto | 환불 | sc-ref-stablecoin | Stablecoin Payments 환불 |
| 45 | Stripe Crypto | 환불 | sc-ref-crypto | Pay with Crypto 환불 |
| 46 | Stripe Crypto | 환불 | sc-ref-dispute | 분쟁 처리 |

**총 46개 시나리오** (결제 18 + 정산 10 + 환불 18)
