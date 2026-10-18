# nextjs-static-rules

A strict behavioral ruleset (`CLAUDE.md` / `.cursorrules`) to stop LLMs from ruining your static Next.js projects.

Tired of Claude or Cursor:
- Installing Supabase or Prisma when you just wanted a static site?
- Breaking layouts because it forgot image dimensions (CLS hell)?
- Causing Framer Motion hydration flash errors on page refresh?
- Throwing random modal pop-ups everywhere?
- Messing up mobile responsiveness and touching unrelated files?

This ruleset fixes that.

## Quick Start

Drop `CLAUDE.md` into your project root:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/ocalirdigital/nextjs-static-rules/main/CLAUDE.md
