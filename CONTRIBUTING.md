# Contributing

Thank you for your interest in contributing! This document explains the process for proposing changes, reporting bugs, and getting your work merged.

---

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [How to Contribute](#how-to-contribute)
3. [Development Setup](#development-setup)
4. [Branching Strategy](#branching-strategy)
5. [Commit Messages](#commit-messages)
6. [Pull Request Process](#pull-request-process)
7. [Reporting Bugs](#reporting-bugs)
8. [Suggesting Features](#suggesting-features)

---

## Code of Conduct

All contributors are expected to be respectful and constructive. Harassment, discrimination, or personal attacks of any kind will not be tolerated. By participating you agree to uphold a welcoming environment for everyone.

---

## How to Contribute

1. **Fork** the repository and clone your fork locally.
2. **Create a branch** from `main` (see [Branching Strategy](#branching-strategy)).
3. Make your changes following the guidelines below.
4. **Test** your changes thoroughly.
5. Open a **Pull Request** targeting `main`.

---

## Development Setup

### Prerequisites

| Tool | Version |
|------|---------|
| Python | ≥ 3.11 |
| Node.js | ≥ 18 LTS |
| Flutter | ≥ 3.x |
| PostgreSQL | ≥ 15 |
| Redis | ≥ 7 |

### Backend (Django)

```bash
# Clone and enter directory
git clone https://github.com/NHRICH/NHRICH.git
cd NHRICH

# Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env
# Edit .env with your local settings

# Apply migrations and start the dev server
python manage.py migrate
python manage.py runserver
```

### Frontend (Next.js)

```bash
cd frontend
npm install
cp .env.local.example .env.local
npm run dev
```

### Mobile (Flutter)

```bash
cd mobile
flutter pub get
flutter run
```

---

## Branching Strategy

| Branch pattern | Purpose |
|----------------|---------|
| `main` | Production-ready code |
| `feature/<name>` | New features |
| `fix/<name>` | Bug fixes |
| `chore/<name>` | Maintenance (deps, configs) |
| `docs/<name>` | Documentation only |

Branch names should be lowercase and use hyphens, e.g. `feature/payment-webhooks`.

---

## Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<scope>): <short description>

[optional body]

[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

**Examples:**

```
feat(payments): add Chapa webhook signature verification
fix(auth): prevent token reuse after logout
docs(architecture): add sequence diagram for payment flow
```

---

## Pull Request Process

1. Ensure your branch is up-to-date with `main` before opening a PR.
2. Fill in the PR template completely.
3. Link any related issues using `Closes #<issue-number>`.
4. Ensure all CI checks pass before requesting a review.
5. At least one maintainer approval is required before merging.
6. Squash or rebase commits when asked by a reviewer.

---

## Reporting Bugs

Open a [GitHub Issue](https://github.com/NHRICH/NHRICH/issues) and include:

- A clear, descriptive title
- Steps to reproduce
- Expected vs. actual behaviour
- Environment details (OS, browser/device, versions)
- Screenshots or logs if applicable

> **Security issues must NOT be reported as public issues.**  
> See [SECURITY.md](SECURITY.md) for the responsible disclosure process.

---

## Suggesting Features

Open a [GitHub Issue](https://github.com/NHRICH/NHRICH/issues) labelled `enhancement` and describe:

- The problem you are trying to solve
- Your proposed solution or feature
- Any alternatives you have considered
- Why this would benefit the project

---

## Questions?

Reach out via [nahom.tech/contact](https://nahom.tech/contact) or open a [Discussion](https://github.com/NHRICH/NHRICH/discussions).
