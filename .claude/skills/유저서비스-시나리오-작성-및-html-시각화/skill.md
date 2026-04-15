---
name: user-scenario-html-visualizer
description: "'서비스 사용 시나리오를 작성하고 HTML로 시각화해줘', '유저 플로우를 분석해서 웹 페이지로 보여줘', '우리 서비스의 사용자 여정을 시나리오로 정리하고 화면으로 만들어줘', '신규 기능에 대한 사용 시나리오와 인터랙티브 프로토타입이 필요해', '고객 경험 흐름을 시나리오로 문서화하고 HTML 대시보드로 출력해줘'"
---

# user-scenario-html-visualizer — 유저/서비스 시나리오 작성 및 HTML 시각화

사용자 또는 서비스의 요구사항을 입력받아 구체적인 사용 시나리오를 자동으로 작성합니다. 작성된 시나리오를 기반으로 흐름도, 다이어그램, 스토리보드 등을 HTML 형태로 시각화하여 직관적으로 확인할 수 있게 제공합니다. 기획자, 디자이너, 개발자가 시나리오를 빠르게 공유하고 검토할 수 있도록 완성된 HTML 파일을 최종 산출물로 출력합니다.

## 에이전트 구성

| 에이전트 | 파일 | 역할 | 타입 |
|---------|------|------|------|
| h5a-dsyugF_HcvLyvmHU4 | `.claude/agents/h5a-dsyugF_HcvLyvmHU4.md` | 요구사항을 분석하여 구조화된 사용 시나리오를 작성 | general-purpose |
| 1Lx6dIe02ua4L5b6DxNJb | `.claude/agents/1Lx6dIe02ua4L5b6DxNJb.md` | 시나리오를 기반으로 흐름도와 다이어그램 데이터를 설계 | general-purpose |
| JThywScxn-Y5wq9pV-bBy | `.claude/agents/JThywScxn-Y5wq9pV-bBy.md` | 프론트엔드 개발자 | general-purpose |
| l9NjPTjTr6Z9sHOkKvvZW | `.claude/agents/l9NjPTjTr6Z9sHOkKvvZW.md` | 시나리오 완결성 검토 및 HTML 파일 품질 검증 | general-purpose |

## 실행 준비 (오케스트레이터 수행)

1. 사용자 입력에서 핵심 요구사항을 추출한다
2. `_workspace/` 디렉토리를 프로젝트 루트에 생성한다
3. 입력을 정리하여 `_workspace/00_input.md`에 저장한다
4. 요청 범위에 따라 실행 모드를 결정한다 (아래 "작업 규모별 모드" 참조)

## 워크플로우

### Phase 1

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| h5a-dsyugF_HcvLyvmHU4 | 요구사항을 분석하여 구조화된 사용 시나리오를 작성 | 없음 | `_workspace/01_scenario-analyst_output.md` |

### Phase 2

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| 1Lx6dIe02ua4L5b6DxNJb | 시나리오를 기반으로 흐름도와 다이어그램 데이터를 설계 | h5a-dsyugF_HcvLyvmHU4 | `_workspace/02_flow-designer_output.md` |

### Phase 3

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| JThywScxn-Y5wq9pV-bBy | 프론트엔드 개발자 | 1Lx6dIe02ua4L5b6DxNJb | `_workspace/03_frontend-dev_output.md` |

### Phase 4

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| l9NjPTjTr6Z9sHOkKvvZW | 시나리오 완결성 검토 및 HTML 파일 품질 검증 | JThywScxn-Y5wq9pV-bBy | `_workspace/04_qa-engineer_output.md` |

## 에이전트 간 통신 프로토콜

- 에이전트 간 SendMessage를 통해 직접 통신하며 작업 결과를 교차 검증한다
- 각 에이전트는 작업 완료 후 산출물을 `_workspace/` 디렉토리에 저장한다
- 후속 에이전트는 선행 에이전트의 산출물을 읽어 작업을 이어간다

## 순서 (요약)

| 순서 | 담당 | 의존 |
|------|------|------|
| 1 | h5a-dsyugF_HcvLyvmHU4 | 없음 |
| 2 | 1Lx6dIe02ua4L5b6DxNJb | h5a-dsyugF_HcvLyvmHU4 |
| 3 | JThywScxn-Y5wq9pV-bBy | 1Lx6dIe02ua4L5b6DxNJb |
| 4 | l9NjPTjTr6Z9sHOkKvvZW | JThywScxn-Y5wq9pV-bBy |

## 작업 규모별 모드

| 사용자 요청 패턴 | 실행 모드 | 투입 에이전트 |
|----------------|----------|-------------|
| "전체 실행" | **전체 파이프라인** | scenario-analyst, flow-designer, frontend-dev, qa-engineer |
| "간단히" | **간단 실행** | scenario-analyst |
| "리뷰만" | **리뷰만** | qa-engineer |

## 에이전트별 확장 스킬

| 스킬 | 경로 | 대상 에이전트 | 역할 |
|------|------|-------------|------|
| ux-scenario-patterns | ux-scenario-patterns/skill.md | h5a-dsyugF_HcvLyvmHU4 | 페르소나 기반 시나리오, 엣지 케이스, 예외 흐름 등 UX 시나리오 작성 패턴과 구조화 방법론 지식 |
| diagram-syntax-library | diagram-syntax-library/skill.md | 1Lx6dIe02ua4L5b6DxNJb | Flowchart, Swimlane, Sequence Diagram 등 주요 다이어그램 표기법과 HTML/SVG 변환 규칙 지식 |

## 제약사항

- 이 스킬은 위 에이전트 팀의 협업 범위 내에서 동작한다
- 에이전트 정의에 명시되지 않은 외부 도구 실행이나 배포는 이 스킬의 범위가 아니다
- 산출물은 모두 `_workspace/` 디렉토리에 마크다운 형식으로 저장된다
