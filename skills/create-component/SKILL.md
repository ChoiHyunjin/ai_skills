---
name: create-component
description: React 컴포넌트를 프로젝트 컨벤션에 맞게 생성합니다. Simple, Responsive, Compound 세 가지 타입을 지원합니다.
metadata:
  author: apartmentary
  version: "1.0.0"
---

# Create Component

프로젝트 컨벤션에 맞는 React 컴포넌트 구조를 생성하는 스킬입니다.

## 사용법

```bash
/create-component <ComponentName> [options] [path]
```

### Options

| 옵션 | 설명 |
|------|------|
| (없음) | Simple 컴포넌트 |
| `--responsive` | Desktop/Mobile 분리 반응형 컴포넌트 |
| `--compound` | Compound Component 패턴 |

### Examples

```bash
/create-component MyButton
/create-component MyButton apps/pts/src/components
/create-component MenuModal --responsive
/create-component ItemRow --compound
```

---

## Instructions for Claude

When this skill is invoked, follow these steps:

### 1. Parse Arguments

- `ComponentName`: PascalCase 컴포넌트 이름 (필수)
- `--responsive`: Responsive 타입
- `--compound`: Compound 타입
- `path`: 생성 경로 (선택, 없으면 사용자에게 질문)

### 2. Ask for Path (if not provided)

경로가 제공되지 않은 경우 AskUserQuestion으로 질문:
- 어느 앱에 생성할지 (pts, admin, a-peach, spoke, survey)
- 구체적인 경로

### 3. Generate Files by Type

---

## Type 1: Simple (기본)

### 폴더 구조
```
ComponentName/
├── index.tsx
├── types.ts                       # Props가 있는 경우
├── constants.ts                   # (선택)
├── componentNameHelpers.ts        # (선택) 또는 helpers/ 디렉토리
└── hooks/                         # (선택)
    ├── index.ts
    └── useComponentName.ts
```

### index.tsx
```tsx
"use client";

import type { ComponentNameProps } from "./types";

export function ComponentName({ /* props */ }: ComponentNameProps) {
  return (
    <div>
      {/* TODO: Implement ComponentName */}
    </div>
  );
}

export default ComponentName;
```

### types.ts
```tsx
export interface ComponentNameProps {
  // TODO: Define props
}
```

---

## Type 2: Responsive (`--responsive`)

### 폴더 구조
```
ComponentName/
├── ComponentName.tsx              # Public API
├── _ComponentName.desktop.tsx      # 🔒 Desktop (internal)
├── _ComponentName.mobile.tsx       # 🔒 Mobile (internal)
├── types.ts
├── constants.ts                   # (선택)
├── componentNameHelpers.ts        # (선택) 또는 helpers/ 디렉토리
└── hooks/                         # (선택)
    ├── index.ts
    └── useComponentName.ts
```

### ComponentName.tsx (Public API)
```tsx
"use client";

import { useResponsiveComponent } from "@aptmtr/utils/hooks";

import { ComponentNameDesktop } from "./_ComponentName.desktop";
import { ComponentNameMobile } from "./_ComponentName.mobile";
import type { ComponentNameProps } from "./types";

export function ComponentName(props: ComponentNameProps) {
  const ResponsiveComponent = useResponsiveComponent(
    ComponentNameDesktop,
    ComponentNameMobile
  );

  if (!ResponsiveComponent) {
    return null;
  }

  return <ResponsiveComponent {...props} />;
}

export default ComponentName;
```

### _ComponentNameDesktop.tsx
```tsx
"use client";

import type { ComponentNameProps } from "./types";

export function ComponentNameDesktop({ /* props */ }: ComponentNameProps) {
  return (
    <div>
      {/* TODO: Implement Desktop version */}
    </div>
  );
}
```

### _ComponentNameMobile.tsx
```tsx
"use client";

import type { ComponentNameProps } from "./types";

export function ComponentNameMobile({ /* props */ }: ComponentNameProps) {
  return (
    <div>
      {/* TODO: Implement Mobile version */}
    </div>
  );
}
```

### types.ts
```tsx
export interface ComponentNameProps {
  // TODO: Define shared props
}
```

---

## Type 3: Compound (`--compound`)

### 폴더 구조
```
ComponentName/
├── index.tsx                      # Public API (compound export)
├── ComponentNameRoot.tsx          # Root 컴포넌트
├── _ComponentNameParts.tsx        # 🔒 서브 컴포넌트 모음
├── types.ts                       # 모든 타입 정의
├── context.ts                     # (선택) Context + hook
├── constants.ts                   # (선택)
├── componentNameHelpers.ts        # (선택) 또는 helpers/ 디렉토리
└── hooks/                         # (선택)
    ├── index.ts
    └── useComponentNameActions.ts
```

