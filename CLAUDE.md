# CLAUDE.md - AI Assistant Guide

**Last Updated:** 2025-11-15
**Project:** claude-code
**Framework:** Next.js 16.0.3 (App Router) + React 19 + TypeScript 5

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Codebase Structure](#codebase-structure)
- [Technology Stack](#technology-stack)
- [Development Workflow](#development-workflow)
- [Code Conventions](#code-conventions)
- [Styling Guidelines](#styling-guidelines)
- [File Organization Patterns](#file-organization-patterns)
- [Common Tasks](#common-tasks)
- [Important Notes for AI Assistants](#important-notes-for-ai-assistants)

---

## 🎯 Project Overview

This is a modern Next.js 16 application using the App Router architecture. It's currently a starter template ready for feature development.

**Key Characteristics:**
- Server Components by default (Next.js App Router)
- TypeScript strict mode enabled
- Tailwind CSS v4 with dark mode support
- Optimized fonts (Geist Sans & Geist Mono)
- No existing API routes (ready to add)
- No existing component library (ready to build)

---

## 📁 Codebase Structure

```
/home/user/test/
├── .git/                          # Version control
├── .gitignore                     # Git ignore patterns
├── eslint.config.mjs              # ESLint flat config (v9)
├── next.config.ts                 # Next.js configuration
├── package.json                   # Dependencies & scripts
├── package-lock.json              # Locked dependencies
├── postcss.config.mjs             # PostCSS with Tailwind
├── tsconfig.json                  # TypeScript config
├── README.md                      # Project documentation
├── public/                        # Static assets (SVGs, images)
│   ├── file.svg
│   ├── globe.svg
│   ├── next.svg
│   ├── vercel.svg
│   └── window.svg
└── src/                           # Source code
    └── app/                       # Next.js App Router
        ├── favicon.ico            # Site favicon
        ├── globals.css            # Global styles + Tailwind
        ├── layout.tsx             # Root layout (required)
        └── page.tsx               # Home page (/)
```

### Expected Structure for New Features

When adding features, follow these conventions:

```
src/
├── app/                           # App Router pages & layouts
│   ├── api/                       # API route handlers (create as needed)
│   │   └── [endpoint]/
│   │       └── route.ts           # GET, POST, etc.
│   ├── (routes)/                  # Route groups (optional)
│   │   └── dashboard/
│   │       └── page.tsx
│   ├── layout.tsx                 # Root layout
│   ├── page.tsx                   # Home page
│   └── globals.css                # Global styles
├── components/                    # Reusable components (create as needed)
│   ├── ui/                        # Base UI components
│   └── features/                  # Feature-specific components
├── lib/                           # Utility functions (create as needed)
│   ├── utils.ts                   # General utilities
│   └── api.ts                     # API helpers
└── types/                         # TypeScript types (create as needed)
    └── index.ts
```

---

## 🛠 Technology Stack

### Core Framework
| Technology | Version | Purpose |
|------------|---------|---------|
| Next.js | 16.0.3 | React framework with App Router |
| React | 19.2.0 | UI library (latest) |
| TypeScript | 5.x | Type safety |

### Styling
| Technology | Version | Purpose |
|------------|---------|---------|
| Tailwind CSS | 4.x | Utility-first CSS (latest) |
| PostCSS | Latest | CSS processing |
| next/font | Built-in | Font optimization (Geist fonts) |

### Development Tools
| Tool | Version | Purpose |
|------|---------|---------|
| ESLint | 9.x | Code linting (flat config) |
| eslint-config-next | 16.0.3 | Next.js ESLint rules |

### Path Aliases
- `@/*` maps to `./src/*` (configured in tsconfig.json)

**Example usage:**
```typescript
import { Button } from '@/components/ui/button'
import { fetchData } from '@/lib/api'
```

---

## ⚙️ Development Workflow

### Setup
```bash
# Install dependencies
npm install

# Start development server
npm run dev
# → http://localhost:3000
```

### Available Scripts
```bash
npm run dev      # Development mode (hot reload)
npm run build    # Production build
npm run start    # Serve production build
npm run lint     # Run ESLint
```

### Development Process
1. **Start dev server**: `npm run dev`
2. **Make changes**: Edit files in `src/app/`
3. **Verify**: Check browser at http://localhost:3000
4. **Lint**: Run `npm run lint` before committing
5. **Build**: Run `npm run build` to verify production build

### Before Deployment
- [ ] Run `npm run lint` (must pass)
- [ ] Run `npm run build` (must succeed)
- [ ] Test production build with `npm start`
- [ ] Verify TypeScript types compile

---

## 📝 Code Conventions

### Component Structure

**Server Components (Default):**
```typescript
// src/app/dashboard/page.tsx
import type { Metadata } from 'next'

export const metadata: Metadata = {
  title: 'Dashboard',
  description: 'User dashboard',
}

export default async function DashboardPage() {
  // Can use async/await directly
  const data = await fetch('https://api.example.com/data')

  return (
    <div className="container mx-auto">
      <h1>Dashboard</h1>
    </div>
  )
}
```

**Client Components (Interactive):**
```typescript
// src/components/counter.tsx
'use client'

import { useState } from 'react'

export function Counter() {
  const [count, setCount] = useState(0)

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  )
}
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `UserProfile`, `DashboardLayout` |
| Files (React) | kebab-case or PascalCase | `user-profile.tsx` or `UserProfile.tsx` |
| Files (Next.js) | lowercase | `page.tsx`, `layout.tsx`, `route.ts` |
| Variables/Functions | camelCase | `userData`, `fetchUser()` |
| Types/Interfaces | PascalCase | `User`, `ApiResponse` |
| Constants | UPPER_SNAKE_CASE | `API_BASE_URL`, `MAX_RETRIES` |
| CSS Variables | kebab-case | `--font-geist-sans` |

### TypeScript Patterns

**Use type imports:**
```typescript
import type { Metadata } from 'next'
import type { ReactNode } from 'react'
```

**Readonly props pattern:**
```typescript
export default function Layout({
  children,
}: Readonly<{
  children: ReactNode
}>) {
  return <div>{children}</div>
}
```

**Strict typing:**
- Always define types for props
- Avoid `any` - use `unknown` if needed
- Use type inference when obvious
- Export types for shared interfaces

---

## 🎨 Styling Guidelines

### Tailwind CSS v4

**Current configuration** (in `globals.css`):
```css
@import "tailwindcss";

@theme inline {
  --font-geist-sans: "Geist Sans", sans-serif;
  --font-geist-mono: "Geist Mono", monospace;
}
```

**Usage patterns:**
```typescript
// ✅ Good: Utility-first approach
<div className="flex items-center justify-center min-h-screen p-8 sm:p-20">
  <button className="rounded-lg bg-blue-500 px-4 py-2 text-white hover:bg-blue-600 dark:bg-blue-600">
    Click me
  </button>
</div>

// ❌ Avoid: Inline styles (use Tailwind instead)
<div style={{ display: 'flex', padding: '8px' }}>
```

### Dark Mode

**System preference detection** (automatic):
```css
@media (prefers-color-scheme: dark) {
  :root {
    --background: #0a0a0a;
    --foreground: #ededed;
  }
}
```

**Tailwind dark mode classes:**
```typescript
<div className="bg-white dark:bg-gray-900 text-black dark:text-white">
  Content adapts to dark mode
</div>
```

### Responsive Design

**Tailwind breakpoints:**
```typescript
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
  {/* Mobile: 1 col, Tablet: 2 cols, Desktop: 4 cols */}
</div>
```

### Font Usage

**System fonts are already configured** in `layout.tsx`:
```typescript
import { Geist, Geist_Mono } from 'next/font/google'

const geistSans = Geist({
  variable: "--font-geist-sans",
  subsets: ["latin"],
})

const geistMono = Geist_Mono({
  variable: "--font-geist-mono",
  subsets: ["latin"],
})
```

**Use in components:**
```typescript
<p className="font-sans">Sans serif text</p>
<code className="font-mono">Monospace code</code>
```

---

## 📂 File Organization Patterns

### Creating New Pages

**File-system based routing** (Next.js App Router):

```typescript
// src/app/about/page.tsx
export default function AboutPage() {
  return <div>About page</div>
}
// → URL: /about

// src/app/blog/[slug]/page.tsx
export default function BlogPost({ params }: { params: { slug: string } }) {
  return <div>Post: {params.slug}</div>
}
// → URL: /blog/hello-world
```

### Creating API Routes

```typescript
// src/app/api/users/route.ts
import { NextResponse } from 'next/server'

export async function GET() {
  const users = await fetchUsers()
  return NextResponse.json(users)
}

export async function POST(request: Request) {
  const body = await request.json()
  const user = await createUser(body)
  return NextResponse.json(user, { status: 201 })
}
// → API: /api/users
```

### Creating Layouts

```typescript
// src/app/dashboard/layout.tsx
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <div className="dashboard">
      <nav>Dashboard Nav</nav>
      <main>{children}</main>
    </div>
  )
}
```

### Creating Components

**Recommended structure:**
```typescript
// src/components/ui/button.tsx
import type { ButtonHTMLAttributes } from 'react'

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary'
}

export function Button({ variant = 'primary', children, ...props }: ButtonProps) {
  return (
    <button
      className={`px-4 py-2 rounded ${
        variant === 'primary' ? 'bg-blue-500' : 'bg-gray-500'
      }`}
      {...props}
    >
      {children}
    </button>
  )
}
```

---

## 🔧 Common Tasks

### Adding a New Feature Page

1. Create page file: `src/app/[feature]/page.tsx`
2. Export default component
3. Add metadata export for SEO
4. Use Server Component (default) or Client Component (`'use client'`)

### Adding a Client Component

1. Create file: `src/components/[name].tsx`
2. Add `'use client'` directive at top
3. Use React hooks (useState, useEffect, etc.)
4. Import into page

### Adding an API Endpoint

1. Create file: `src/app/api/[endpoint]/route.ts`
2. Export named functions: `GET`, `POST`, `PUT`, `DELETE`
3. Use `NextResponse` for responses
4. Handle errors with try/catch

### Adding a Layout

1. Create `layout.tsx` in route folder
2. Accept `children` prop
3. Return JSX wrapping children
4. Layout applies to all pages in that folder

### Adding Environment Variables

1. Create `.env.local` file (already gitignored)
2. Add variables: `NEXT_PUBLIC_API_URL=...`
3. Use in code: `process.env.NEXT_PUBLIC_API_URL`
4. Restart dev server after changes

### Adding a Utility Function

1. Create file: `src/lib/[name].ts`
2. Export functions
3. Import with alias: `import { fn } from '@/lib/[name]'`

---

## ⚠️ Important Notes for AI Assistants

### What to Know

1. **App Router (NOT Pages Router)**
   - Use `src/app/` directory structure
   - Server Components by default
   - Client Components need `'use client'`
   - File-based routing with `page.tsx` and `layout.tsx`

2. **TypeScript Strict Mode**
   - All code must be properly typed
   - Use `type` imports when importing types
   - Avoid `any` type
   - Props must be typed

3. **Tailwind CSS v4**
   - No `tailwind.config.js` file (v4 uses CSS config)
   - Theme configured in `globals.css` with `@theme inline`
   - Use utility classes, avoid inline styles
   - Dark mode via `dark:` prefix

4. **ESLint Flat Config**
   - Using ESLint v9 flat config format
   - Run `npm run lint` before committing
   - Config in `eslint.config.mjs`

5. **Path Aliases**
   - Always use `@/` for imports from `src/`
   - Example: `import { Button } from '@/components/ui/button'`

### When Making Changes

- ✅ **DO:**
  - Create components in `src/components/` (not in `src/app/`)
  - Use Server Components when possible (faster, smaller bundle)
  - Use TypeScript types for all props and functions
  - Follow existing naming conventions
  - Use Tailwind classes for styling
  - Add metadata exports to pages for SEO
  - Test with `npm run build` before finalizing

- ❌ **DON'T:**
  - Create Pages Router files (no `pages/` directory)
  - Mix Client Components unnecessarily (keep Server Components when possible)
  - Use inline styles (use Tailwind instead)
  - Use `any` type in TypeScript
  - Create `tailwind.config.js` (Tailwind v4 doesn't need it)
  - Import without path aliases when importing from `src/`

### Server vs Client Components

**Use Server Components (default) when:**
- Fetching data
- Accessing backend resources
- Rendering static content
- No browser APIs needed
- No event handlers needed

**Use Client Components (`'use client'`) when:**
- Using React hooks (useState, useEffect, etc.)
- Using browser APIs (localStorage, window, etc.)
- Adding event listeners (onClick, onChange, etc.)
- Using React context

### Data Fetching Patterns

**Server Component (recommended):**
```typescript
export default async function Page() {
  // Direct fetch in Server Component
  const data = await fetch('https://api.example.com/data', {
    cache: 'no-store' // or 'force-cache' for static
  })
  const json = await data.json()

  return <div>{json.title}</div>
}
```

**Client Component (when needed):**
```typescript
'use client'

import { useEffect, useState } from 'react'

export function ClientData() {
  const [data, setData] = useState(null)

  useEffect(() => {
    fetch('/api/data')
      .then(r => r.json())
      .then(setData)
  }, [])

  return <div>{data?.title}</div>
}
```

### Performance Best Practices

1. **Use Server Components by default** (smaller bundle, faster)
2. **Optimize images**: Use `next/image` component
3. **Lazy load Client Components**: `const Component = dynamic(() => import('./component'))`
4. **Use metadata exports**: Better SEO
5. **Minimize client-side JavaScript**: Keep interactivity in small Client Components

---

## 🔄 Version History

| Date | Changes |
|------|---------|
| 2025-11-15 | Initial CLAUDE.md creation - documented Next.js 16 App Router structure |

---

## 📚 Additional Resources

- **Next.js Docs**: https://nextjs.org/docs
- **React Docs**: https://react.dev
- **Tailwind CSS v4**: https://tailwindcss.com/docs
- **TypeScript Handbook**: https://www.typescriptlang.org/docs

---

**For questions or updates to this guide, please maintain this file as the codebase evolves.**
