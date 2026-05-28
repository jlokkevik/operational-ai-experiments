# HytteHub

## Overview

HytteHub is a lightweight web application for coordinating access to shared cabins. It helps a small group see cabin availability, create bookings, manage cabin-specific information, and keep operational checklists in one place.

This document is written as a public-facing project summary for portfolio and employer review. It intentionally avoids secrets, tokens, credentials, private URLs, IP addresses, environment values, production data, and sensitive infrastructure details.

The app was initially built with Lovable and then connected to GitHub for source control. AI-assisted development was used throughout the project: Lovable helped with rapid product scaffolding and UI iteration, while GitHub/Codex-style review workflows supported follow-up improvements, documentation, refactoring, testing, and security-aware review.

## Product Concept

The product goal is to make shared cabin usage easier to coordinate without introducing a heavy enterprise system. The core user needs are:

- **Availability:** see which cabins are available and which bookings are upcoming.
- **Booking:** reserve a cabin for a date range with relevant trip details.
- **Operations:** maintain inventories, cabin notes, and checklists.
- **Access control:** separate regular member access from administrative capabilities.
- **Calendar integration:** expose user-scoped booking data through a revocable calendar feed.
- **Mobile-friendly usage:** support quick access from a phone, including progressive web app behavior.

The app is intentionally pragmatic: it favors clear workflows, minimal ceremony, and small iterative improvements over a large up-front platform design.

## High-Level Architecture

HytteHub is a React single-page application backed by Supabase services.

```text
Browser / PWA
  |
  | React + TypeScript UI
  | Vite build pipeline
  | TanStack Query data fetching
  v
Supabase client SDK
  |
  | Auth, database queries, RPC calls
  v
Supabase backend
  |
  | PostgreSQL schema, row-level access patterns, edge functions
  v
Calendar feed / operational integrations
```

Key architectural pieces:

- **Frontend:** React, TypeScript, Vite, Tailwind, and shadcn-style UI components.
- **Routing:** route guards protect authenticated, organization-scoped, admin, and platform-admin areas.
- **State and data fetching:** React context handles authentication and active organization state; TanStack Query is used for server data caching and loading states.
- **Backend:** Supabase provides authentication, database access, typed client integration, RPC-based permission checks, and Deno edge functions.
- **PWA support:** Vite PWA configuration provides installable app behavior and a conservative caching strategy.
- **Automation:** GitHub Dependabot is configured for dependency updates, with an auto-merge workflow for minor and patch updates from Dependabot.

## My Role

My role covered end-to-end product development and iteration:

- translated a real coordination problem into a focused lightweight app concept;
- used Lovable to quickly scaffold and iterate on the first usable version;
- connected the project to GitHub for versioned source control and review;
- used Codex-style AI assistance to inspect code, propose changes, review security-sensitive flows, and document implementation decisions;
- refined authentication, role-aware routing, booking flows, calendar feed behavior, and admin-oriented workflows;
- maintained operational documentation and release-oriented checklists; and
- kept public documentation free from credentials, private endpoints, real user data, and sensitive database details.

## Development Workflow

The project uses a lightweight branch-and-review workflow suitable for a small product:

1. **Define a narrow change**
   - Example: improve role checks, add calendar-feed safeguards, or document a release checklist.
2. **Prototype with AI assistance**
   - Lovable is useful for UI-first iteration and product flow exploration.
   - Codex-style review is useful for codebase-aware implementation, refactoring, and documentation.
3. **Review the generated change**
   - Check whether the implementation matches the product intent.
   - Remove overly broad changes and avoid leaking sensitive values into code or docs.
4. **Run local quality checks**
   - Typical commands are `npm run lint`, `npm run test`, and `npm run build`.
5. **Commit and open a pull request**
   - Keep commits small enough to review.
   - Use the PR description to explain user impact, implementation notes, and test coverage.
6. **Release deliberately**
   - Prefer a short release checklist covering authentication, booking, admin access, and regression-prone areas.

A simplified release checklist:

```text
- Confirm the app starts locally.
- Run linting and tests.
- Build the production bundle.
- Manually verify login, cabin list, booking creation, admin access, and sign-out.
- Review docs for accidental secrets or private data before publishing.
```

## Example Implementation Snippets

The following snippets are simplified examples based on project patterns. They are intentionally shortened and do not include secrets, real tokens, private URLs, or sensitive data.

