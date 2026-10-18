# Strict Static Next.js Constraints

## CONFIG
- TARGET_LANGUAGE: "en" <!-- Change to "tr", "de", "es", "ja", etc. -->
- DB_POLICY: "forbidden"
- POPUP_POLICY: "forbidden"

## 1. Language & Localization
- All user-facing UI text, buttons, alerts, form placeholders, and metadata MUST strictly match TARGET_LANGUAGE.
- Set the root HTML `lang` attribute dynamically to match TARGET_LANGUAGE.

## 2. Zero CLS & Asset Optimization
- No unconstrained `<img>` or Next.js `<Image />` tags allowed.
- Every Next.js Image component MUST provide explicit `width`/`height` or use an aspect-ratio container (`fill` + `relative`).
- Cumulative Layout Shift (CLS) must be strictly 0. Always provide placeholder skeletons or layout dimensions.

## 3. Hydration & SSR Safety
- Prevent F5 refresh flickering caused by client animations (Framer Motion) or browser APIs (`window`, `localStorage`).
- Never render client-only state conditionally during initial SSR pass. Always use proper mount guards or dynamic imports with `{ ssr: false }`.

## 4. Zero-Database Architecture (Static Vercel Deploy)
- Strictly 100% static & client-side. DO NOT introduce Supabase, Firebase, Prisma, or any remote database.
- Must compile cleanly for static export (`output: 'export'`) or static Vercel deployment.
- Dynamic data (blogs, testimonials, FAQs) must reside in local, type-safe JSON or TS mock files.

## 5. No-Modal Policy
- NEVER implement modal dialogues, pop-ups, or screen overlays.
- All detail views, alert messages, and forms must exist inline or navigate to a dedicated sub-page.

## 6. Routing & Dynamic Pages
- Footer must provide dedicated clean legal routes matching the TARGET_LANGUAGE:
  - English: `/privacy`, `/terms`, `/cookie-policy`
  - Turkish: `/gizlilik`, `/kullanim-kosullari`, `/cerez-politikasi`
- Blog/news cards must route to dynamic static pages (`/blog/[slug]`) configured with `generateStaticParams`.

## 7. Mobile Viewports & Responsiveness
- Mobile-first layout design. Prevent horizontal scrolling (`overflow-x-hidden` safety on main layout).
- Minimum interactive touch target size: 44x44px.
- Pixel-perfect across `sm`, `md`, `lg`, and `xl` breakpoints.

## 8. Client-Side Security Hardening
- Do not use `dangerouslySetInnerHTML` unless explicitly sanitized.
- Outbound external links must always include `rel="noopener noreferrer"`.
- Sanitize and validate all client form inputs against basic XSS vectors before state processing.
