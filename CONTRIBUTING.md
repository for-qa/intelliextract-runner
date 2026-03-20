# Contributing to IntelliExtract Runner

Thank you for your interest! This is a public portfolio project — contributions that improve architecture, documentation, or test coverage are welcome.

---

## 🚀 Getting Started

### Prerequisites
- **Node.js** 20+
- **npm** 9+

### Setup

```bash
git clone https://github.com/for-qa/intelliextract-runner.git
cd intelliextract-runner
npm ci
```

### Environment & Config

```bash
cp .env.example .env                        # fill in your credentials
cp config/config.example.yaml config/config.yaml  # fill in your config
```

See `.env.example` for all required environment variables. Secrets can be provided as plain text or Fernet-encrypted.

---

## 🧪 Running Tests

```bash
npm test              # Run all Vitest unit tests
npm run test:watch    # Watch mode
npm run test:coverage # Coverage report
```

Unit tests require **no credentials** and run with zero network/disk I/O.

---

## 🏗️ Building

```bash
npm run build      # Compile TypeScript → dist/
npm run typecheck  # Type check without emitting files
```

---

## ✅ Before Submitting a PR

```bash
npm run typecheck   # Must pass
npm test            # All unit tests must pass
npm run build       # Must compile cleanly
```

---

## 🗂️ Project Structure

```
src/
  core/
    domain/       # Entities, repository interfaces, use-case interfaces
    use-cases/    # Pure business logic — no infrastructure imports
  adapters/
    controllers/  # HTTP request handlers
    presenters/   # UI data formatters
    router.ts     # Zero-dependency HTTP router
  infrastructure/
    database/     # SQLite repository implementations
    services/     # AWS S3, Nodemailer, Fernet, Cron, Config…
    utils/        # Metrics, path normalization, stdout parsing
    views/        # Server-rendered HTML templates
assets/
  js/             # Client-side dashboard scripts
  css/            # Dashboard styles
tests/            # Vitest unit tests
config/           # YAML config (config.example.yaml is the template)
```

---

## 🎯 Architecture Principles

This project follows **Clean Architecture**:

- **`core/domain/`** — zero infrastructure imports; only TypeScript primitives and interfaces
- **`core/use-cases/`** — depend only on domain interfaces; never on concrete implementations
- **`infrastructure/`** — only layer that imports AWS SDK, SQLite, Nodemailer, etc.
- **`adapters/`** — HTTP boundary; maps requests to use-case calls and formats responses

---

## 📝 Pull Request Guidelines

- **One feature/fix per PR**
- **Add unit tests** for new pure-logic code
- **Follow Clean Architecture boundaries** — don't import infrastructure from use-cases
- **Clear PR description** — explain what and why

---

## 📄 License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).
