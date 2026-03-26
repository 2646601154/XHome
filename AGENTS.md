# AGENTS.md

## Project Overview

A personal homepage site ("ruoxin-home") built with Vue 3 + TypeScript + Vite. Package manager: **pnpm**.

## Build / Dev Commands

| Command | Description |
|---------|-------------|
| `pnpm dev` | Start Vite dev server |
| `pnpm build` | Production build (runs type-check + vite build in parallel) |
| `pnpm build-only` | Production build without type-check |
| `pnpm preview` | Preview production build locally |
| `pnpm type-check` | Run Vue TypeScript type checking via `vue-tsc --build` |

### Testing

No test framework is configured yet. The `tsconfig.node.json` references Vitest/Cypress/Playwright paths, suggesting future intent. If tests are added, Vitest is the natural fit for unit tests in this Vite project.

### Linting / Formatting

No ESLint, Prettier, or Stylelint configuration exists. No lint/format scripts in `package.json`. When adding lint tools, follow Vue ecosystem defaults: `@antfu/eslint-config` or `@vue/eslint-config` + Prettier.

## Code Style Guidelines

### Vue Components

- Use `<script setup lang="ts">` (Composition API, no Options API)
- Use `ref()`, `computed()`, `watch()` from Vue 3 — avoid `setup()` function syntax
- Component filenames: `index.vue` inside kebab-case directories (e.g., `home/index.vue`)
- Always use `scoped` styles unless intentionally styling globally
- Style lang: SCSS (`<style lang="scss" scoped>`)

```vue
<script setup lang="ts">
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <div class="example">{{ count }}</div>
</template>

<style lang="scss" scoped>
.example {
  color: #333;
}
</style>
```

### Imports

- Use the `@/` path alias (maps to `./src/`) for imports within `src/`
- Example: `import MyComponent from '@/components/my-component/index.vue'`
- Group imports (blank line between groups):
  1. Vue core (`vue`, `vue-router`, `pinia`)
  2. Third-party libraries
  3. Local components (`@/components/...`)
  4. Utilities / composables (`@/utils/...`, `@/composables/...`)
  5. Types (`@/types/...`)

### Props, Emits, and Slots

- Define props with `defineProps<{}>()` using TypeScript interface
- Define emits with `defineEmits<{}>()` typed
- Avoid using the runtime props/emits declaration; prefer the type-only syntax

```vue
<script setup lang="ts">
interface Props {
  title: string
  count?: number
}
const props = withDefaults(defineProps<Props>(), {
  count: 0,
})
const emit = defineEmits<{
  'update:title': [value: string]
}>()
</script>
```

### Naming Conventions

- **Directories**: kebab-case (`home/`, `my-avatar/`)
- **Components**: `index.vue` inside a named directory
- **Variables/functions**: camelCase (`showEmailModal`, `copyEmail`)
- **TypeScript types/interfaces**: PascalCase (`UserConfig`, `RouteMeta`)
- **SCSS classes**: kebab-case or BEM-lite

### TypeScript

- `tsconfig.app.json` enables `noUncheckedIndexedAccess` — always guard array/object access
- Prefer `interface` over `type` for object shapes
- Use explicit return types on exported functions
- Path alias `@/*` → `./src/*` is configured in `tsconfig.app.json`
- Avoid `any`; use `unknown` and narrow with type guards if needed
- Use optional chaining (`?.`) and nullish coalescing (`??`) consistently

### Reactive Data Patterns

- Use `ref()` for primitives, `reactive()` for objects when destructuring is not needed
- Prefer `ref()` when passing reactive state to composables or child components
- Use `computed()` for derived state; avoid computed with side effects
- Use `watch()` with `{ immediate: true }` only when initial sync is required

### Router & State Management

- Vue Router 5 (`vue-router`) for routing; Pinia 3 for state
- Define routes in a dedicated router file, keep components stateless where possible
- Use Pinia stores for shared state across components
- Access route params via `useRoute()` composable inside `<script setup>`

### SCSS

- Use SCSS nesting for scoped styles (max 3 levels deep)
- Use CSS custom properties (`var(--color-bg)`) for theming values
- Responsive: prefer `@media` queries within component styles
- Keep style rules colocated with their component; avoid global stylesheets unless for resets

### Error Handling

- No specific error handling patterns established. Use standard Vue error handling (`onErrorCaptured`) and try/catch for async operations.

## Directory Structure

```
├── src/
│   ├── App.vue              # Root component
│   ├── main.ts              # App entry point
│   ├── components/          # Shared components (empty, add here)
│   ├── view/                # Page-level views (empty, add here)
│   ├── home/                # Home page component
│   └── avatar/              # Static assets (images)
├── public/                  # Static assets served as-is
├── vite.config.ts           # Vite configuration
├── tsconfig.json            # Root TS config (references app + node)
├── tsconfig.app.json        # App TS config (includes src/**)
└── tsconfig.node.json       # Node TS config (build tools)
```

## Environment

- Node.js v24.14.0
- pnpm 10.32.1
- Vite 7.x, Vue 3.5, TypeScript 5.9

## Cursor / Copilot Rules

No `.cursorrules`, `.cursor/rules/`, or `.github/copilot-instructions.md` files exist.

## PR / Commit Guidelines

No formal commit conventions enforced. When committing, use descriptive messages. Run `pnpm type-check` before committing to catch type errors.
