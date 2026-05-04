# UNIZIK Institutional Website & CMS Platform

## Project Overview

Official redesign and redevelopment of the Nnamdi Azikiwe University (UNIZIK) institutional website and content management platform. The project delivers a unified digital presence across one main university domain and six faculty subdomains, backed by a centralized media server and a dual‑surface CMS that enforces role‑based content ownership.

The platform replaces the existing static HTML prototype with a production‑ready, multi‑tenant PHP/MySQL system, modernising the user experience while preserving the established design language and component library.

## Objectives

- **Modernise UX/UI** – Deliver a responsive, accessible, and visually cohesive experience across all devices, based on the existing design system (light/dark themes, reveal animations, typography tokens).
- **Multi‑tenant faculty structure** – Operate six independent faculty subsites (`arts`, `engineering`, `health`, `law`, `management`, `sciences`) from a single codebase, each with its own subdomain and brand identity.
- **Scoped CMS for decentralised content control** – Provide two distinct admin surfaces: a Main CMS for university‑wide content (news, events, leadership, admissions) and a Faculty CMS for faculty‑scoped content (departments, programmes, staff, faculty news/events). Role‑based permissions enforce strict tenant isolation.
- **Accessibility compliance** – Meet WCAG 2.1 AA standards, including semantic HTML, keyboard navigation, and screen‑reader support.
- **Performance optimisation** – Achieve <3 second load times on standard Nigerian 4G connections, with Lighthouse performance scores ≥80 on all primary pages.

## Tech Stack (Surface)

- **Backend:** PHP 8.x (no frameworks – MVC‑lite)
- **Database:** MySQL 8.0
- **Frontend:** Vanilla HTML5 / CSS3 / JavaScript (ES6+)
- **Media Storage:** S3‑compatible object storage (AWS S3, Cloudflare R2, or self‑hosted MinIO)
- **Image Processing:** PHP GD or ImageMagick
- **Authentication:** PHP sessions + bcrypt
- **Web Server:** Apache 2.4+ / Nginx

## Project Phases

- **Discovery & Audit** – Inventory of existing assets (HTML templates, JavaScript data objects, placeholders); extract reusable components; define migration scope.
- **Architecture Design** – Multi‑tenant routing, tenant detection, database schema, URL structure, subdomain strategy, and media object storage schema.
- **Core CMS Development** – User authentication, role/permission system, Main CMS (news, events, faculties, departments, programmes, staff, media library), shared includes, and base templates.
- **Faculty Subdomain Rollout** – Faculty CMS (scoped CRUD for news, events, staff, programmes, research), faculty‑specific theming, department/programme content editing, and cross‑domain aggregation (main site feeds).
- **QA & Performance** – Cross‑browser testing, mobile validation, Lighthouse auditing, security review, and content isolation testing.
- **Deployment** – Virtual host configuration, wildcard SSL installation, DNS setup for 7 PHP domains + `media.unizik.edu.ng`, production `.env` configuration, seed data upload, and technical handover.

## Contribution Guidelines

### Branch Naming Conventions

All branches must follow one of these patterns:

- `feature/short-description` – for new features (e.g. `feature/faculty-news-approval`)
- `fix/short-description` – for bug fixes (e.g. `fix/media-url-variant-suffix`)
- `docs/short-description` – for documentation updates only
- `refactor/short-description` – for code changes that do not alter behaviour

Use lowercase, hyphen‑separated words. Keep the description under 50 characters.

### PR Review Policy

- **Minimum reviewers:** 1 (project lead or senior developer)
- **Review checklist:**
  - No hard‑coded environment credentials
  - All database queries use prepared statements (no string interpolation)
  - Every user‑supplied output is escaped (`htmlspecialchars()`)
  - Media uploads go through `MediaService` (no direct S3 client usage)
  - Faculty‑scoped models include `faculty_id` in WHERE clauses
  - All new pages include proper meta tags and canonical URLs
- **Merge requirements:** passing automated checks (if any) + at least one approval + no unresolved conversations
- **Rebase policy:** squash merge into `main` – keep commit history clean

### Issue Template

When opening a new issue, please use the following markdown template:

```markdown
## Summary
(One‑sentence description)

## Type
[ ] Bug
[ ] Feature
[ ] Task (non‑functional change)
[ ] Documentation

## Tenant Scope
[ ] Main domain only
[ ] Faculty subdomains (specify which)
[ ] Both
[ ] Media subdomain (S3 / object storage)

## Current Behaviour / Missing Feature
(Describe what happens now, or what is not yet implemented)

## Expected Behaviour / Acceptance Criteria
(Concrete, testable bullet points)

## Steps to Reproduce (if bug)
1. …
2. …

## Environment (if relevant)
- PHP version:
- MySQL version:
- Browser:

## Screenshots / Mockups (optional)
(Attach or link)

## Additional Context
(Logs, related PRD sections, open questions)