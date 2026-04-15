---
name: internal-pptx-creator
description: "'내부 공유용 PPT 만들어줘', '팀 발표 자료 작성해줘', '사내 보고용 슬라이드 제작해줘', '회의 자료 PPT로 정리해줘', '내부 공유할 프레젠테이션 파일 만들어줘'"
---

# internal-pptx-creator — 내부 공유용 PPTX 작성

사용자가 제공한 주제나 내용을 바탕으로 내부 공유용 파워포인트 발표 자료를 자동으로 작성합니다. 슬라이드 구성, 핵심 메시지 정리, 시각적 레이아웃 제안까지 포함한 PPTX 파일을 생성합니다. 팀 내 보고, 업무 공유, 프로젝트 현황 전달 등 다양한 내부 커뮤니케이션 목적에 맞게 활용할 수 있습니다.

## 에이전트 구성

| 에이전트 | 파일 | 역할 | 타입 |
|---------|------|------|------|
| qCLvQBxrVaT--83jk1DOV | `.claude/agents/qCLvQBxrVaT--83jk1DOV.md` | 발표 목적과 청중을 분석하고 슬라이드 구성안(목차)을 설계한다 | general-purpose |
| psURZPKI-a3rVsU4wpmlO | `.claude/agents/psURZPKI-a3rVsU4wpmlO.md` | 슬라이드 구성안을 바탕으로 각 슬라이드의 본문 콘텐츠를 작성한다 | general-purpose |
| O3SKlVKmjN6yOPfG05x-e | `.claude/agents/O3SKlVKmjN6yOPfG05x-e.md` | 슬라이드별 레이아웃, 색상 테마, 시각화 요소를 설계하고 Mermaid 다이어그램을 작성한다 | general-purpose |
| AjEWliVaNE6MmgqxCgBou | `.claude/agents/AjEWliVaNE6MmgqxCgBou.md` | 모든 산출물을 종합하여 python-pptx로 실제 PPTX 파일을 생성한다 | general-purpose |

## 실행 준비 (오케스트레이터 수행)

1. 사용자 입력에서 핵심 요구사항을 추출한다
2. `_workspace/` 디렉토리를 프로젝트 루트에 생성한다
3. 입력을 정리하여 `_workspace/00_input.md`에 저장한다
4. 요청 범위에 따라 실행 모드를 결정한다 (아래 "작업 규모별 모드" 참조)

## 워크플로우

### Phase 1

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| qCLvQBxrVaT--83jk1DOV | 발표 목적과 청중을 분석하고 슬라이드 구성안(목차)을 설계한다 | 없음 | `_workspace/01_content-planner_output.md` |

### Phase 2

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| psURZPKI-a3rVsU4wpmlO | 슬라이드 구성안을 바탕으로 각 슬라이드의 본문 콘텐츠를 작성한다 | qCLvQBxrVaT--83jk1DOV | `_workspace/02_slide-writer_output.md` |

### Phase 3

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| O3SKlVKmjN6yOPfG05x-e | 슬라이드별 레이아웃, 색상 테마, 시각화 요소를 설계하고 Mermaid 다이어그램을 작성한다 | psURZPKI-a3rVsU4wpmlO | `_workspace/03_visual-designer_output.md` |

### Phase 4

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| AjEWliVaNE6MmgqxCgBou | 모든 산출물을 종합하여 python-pptx로 실제 PPTX 파일을 생성한다 | qCLvQBxrVaT--83jk1DOV, psURZPKI-a3rVsU4wpmlO, O3SKlVKmjN6yOPfG05x-e | `_workspace/04_pptx-builder_output.md` |

## 에이전트 간 통신 프로토콜

- 에이전트 간 SendMessage를 통해 직접 통신하며 작업 결과를 교차 검증한다
- 각 에이전트는 작업 완료 후 산출물을 `_workspace/` 디렉토리에 저장한다
- 후속 에이전트는 선행 에이전트의 산출물을 읽어 작업을 이어간다

## 순서 (요약)

| 순서 | 담당 | 의존 |
|------|------|------|
| 1 | qCLvQBxrVaT--83jk1DOV | 없음 |
| 2 | psURZPKI-a3rVsU4wpmlO | qCLvQBxrVaT--83jk1DOV |
| 3 | O3SKlVKmjN6yOPfG05x-e | psURZPKI-a3rVsU4wpmlO |
| 4 | AjEWliVaNE6MmgqxCgBou | qCLvQBxrVaT--83jk1DOV, psURZPKI-a3rVsU4wpmlO, O3SKlVKmjN6yOPfG05x-e |

## 작업 규모별 모드

| 사용자 요청 패턴 | 실행 모드 | 투입 에이전트 |
|----------------|----------|-------------|
| "전체 실행" | **전체 파이프라인** | content-planner, slide-writer, visual-designer, pptx-builder |
| "간단히" | **간단 실행** | content-planner |
| "리뷰만" | **리뷰만** | pptx-builder |

## 에이전트별 확장 스킬

| 스킬 | 경로 | 대상 에이전트 | 역할 |
|------|------|-------------|------|
| pptx-layout-patterns | pptx-layout-patterns/skill.md | AjEWliVaNE6MmgqxCgBou | python-pptx의 슬라이드 레이아웃, 텍스트박스 좌표계, 도형 스타일링, 이미지 삽입 등 실제 파일 생성에 필요한 API 사용 패턴과 예제 코드를 제공한다 |
| business-slide-structure | business-slide-structure/skill.md | qCLvQBxrVaT--83jk1DOV | 내부 보고, 프로젝트 현황, 업무 공유 등 목적별 슬라이드 구성 원칙과 청중 분석 프레임워크(SCQA, Pyramid Principle 등)를 제공한다 |

## 제약사항

- 이 스킬은 위 에이전트 팀의 협업 범위 내에서 동작한다
- 에이전트 정의에 명시되지 않은 외부 도구 실행이나 배포는 이 스킬의 범위가 아니다
- 산출물은 모두 `_workspace/` 디렉토리에 마크다운 형식으로 저장된다
