# AGENTS.md

## Project Overview

NestJS API for an e-commerce application. **This is a learning project for NestJS** - explain concepts and patterns, don't just implement.

## Repository Structure

```
/Users/kanit/Desktop/play3/nest-next-ecommerce/
├── api/                    # NestJS application (all code lives here)
│   ├── src/               # Application source
│   ├── prisma/            # Database schema & migrations
│   ├── test/              # E2E tests
│   └── dist/              # Build output (auto-deleted on rebuild)
```

## Tech Stack

- **Framework**: NestJS 11.x with Express
- **Language**: TypeScript 5.x (ES2023 target)
- **Database**: PostgreSQL + Prisma 7.x ORM
- **Testing**: Jest with ts-jest
- **Module System**: ES Modules (`"type": "module"` in package.json)

## Essential Commands

All commands run from `api/` directory:

```bash
# Development
npm run start:dev          # Watch mode with hot reload

# Database (Prisma)
npx prisma migrate dev     # Create and apply migrations
npx prisma generate        # Regenerate Prisma Client
npx prisma studio          # Open Prisma Studio (DB GUI)

# Testing
npm run test               # Unit tests (*.spec.ts)
npm run test:watch         # Unit tests in watch mode
npm run test:e2e           # E2E tests (*.e2e-spec.ts)

# Code Quality
npm run lint               # ESLint with auto-fix
npm run format             # Prettier formatting
```

## Key Configuration

### TypeScript Module Resolution
- Uses `nodenext` module resolution (not Node10)
- Import paths must include `.js` extensions for relative imports
- TypeScript enforces ES module semantics strictly

### Prisma Setup
- Schema: `prisma/schema.prisma`
- Config: `prisma.config.ts` (Prisma 7 format)
- Client uses `@prisma/adapter-pg` for PostgreSQL
- Env var: `DATABASE_URL` (defined in `.env`)

### Testing Setup
- Unit tests: Jest config in `package.json`, tests in `src/**/*.spec.ts`
- E2E tests: Config in `test/jest-e2e.json`, tests in `test/**/*.e2e-spec.ts`
- No separate test database configured (runs against same DB)

## Domain Models (Prisma Schema)

E-commerce domain with:
- **User** → Orders, Reviews, CartItems
- **Product** → Category, OrderItems, Reviews, CartItems
- **Order** → OrderItems, User
- **Category** → Products
- **Review** → User, Product
- **CartItem** → User, Product

Enums: `Role` (CUSTOMER/ADMIN), `OrderStatus` (PENDING → PROCESSING → SHIPPED → DELIVERED/CANCELLED)

## Important Notes

1. **Prisma src folder is empty** - No Prisma service module exists yet. Need to create `PrismaService` extending `PrismaClient` and `PrismaModule` for dependency injection.

2. **ESM constraints** - All imports must use full paths with extensions where required by `nodenext` resolution.

3. **No authentication implemented** - User model exists but no JWT/auth guards yet.

4. **Database URL** - Points to external PostgreSQL instance (not localhost). Check `.env` before running migrations.

5. **Lint/Format order**: Run `npm run format` before `npm run lint` - Prettier and ESLint rules can conflict.

## Learning Focus

When implementing features:
- Explain NestJS patterns: Modules, Controllers, Services, Dependency Injection
- Show Prisma integration patterns with NestJS
- Demonstrate testing approaches (unit vs E2E)
- Discuss when to use Guards, Pipes, Interceptors, and Middleware
