---
name: service-deep-research
description: "'[서비스명] 시장을 심층 분석해줘', '[서비스명]의 경쟁사와 소비자 트렌드를 리서치해줘', '[서비스명] 비즈니스 모델과 시장 환경을 조사해줘', '[서비스명] 서비스에 대한 종합 리서치 보고서를 작성해줘', '[서비스명] 산업 동향과 경쟁 구도를 분석해줘'"
---

# service-deep-research — 서비스 심층 리서치

특정 서비스나 제품에 대해 다각도로 심층 조사를 수행하는 하네스입니다. 시장 현황, 경쟁사 분석, 사용자 리뷰, 기술 스택, 비즈니스 모델 등 다양한 관점에서 정보를 수집하고 분석합니다. 최종적으로 구조화된 리서치 보고서를 생성하여 의사결정에 필요한 인사이트를 제공합니다.

## 에이전트 구성

| 에이전트 | 파일 | 역할 | 타입 |
|---------|------|------|------|
| TCV4MYGm4A7wXXuVcgVeB | `.claude/agents/TCV4MYGm4A7wXXuVcgVeB.md` | 서비스 대상 산업의 시장 현황과 구조를 분석한다 | general-purpose |
| j7-7W8HIcGaay0nrOoO9m | `.claude/agents/j7-7W8HIcGaay0nrOoO9m.md` | 경쟁 서비스를 다각도로 비교 분석한다 | general-purpose |
| geV61oHljb7VKG8cn7nVB | `.claude/agents/geV61oHljb7VKG8cn7nVB.md` | 서비스 사용자의 리뷰와 니즈를 분석한다 | general-purpose |
| FFf_uG1p5qNLpusMem0c7 | `.claude/agents/FFf_uG1p5qNLpusMem0c7.md` | 서비스의 비즈니스 모델과 수익 구조를 분석한다 | general-purpose |
| qaTW86n21zYZU9wyGbxBR | `.claude/agents/qaTW86n21zYZU9wyGbxBR.md` | 전체 리서치 결과를 검증하고 최종 통합 보고서를 생성한다 | general-purpose |

## 실행 준비 (오케스트레이터 수행)

1. 사용자 입력에서 핵심 요구사항을 추출한다
2. `_workspace/` 디렉토리를 프로젝트 루트에 생성한다
3. 입력을 정리하여 `_workspace/00_input.md`에 저장한다
4. 요청 범위에 따라 실행 모드를 결정한다 (아래 "작업 규모별 모드" 참조)

## 워크플로우

### Phase 1

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| TCV4MYGm4A7wXXuVcgVeB | 서비스 대상 산업의 시장 현황과 구조를 분석한다 | 없음 | `_workspace/01_industry-analyst_output.md` |

### Phase 2

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| j7-7W8HIcGaay0nrOoO9m | 경쟁 서비스를 다각도로 비교 분석한다 | TCV4MYGm4A7wXXuVcgVeB | `_workspace/02_competitor-analyst_output.md` |
| geV61oHljb7VKG8cn7nVB | 서비스 사용자의 리뷰와 니즈를 분석한다 | TCV4MYGm4A7wXXuVcgVeB | `_workspace/03_consumer-analyst_output.md` |

### Phase 3

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| FFf_uG1p5qNLpusMem0c7 | 서비스의 비즈니스 모델과 수익 구조를 분석한다 | j7-7W8HIcGaay0nrOoO9m, geV61oHljb7VKG8cn7nVB | `_workspace/04_business-modeler_output.md` |

### Phase 4

| 담당 | 역할 | 의존 | 산출물 |
|------|------|------|--------|
| qaTW86n21zYZU9wyGbxBR | 전체 리서치 결과를 검증하고 최종 통합 보고서를 생성한다 | TCV4MYGm4A7wXXuVcgVeB, j7-7W8HIcGaay0nrOoO9m, geV61oHljb7VKG8cn7nVB, FFf_uG1p5qNLpusMem0c7 | `_workspace/05_research-reviewer_output.md` |

## 에이전트 간 통신 프로토콜

- 에이전트 간 SendMessage를 통해 직접 통신하며 작업 결과를 교차 검증한다
- 각 에이전트는 작업 완료 후 산출물을 `_workspace/` 디렉토리에 저장한다
- 후속 에이전트는 선행 에이전트의 산출물을 읽어 작업을 이어간다

## 순서 (요약)

| 순서 | 담당 | 의존 |
|------|------|------|
| 1 | TCV4MYGm4A7wXXuVcgVeB | 없음 |
| 2 | j7-7W8HIcGaay0nrOoO9m | TCV4MYGm4A7wXXuVcgVeB |
| 3 | geV61oHljb7VKG8cn7nVB | TCV4MYGm4A7wXXuVcgVeB |
| 4 | FFf_uG1p5qNLpusMem0c7 | j7-7W8HIcGaay0nrOoO9m, geV61oHljb7VKG8cn7nVB |
| 5 | qaTW86n21zYZU9wyGbxBR | TCV4MYGm4A7wXXuVcgVeB, j7-7W8HIcGaay0nrOoO9m, geV61oHljb7VKG8cn7nVB, FFf_uG1p5qNLpusMem0c7 |

## 작업 규모별 모드

| 사용자 요청 패턴 | 실행 모드 | 투입 에이전트 |
|----------------|----------|-------------|
| "전체 실행" | **전체 파이프라인** | industry-analyst, competitor-analyst, consumer-analyst, business-modeler, research-reviewer |
| "간단히" | **간단 실행** | industry-analyst |
| "리뷰만" | **리뷰만** | research-reviewer |

## 에이전트별 확장 스킬

| 스킬 | 경로 | 대상 에이전트 | 역할 |
|------|------|-------------|------|
| market-sizing-methodology | market-sizing-methodology/skill.md | TCV4MYGm4A7wXXuVcgVeB | TAM/SAM/SOM 산출 방법론과 시장 규모 추정 프레임워크를 적용하여 정량적 시장 분석을 수행한다 |
| competitive-framework | competitive-framework/skill.md | j7-7W8HIcGaay0nrOoO9m | Porter's Five Forces, SWOT, 포지셔닝 맵 등 경쟁 분석 프레임워크를 활용하여 경쟁 구도를 구조화한다 |
| business-model-canvas | business-model-canvas/skill.md | FFf_uG1p5qNLpusMem0c7 | Business Model Canvas와 수익 모델 유형 분류 체계를 기반으로 서비스의 가치 창출 및 수익 구조를 체계적으로 분해한다 |

## 제약사항

- 이 스킬은 위 에이전트 팀의 협업 범위 내에서 동작한다
- 에이전트 정의에 명시되지 않은 외부 도구 실행이나 배포는 이 스킬의 범위가 아니다
- 산출물은 모두 `_workspace/` 디렉토리에 마크다운 형식으로 저장된다
