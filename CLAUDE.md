# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Core Development
- `npm run dev` - Start development server with turbopack, auto-starts PGlite database server
- `npm run build` - Build for production with memory database
- `npm run start` - Start production server
- `npm run clean` - Clean build artifacts and coverage files

### Code Quality
- `npm run lint` - Run ESLint
- `npm run lint:fix` - Fix ESLint issues automatically
- `npm run check:types` - TypeScript type checking
- `npm run check:deps` - Check for unused dependencies (Knip)
- `npm run check:i18n` - Validate translations

### Testing
- `npm test` - Run unit tests (Vitest)
- `npm run test:e2e` - Run E2E tests (Playwright, requires `npx playwright install` first)
- `npm run storybook` - Start Storybook dev server
- `npm run storybook:test` - Run Storybook tests

### Database
- `npm run db:generate` - Generate database migrations from schema changes
- `npm run db:studio` - Open Drizzle Studio at https://local.drizzle.studio
- `npm run db-server:file` - Start PGlite server with file persistence
- `npm run db-server:memory` - Start PGlite server in memory mode

## Architecture Overview

This is a Next.js 15+ boilerplate with App Router using TypeScript, featuring a comprehensive modern development stack.

### Tech Stack
- **Framework**: Next.js 15 with App Router and Turbopack
- **Authentication**: Clerk (supports social auth, MFA, passwordless)
- **Database**: PostgreSQL with DrizzleORM, PGlite for local development
- **UI**: Tailwind CSS 4, React 19
- **Testing**: Vitest, Playwright, Storybook
- **Security**: Arcjet (bot protection, WAF), Sentry (error monitoring)
- **Internationalization**: next-intl with Crowdin integration

### Key Directories
- `src/app/[locale]` - Internationalized App Router pages
- `src/components/` - React components
- `src/libs/` - Third-party library configurations (DB, Auth, I18n, etc.)
- `src/models/Schema.ts` - Database schema definitions
- `src/middleware.ts` - Next.js middleware with Arcjet security and Clerk auth
- `migrations/` - Database migration files
- `tests/` - Test files (e2e/ and integration/)

### Authentication Structure
- Protected routes: `/dashboard/*` (requires authentication)
- Auth pages: `/sign-in/*`, `/sign-up/*`
- Public routes: marketing pages, API routes

### Database Management
- Schema changes: Edit `src/models/Schema.ts`, then run `npm run db:generate`
- Migrations auto-apply on database connection
- Local development uses PGlite (SQLite-compatible PostgreSQL)
- Production ready for any PostgreSQL provider

### Internationalization
- Default locales: English (en), French (fr)
- Update `src/utils/AppConfig.ts` for locale configuration
- Translation files in `src/locales/`
- Crowdin integration for automated translations

### Security Features
- Arcjet middleware for bot detection and WAF protection
- Environment variable validation with T3 Env
- Sentry error monitoring with Spotlight for local development

### Development Workflow
1. Run `npm run dev` to start with hot reload and database
2. Database schema changes require `npm run db:generate`
3. Use `npm run commit` for conventional commit messages
4. Run quality checks before committing: lint, types, tests
