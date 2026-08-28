# Rules: Your Stack (React 19 + Vite + Supabase)

## Stack
- React 19.2.8, Vite 8.2.1, TypeScript 7.0.2
- Tailwind CSS 4.3.3 + shadcn/ui
- @supabase/supabase-js 2.112.3
- react-router-dom 7.18.2
- lucide-react 1.32.0
- date-fns 4.4.0

## Coding Style
- Functional components ONLY. No class components.
- Use shadcn/ui components. Do NOT build custom UI from scratch.
- Supabase calls go in /lib/supabase/ files. NEVER in components directly.
- All API calls must handle loading/error states.
- Use lucide-react for icons. Do not install other icon libraries.
- Use date-fns for all date formatting. No moment.js.

## Routing
- Use react-router-dom v7 with createBrowserRouter.
- Lazy load all route components with React.lazy() and Suspense.

## Supabase
- Never expose SUPABASE_SECRET_KEY in frontend code.
- Always validate user input before Supabase queries.
- Use RLS (Row Level Security) on all tables.
- Use supabase.auth for authentication. Do not build custom auth.

## Testing
- Use Vitest + React Testing Library.
- Test user behavior, not implementation details.
- Use MSW for mocking Supabase API calls in tests.