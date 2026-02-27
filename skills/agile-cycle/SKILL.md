---
name: agile-cycle
description: 애자일 개발 사이클을 실행합니다. User Story 하나를 선택하고, 전 역할을 빠르게 한 바퀴 돌린 뒤, 피드백을 반영하여 반복합니다. `/agile-cycle`로 실행합니다.
---

# Agile Development Cycle

User Story 하나 단위로 전체 역할을 빠르게 순환하고, 피드백을 반영하여 반복한다.

## Core Principle

**가장 작은 동작 가능한 조각을 빠르게 완성하고, 피드백을 받고, 반복한다.**

## Cycle

```
┌─────────────────────────────────────────────┐
│                                             │
│  ┌──────────┐                               │
│  │ Backlog  │ ← 피드백 반영, 다음 Story 선택  │
│  └────┬─────┘                               │
│       ▼                                     │
│  ┌──────────┐                               │
│  │ Sprint   │ Story 1개 선택                 │
│  │ Planning │                               │
│  └────┬─────┘                               │
│       ▼                                     │
│  ┌──────────────────────────────────┐       │
│  │ Sprint Execution (1 Story)       │       │
│  │                                  │       │
│  │  PO: Story 확정                  │       │
│  │   ↓                              │       │
│  │  UX: 해당 Story 플로우/상태       │       │
│  │   ↓                              │       │
│  │  Visual: 해당 화면 비주얼 스펙     │       │
│  │   ↓                              │       │
│  │  Architect: 해당 범위 기술 설계    │       │
│  │   ↓                              │       │
│  │  Dev: 구현 + 테스트               │       │
│  │   ↓                              │       │
│  │  Review: 코드 리뷰               │       │
│  └────┬─────────────────────────────┘       │
│       ▼                                     │
│  ┌──────────┐                               │
│  │ Demo &   │ 사용자에게 결과 보여주기        │
│  │ Feedback │                               │
│  └────┬─────┘                               │
│       ▼                                     │
│  ┌──────────┐                               │
│  │ Retro    │ 무엇을 개선할지 정리            │
│  └────┬─────┘                               │
│       │                                     │
│       └─────────────────────────────────────┘
│              다음 Story로 반복
```

## Process

### Step 0: Backlog 생성 (최초 1회)

PO 역할로 전체 기능을 Epic + User Stories로 분해한다.

```
You are a Startup Product Owner Agent.
```

- Epic 정의 (Goal, Business Value)
- User Stories 분해 (As a / I want / So that + Acceptance Criteria)
- 각 Story는 **1 Sprint(= 1 Cycle)에 완료 가능한 크기**
- Stories 우선순위 정렬 (MoSCoW 또는 Impact/Effort)
- 사용자에게 Backlog를 보여주고 우선순위 확인

**Output:**
| # | Story | Priority | Size (S/M/L) | Status |
|---|-------|----------|-------------|--------|

### Step 1: Sprint Planning

사용자와 함께 이번 Sprint에서 작업할 Story 1개(또는 2-3개 소규모)를 선택한다.

선택 기준:
- 가장 높은 우선순위
- 이전 Sprint 피드백 반영 Story
- 의존성이 해소된 Story

**Output:** 이번 Sprint의 Story 목록 + Definition of Done

### Step 2: Sprint Execution

선택된 Story에 대해 전 역할을 순차 실행한다. **해당 Story 범위만 다룬다.**

#### 2-1. PO: Story 확정
- Acceptance Criteria 최종 확인
- 불명확한 부분 질의
- 범위 벗어나는 것은 Backlog에 추가

#### 2-2. UX Designer: Story 플로우 설계
```
You are a UX Designer Agent.
```
- 해당 Story의 화면, 플로우, 상태, UX 카피만 설계
- 전체 시스템이 아니라 이 Story에 필요한 최소 범위

#### 2-3. Visual Designer: Story 비주얼 스펙
```
You are a Visual Designer Agent.
```
- 해당 화면의 토큰, 컴포넌트, 비주얼 상태만 정의
- 기존 디자인 시스템 재사용 우선

#### 2-4. Architect: Story 기술 설계
```
You are a Software Architect Agent.
```
- 해당 Story 구현에 필요한 범위만 설계
- 기존 아키텍처 확장이면 변경점만
- 새 모듈이 필요하면 최소 범위로

#### 2-5. Developer: 구현
```
You are a Frontend/Backend Developer Agent.
```
- 해당 Story 구현 + 테스트
- FE/BE 필요 시 Task tool로 병렬 실행
- Acceptance Criteria 충족 확인

#### 2-6. Code Reviewer: 리뷰
```
You are a Code Reviewer Agent.
```
- 스펙 대비 검증
- Approve → Step 3으로
- Request Changes → Step 2-5로 복귀

### Step 3: Demo & Feedback

완성된 Story를 사용자에게 보여주고 피드백을 수집한다.

```
---
## Sprint [N] Demo: [Story Name]

### 완성된 것
[구현된 기능 요약]

### 확인 요청
1. Acceptance Criteria 충족 여부
2. 기대와 다른 부분
3. 추가로 필요한 것
4. 우선순위 변경 사항

### Backlog 업데이트
- 새로 추가된 Story:
- 우선순위 변경:
- 제거된 Story:
---
```

### Step 4: Retrospective

짧은 회고를 수행한다.

```
---
## Sprint [N] Retro

### What went well
### What to improve
### Action items for next Sprint
---
```

### Step 5: 다음 Sprint

피드백을 Backlog에 반영하고 Step 1로 돌아간다.

Backlog 상태를 업데이트하여 보여준다:
| # | Story | Priority | Size | Status |
|---|-------|----------|------|--------|
| 1 | ... | ... | ... | Done (Sprint 1) |
| 2 | ... | ... | ... | ← Next |
| 3 | ... | ... | ... | Pending |

## Execution Rules

1. **Story 단위로만 작업** — 전체 기능을 한 번에 하지 않는다.
2. **각 역할은 해당 Story 범위만** — 전체 시스템 설계가 아니라 이 Story에 필요한 최소 범위.
3. **Sprint 내 승인 게이트 없음** — Story 단위로 빠르게 흐른다. 피드백은 Demo에서 한 번에.
4. **피드백은 Backlog로** — Demo에서 나온 변경사항은 새 Story로 Backlog에 추가한다. 현재 Sprint을 되돌리지 않는다.
5. **진행 추적** — Backlog를 task로 관리한다.
6. **Scope creep 방지** — Sprint 중 새로운 요청은 Backlog에 추가하고 다음 Sprint에서 처리한다.

## Comparison with full-cycle

| | `/full-cycle` (워터폴) | `/agile-cycle` (애자일) |
|---|---|---|
| 단위 | 기능 전체 | User Story 1개 |
| Phase 간 승인 | 매 Phase마다 | Sprint 끝 Demo에서 |
| 피드백 반영 | Code Review → Dev | Demo → Backlog → 다음 Sprint |
| 방향 전환 | 어려움 | 매 Sprint |
| 첫 결과물 | 6 Phase 후 | 첫 Sprint 후 |

## How to Start

사용자에게 어떤 기능을 만들 것인지 물어보세요.

1. Step 0 (Backlog 생성)부터 시작합니다.
2. Epic을 정의하고 User Stories로 분해합니다.
3. 우선순위를 확인한 후 첫 Sprint를 시작합니다.
