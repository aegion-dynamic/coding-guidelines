# Coding Guidelines for Frontend (Next.js & TypeScript)

### Technology Stack & Frameworks

*   **Core Framework**: The project is built with **Next.js 15** and **React 19**, utilizing the **App Router** for routing and layouts.
*   **Language**: **TypeScript** is used with `strict` mode enabled, ensuring type safety and code quality.
*   **UI Components**: You are using **Shadcn UI**, which is a collection of reusable and accessible components built on top of Radix UI and Tailwind CSS. This is evident from the numerous `@radix-ui/*` packages and the `components/ui` directory structure.
*   **Styling**: **Tailwind CSS** is used for styling, with `tailwind-merge` and `clsx` (via the `cn` utility) for managing conditional classes.
*   **Backend & Database**: **Supabase** is the chosen backend, with `@supabase/ssr` and `@supabase/supabase-js` used for server-side rendering and client-side interactions, respectively.
*   **Form Management**: **React Hook Form** (`react-hook-form`) is used for managing forms, coupled with **Zod** for schema validation.
*   **Code Quality**: **ESLint** (with Next.js core web vitals and TypeScript configurations) and **Prettier** are set up to enforce a consistent code style.

### Key Architectural Patterns

#### 1. Project Structure & Organization

*   **App Router and Route Groups**: The `app` directory uses **Route Groups** (`(auth)`, `(authenticated)`, `(public)`) to structure the application into sections with different layouts without affecting the URL. This is a best practice for managing distinct areas of an application (e.g., marketing pages, user dashboards, and authentication flows).
*   **Path Aliases**: The `tsconfig.json` file is configured with a path alias (`@/*`), allowing for cleaner, absolute-like imports (e.g., `import { Button } from '@/components/ui/button'`).
*   **Separation of Concerns**: The codebase is well-organized:
    *   `app/`: Routing, pages, and layouts.
    *   `components/`: Reusable React components. `components/ui` for Shadcn UI components and `components/app-layouts` for higher-level layouts.
    *   `lib/` & `utils/`: Utility functions and shared logic.
    *   `hooks/`: Custom React hooks.
    *   `app/actions/`: Server-side logic using Next.js Server Actions.

#### 2. Authentication and Authorization

*   **Supabase SSR**: The project correctly uses the `@supabase/ssr` library to handle authentication in a server-side rendering context. This is crucial for protecting routes and managing user sessions securely in Next.js.
*   **Client and Server Supabase Clients**: The code properly separates the Supabase client initialization for the server (`utils/supabase/server.ts`) and the client (`utils/supabase/client.ts`). This is the recommended pattern to ensure that server-side code uses service roles or secure user sessions, while client-side code uses the public, anonymous key.
*   **Middleware for Protected Routes**: The `middleware.ts` file is likely used to protect routes under the `(authenticated)` group, redirecting unauthenticated users to the login page.
*   **Server Actions for Auth**: The presence of `app/actions/auth.ts` suggests that user actions like login, logout, and registration are handled by **Next.js Server Actions**, which simplifies form submissions and mutations by co-locating server-side logic with components.

#### 3. Component Design

*   **Composable UI with Shadcn**: By using Shadcn UI, you follow a pattern of building a design system from composable and customizable primitives. Instead of importing a pre-styled library, components are owned by the application, making them easy to modify.
*   **Theming**: The application supports light and dark modes through `next-themes`, with a `mode-toggle.tsx` component to switch between them.

#### 4. Data Fetching & State Management

*   **Server Components for Data Fetching**: Given the use of the App Router, it's highly likely that data fetching for initial page loads is done in **React Server Components**, directly accessing the Supabase client on the server.
*   **Client Components for Interactivity**: Components requiring user interaction (`'use client'`) will handle client-side data fetching and state management, likely using `useState`, `useEffect`, or a lightweight client-side fetching library.
*   **Minimalist State Management**: For global state, the project likely relies on React Context (e.g., for the theme provider) rather than a heavy state management library like Redux or Zustand, which is a common pattern in modern Next.js applications that leverage Server Components.

### Best Practices and Guidelines

*   **Security**: The use of `@upstash/ratelimit` in `lib/ratelimit.ts` indicates that the application implements **rate limiting** for its API routes or Server Actions, which is a critical security best practice to prevent abuse.
*   **Infrastructure as Code**: The `supabase/config.toml` file suggests that the Supabase project configuration (and likely database migrations) is managed via the Supabase CLI. This is an excellent practice for versioning your database schema and ensuring consistency across different environments.
*   **Utility Functions**: The `lib/utils.ts` file, a common pattern with Shadcn UI, centralizes utility functions like the `cn` helper for Tailwind CSS class name composition.

In summary, this codebase represents a modern, robust, and maintainable frontend application. It follows the latest best practices from the Next.js and React ecosystems, with a strong emphasis on server-side rendering, type safety, and a well-organized, composable architecture.****