### Route protection

```tsx
function ProtectedRoute({ children }: { children: React.ReactNode }) {
  const { user, loading, isDeactivated, hasOrgAccess } = useAuth();

  if (loading) return <Spinner />;
  if (!user) return <Navigate to="/auth" replace />;
  if (isDeactivated || !hasOrgAccess) return <NoAccessPage />;

  return <>{children}</>;
}
```

This pattern keeps access decisions close to routing and makes protected product areas easier to reason about.

### Role hierarchy helper

```ts
const ORG_ROLE_HIERARCHY = ["member", "admin", "owner"] as const;

type OrgRole = (typeof ORG_ROLE_HIERARCHY)[number];

function hasOrgRoleAtLeast(role: OrgRole, minimumRole: OrgRole): boolean {
  return ORG_ROLE_HIERARCHY.indexOf(role) >= ORG_ROLE_HIERARCHY.indexOf(minimumRole);
}
```

A small hierarchy helper keeps permission checks readable and reduces repeated conditional logic in UI components.

### Calendar event escaping

```ts
function escapeCalendarText(value: string): string {
  return value
    .replace(/\\/g, "\\\\")
    .replace(/;/g, "\\;")
    .replace(/,/g, "\\,")
    .replace(/\n/g, "\\n");
}
```

Calendar output must escape special characters so user-entered booking text does not break the generated feed.

### Environment-based client setup

```ts
const backendUrl = import.meta.env.VITE_BACKEND_URL;
const publicClientKey = import.meta.env.VITE_PUBLIC_CLIENT_KEY;

export const client = createClient(backendUrl, publicClientKey);
```

The important rule is that configuration names may appear in code, but real values do not belong in public documentation, commits, screenshots, or pull request descriptions.

## Security and Access Control Considerations

Security considerations were treated as part of normal iteration rather than an afterthought:

- **No public secrets:** public documentation uses placeholders and architectural descriptions only.
- **Scoped routing:** protected pages require authentication; admin pages require elevated organization or platform capability.
- **Role-aware UI:** administrative affordances are shown only to users with the relevant role-derived capability.
- **Backend validation:** sensitive operations should not rely solely on UI checks; backend policies and RPC checks remain the enforcement layer.
- **Calendar-feed safety:** feed URLs are treated as sensitive bearer links, generated deliberately, and designed to be revocable.
- **Token handling:** implementation patterns prefer hashing or non-reversible storage for sensitive token material where applicable.
- **Dependency hygiene:** Dependabot is configured to surface dependency updates and reduce drift.
- **Documentation hygiene:** docs avoid production identifiers, private user information, private infrastructure details, and `.env` values.

## Product Decisions

Notable product and technical decisions:

- **Use Lovable for speed:** the first product iterations emphasized fast feedback on real workflows instead of hand-building every UI detail from scratch.
- **Use GitHub for control:** moving the app into GitHub created a durable review history and made it easier to audit AI-generated changes.
- **Use Supabase for a small-team backend:** authentication, database access, and edge functions provided enough backend capability without maintaining a custom server.
- **Keep the UI mobile-first:** cabin coordination often happens while traveling or planning informally, so phone usability matters.
- **Keep roles explicit:** even a small app benefits from clear member/admin/owner/platform distinctions.
- **Document operationally:** README-style checklists and public documentation make the project easier to maintain and explain.

## Key Learnings

- AI tools are most valuable when paired with clear product intent, small changes, and human review.
- Lightweight products still need disciplined access control, release habits, and documentation hygiene.
- Route guards and UI permissions improve usability, but backend policies remain essential for actual authorization.
- Public portfolio documentation should explain decisions and tradeoffs without revealing deployment details or user data.
- A simple workflow built around GitHub, tests, linting, and small PRs is enough to support steady iteration on a small app.

## Screenshots

Screenshots can be added for portfolio use after they have been reviewed for privacy. Recommended screenshots:

- login or welcome screen with demo-only data;
- cabin overview with placeholder names/images;
- booking dialog using non-real dates and names;
- admin checklist or inventory view with sample content; and
- mobile/PWA view showing responsive behavior.

Before publishing screenshots, verify that they do not show real names, private booking dates, tokens, internal URLs, browser bookmarks, account emails, or infrastructure identifiers.
