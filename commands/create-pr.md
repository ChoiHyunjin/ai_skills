# create-pr 가이드 (개정안)

## 0. AI 동작 규칙 (Global Rule)

별도 언급이 없는 한, AI는 다음을 직접 실행합니다.

- git add
- git commit
- git push
- gh pr create

### JIRA 티켓이 없는 경우의 기본 규칙

Jira 티켓이 없는 작업은 다음 형식으로 커밋 / PR 제목을 생성할 수 있습니다.

{type}({scope}): 작업 요약

예시:
feat(a-peach): 견적 계산 API 응답 구조 개선  
refactor(admin): 중복 validation 유틸 정리

---

## 1. 개요

구조화된 PR을 빠르게 생성하고, 리뷰어가 핵심만 빠르게 파악할 수 있도록 하는 것이 목표입니다.  
PR 제목 규칙, 본문 작성 원칙, 리뷰 마감 기한, 생성 절차를 명확히 정의합니다.

---

## 2. PR 작성

### 2-0. 커밋 작성 (create-pr Command 연계)

PR을 만들기 전에, 가능한 한 의미 있는 커밋 단위로 변경사항을 정리합니다.  
create-pr Cursor Command는 아래 과정을 AI가 도와주도록 설계합니다.

#### 1) 변경 사항 확인

- 사용자가 git status -sb 결과를 제공하면, 해당 내용을 기준으로 AI가 분석합니다.
- 결과가 없다면, AI는 다음을 먼저 요청합니다.

git status -sb 실행 결과를 붙여 주세요.

---

#### 2) 커밋 단위 설계 (Commit Plan)

AI는 변경 파일을 기능/주제 단위로 분류하여 커밋 계획(commit plan)을 제안합니다.

각 커밋 단위마다 다음 정보를 제공합니다.

- 포함 파일 목록
- 권장 커밋 타입 (feat, fix, refactor, test 등)
- 권장 scope (a-peach, admin 등)
- 커밋 메시지 초안

예시:

[커밋 1]  
type: feat  
scope: a-peach  
메시지: feat(a-peach): [AP-1234] 견적 계산 API 응답 구조 변경  
포함 파일:
- apps/a-peach/api/...
- packages/domain/...

[커밋 2]  
type: refactor  
scope: a-peach  
메시지: refactor(a-peach): [AP-1234] validation 로직 리팩토링  
포함 파일:
- apps/a-peach/ui/...

---

#### 3) 커밋 메시지 규칙

기본 형식:

{type}({scope}): [{JIRA}] 작업 요약

Jira 티켓이 없는 경우:

{type}({scope}): 작업 요약

---

type: build, chore, ci, docs, feat, fix, perf, refactor, revert, style, test  
scope: 프로젝트 또는 패키지명 (a-peach, admin 등)  
JIRA: 없으면 생략 가능  
작업 요약: 한 줄 요약

---

#### 4) AI가 요청하는 최소 정보

- JIRA 티켓 번호 (없으면 생략)
- scope 정보

---

#### 5) 커밋 실행 방식

별도 지시가 없으면 AI는 다음을 자동 실행합니다.

- git add
- git commit
- git push

실행 로그는 그대로 출력합니다.

---

#### 6) 이미 PR이 생성된 경우 (추가 작업 플로우)

이미 PR이 생성된 상태라면:

1. 변경 분석
2. 동일 규칙으로 커밋 추가
3. push 실행

GitHub PR은 자동 업데이트됩니다.

---

### 2-1. PR 제목 규칙

기본:

{type}({scope}): [{JIRA}] 작업 요약

JIRA 없음:

{type}({scope}): 작업 요약

---

### 2-2. PR 본문 구성

#### 배경
- 변경 이유만 작성

#### 작업 내용
- 기능 단위 요약
- 커밋 로그 나열 금지

#### 리뷰 마감
PR 생성 후 48 Working Hours 이내

예:
2025.04.03 18:00

---

## 3. PR 설정

### 3-1. base 브랜치 자동 추정

git for-each-ref --format="%(refname:short)" refs/heads/ | while read branch; do
  CURRENT=$(git symbolic-ref --short HEAD)
  [ "$branch" = "$CURRENT" ] && continue
  BASE=$(git merge-base HEAD "$branch" 2>/dev/null) || continue
  COUNT=$(git rev-list --count "$BASE"..HEAD)
  echo "$COUNT $branch"
done | sort -n | cut -d' ' -f2 | head -n 1

---

### 3-2. 기타

- PR은 Draft
- Assignee는 본인

---

## 4. PR 생성

AI는 다음을 자동 실행합니다.

BASE_BRANCH=...
HEAD_BRANCH=...

gh pr create \
  --base "$BASE_BRANCH" \
  --head "$HEAD_BRANCH" \
  --draft \
  --assignee @me