### index.tsx (Public API)
```tsx
"use client";

import { memo } from "react";

import {
  ComponentNameSubA,
  ComponentNameSubB,
} from "./_ComponentNameParts";
import { ComponentNameRoot } from "./ComponentNameRoot";

// ========== Export ==========

export const ComponentName = {
  Root: memo(ComponentNameRoot),
  SubA: memo(ComponentNameSubA),
  SubB: memo(ComponentNameSubB),
};

// Re-export types for external use
export type { ComponentNameRootProps } from "./types";
```

### ComponentNameRoot.tsx
```tsx
"use client";

import { useMemo } from "react";

import { ComponentNameContext } from "./context";
import type { ComponentNameContextValue, ComponentNameRootProps } from "./types";

export function ComponentNameRoot({ children, ...props }: ComponentNameRootProps) {
  // ========== Context 값 ==========
  const contextValue: ComponentNameContextValue = useMemo(
    () => ({
      // TODO: Define context values
    }),
    [/* dependencies */]
  );

  return (
    <ComponentNameContext.Provider value={contextValue}>
      <div>
        {children}
      </div>
    </ComponentNameContext.Provider>
  );
}
```

### _ComponentNameParts.tsx
```tsx
"use client";

import { useComponentNameContext } from "./context";

// ========== SubA ==========

export function ComponentNameSubA() {
  const { /* context values */ } = useComponentNameContext();

  return (
    <div>
      {/* TODO: Implement SubA */}
    </div>
  );
}

// ========== SubB ==========

export function ComponentNameSubB() {
  const { /* context values */ } = useComponentNameContext();

  return (
    <div>
      {/* TODO: Implement SubB */}
    </div>
  );
}
```

### context.ts (선택 - Context가 필요한 경우)
```tsx
"use client";

import { createContext, useContext } from "react";

import type { ComponentNameContextValue } from "./types";

// ========== Context ==========

export const ComponentNameContext = createContext<ComponentNameContextValue | null>(null);

export function useComponentNameContext() {
  const context = useContext(ComponentNameContext);
  if (!context) {
    throw new Error(
      "ComponentName 서브 컴포넌트는 ComponentName.Root 내부에서 사용해야 합니다."
    );
  }
  return context;
}
```

### types.ts
```tsx
import type { ReactNode } from "react";

// ========== Context 타입 ==========

export interface ComponentNameContextValue {
  // TODO: Define context values
}

// ========== Root Props ==========

export interface ComponentNameRootProps {
  children: ReactNode;
  // TODO: Define root props
}
```

### constants.ts (선택)
```tsx
// ========== 상수 ==========

/** 예시 상수 */
export const EXAMPLE_CONSTANT = "value";
```

### hooks/index.ts (선택)
```tsx
export { useComponentNameActions } from "./useComponentNameActions";
```

### hooks/useComponentNameActions.ts (선택)
```tsx
import { useCallback } from "react";

interface UseComponentNameActionsParams {
  // TODO: Define params
}

export function useComponentNameActions(params: UseComponentNameActionsParams) {
  // TODO: Implement actions

  return {
    // TODO: Return actions
  };
}
```

---

## 4. After Generation

1. 생성된 파일 목록을 사용자에게 보여주기
2. 다음 단계 안내:
   - Props 타입 정의
   - 컴포넌트 구현
   - 필요시 hooks, constants, helpers 추가

---

## Naming Conventions

| 항목 | 규칙 | 예시 |
|------|------|------|
| 컴포넌트 폴더 | PascalCase | `ItemRow/` |
| 컴포넌트 파일 | PascalCase | `ItemRowRoot.tsx` |
| 내부 파일 | `_` prefix | `_ItemRowParts.tsx` |
| 타입 파일 | lowercase | `types.ts` |
| 상수 파일 | lowercase | `constants.ts` |
| 컨텍스트 파일 | lowercase | `context.ts` |
| 훅 파일 | camelCase | `useItemRowActions.ts` |
| 헬퍼 파일 | camelCase | `itemRowHelpers.ts` |

## File Conventions

- `_` prefix 파일: 내부 전용, 외부에서 직접 import 금지
- `index.tsx`: Public API만 export
- `types.ts`: 모든 타입 정의 집중
- `context.ts`: Context + useContext hook 함께 정의

## Reference Examples

- **Compound**: `apps/pts/src/components/estimations/ItemRow/`
- **Responsive**: `apps/pts/src/app/(guard)/(form)/inbounds/[id]/estimations/[estimationId]/_components/menu-modal/`
