# ProofKit — Technical Feasibility Assessment

*Research date: 2026-04-01*

## Verdict: ✅ HIGHLY FEASIBLE

All core features can be built with existing, well-understood technology. No novel research required. The hardest part is UX, not engineering.

---

## Core Feature Breakdown

### 1. Testimonial Collection
**Difficulty: Low** ⭐

| Component | Technology | Complexity |
|-----------|-----------|------------|
| Collection form | React form + API | Trivial |
| Shareable link | Unique URL per client | Trivial |
| Video collection | Browser MediaRecorder API | Low-medium |
| Email import | Gmail/Outlook API or manual paste | Medium |
| Embeddable widget | iframe or Web Component | Low |

**Risk:** None. This is well-trodden ground (every competitor does this).

### 2. AI Asset Generation (The Differentiator)
**Difficulty: Medium** ⭐⭐⭐

| Asset Type | Approach | Quality Risk | Notes |
|-----------|----------|-------------|-------|
| **Case study** | LLM with structured prompt (testimonial + context questions) | Medium | Needs context beyond just the quote — project type, timeline, results. Collection form must gather this. |
| **LinkedIn post** | LLM with platform-specific formatting prompt | Low | Short-form, well-understood format. Multiple tone options (professional, casual, celebratory). |
| **Twitter/X post** | LLM with character limit constraint | Low | Simple transformation. Include hashtag suggestions. |
| **Portfolio card** | LLM for text + template for visual layout (HTML/CSS) | Low | Generate structured data, render with pre-designed templates. |
| **Email snippet** | LLM with email context prompt | Low | Short testimonial block for email signatures or drip campaigns. |
| **Landing page widget** | Structured data → embeddable component | Low | React component or vanilla JS widget. |

**Key technical insight:** The generation itself is easy (GPT-4o-mini or Claude Haiku handles all of these well). The **quality differentiator** is in the prompts, templates, and how we collect context alongside the testimonial.

**COGS per transformation:** ~$0.015-0.06 (5 assets × ~500 tokens each at current API pricing)

### 3. Template System
**Difficulty: Low-Medium** ⭐⭐

- Pre-built templates for each asset type × industry vertical
- Template customization (brand colors, fonts, logo)
- Template marketplace (future: user-created templates)
- Technology: React components + CSS variables for theming

### 4. Multi-Client Management (Agency Tier)
**Difficulty: Medium** ⭐⭐⭐

- Workspace isolation (multi-tenant)
- Team member access controls
- White-label output (remove ProofKit branding)
- Technology: Standard SaaS multi-tenancy patterns

### 5. Integrations
**Difficulty: Medium-High** ⭐⭐⭐⭐

| Integration | Approach | Priority |
|------------|----------|----------|
| Copy to clipboard | Browser API | MVP (P0) |
| Download as image | HTML → Canvas → PNG | MVP (P0) |
| LinkedIn share | LinkedIn Share API or URL scheme | P1 |
| Twitter/X share | Tweet intent URL | P1 |
| Buffer / Hootsuite | API integration | P2 |
| Mailchimp / ConvertKit | Email template API | P2 |
| Zapier | Zapier app or webhook triggers | P2 |
| Notion / Airtable | API integration | P3 |

**MVP needs only copy-to-clipboard and download-as-image.** Everything else is growth-phase.

---

## Proposed Tech Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| **Frontend** | Next.js 14+ (App Router) | SEO-friendly, fast, our standard stack |
| **Styling** | Tailwind CSS | Rapid UI development |
| **Backend** | Next.js API Routes + Supabase | Serverless, scales to zero |
| **Database** | Supabase (PostgreSQL) | Free tier, auth built-in, realtime |
| **Auth** | Supabase Auth (or Clerk) | Social login, magic link |
| **AI** | OpenAI API (GPT-4o-mini) | Cheapest quality-per-dollar for short-form generation |
| **Payments** | Stripe | Industry standard |
| **Hosting** | Vercel | Free tier, our standard |
| **Email** | Resend | Transactional emails, free tier |
| **Analytics** | PostHog | Our standard, free tier |

**Total infrastructure cost at launch: $0** (all free tiers)
**At 500 users: ~$50-100/mo** (Supabase Pro + Vercel Pro + API costs)

---

## Architecture Overview

```
┌─────────────────────────────────┐
│         User Dashboard          │
│  (Next.js App Router + Tailwind)│
└──────────────┬──────────────────┘
               │
┌──────────────▼──────────────────┐
│         API Layer               │
│  (Next.js API Routes)           │
│  - /api/testimonials            │
│  - /api/generate                │
│  - /api/templates               │
│  - /api/workspaces              │
└──────────────┬──────────────────┘
               │
    ┌──────────┼──────────┐
    │          │          │
┌───▼───┐ ┌───▼───┐ ┌───▼───┐
│Supabase│ │OpenAI │ │Stripe │
│  (DB)  │ │ (AI)  │ │(Pay)  │
└────────┘ └───────┘ └───────┘
```

### Data Model (Simplified)

```
users
  - id, email, name, plan, created_at

workspaces (multi-tenant for agencies)
  - id, owner_id, name, branding (JSON)

testimonials
  - id, workspace_id, client_name, client_title, client_company
  - quote_text, project_type, project_outcome, rating
  - video_url (optional), collected_at

generated_assets
  - id, testimonial_id, asset_type (case_study|linkedin|twitter|portfolio|email|widget)
  - content (JSON), template_id, generated_at
  - share_count, download_count

templates
  - id, asset_type, name, category, config (JSON)
```

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| AI output quality inconsistent | Medium | High | Structured prompts, human review option, template constraints |
| LLM API costs spike | Low | Low | GPT-4o-mini is cheap; can switch to open-source models |
| Competitor copies feature quickly | Medium | Medium | Speed to market, superior UX, template library depth |
| Low free-to-paid conversion | Medium | High | Tight free tier limits, clear upgrade value |
| Video processing complexity | Medium | Low | Defer video to post-MVP; text-first |

---

## MVP Scope (4-Week Build)

### Week 1: Foundation
- [ ] Next.js project setup with Supabase auth
- [ ] Basic testimonial collection form (text only)
- [ ] Shareable collection link
- [ ] Database schema + CRUD

### Week 2: AI Generation
- [ ] OpenAI integration for 3 asset types (case study, LinkedIn, Twitter)
- [ ] Prompt engineering + quality testing
- [ ] Asset preview + copy-to-clipboard
- [ ] Download as image (portfolio card)

### Week 3: Dashboard + Polish
- [ ] User dashboard (testimonials list, generated assets)
- [ ] Template selection (2-3 per asset type)
- [ ] Brand customization (colors, logo)
- [ ] Landing page

### Week 4: Payment + Launch Prep
- [ ] Stripe integration (Free/Pro/Agency tiers)
- [ ] Usage limits enforcement
- [ ] ProductHunt submission prep
- [ ] SEO basics (meta tags, OG images)

**Total effort: ~120-160 hours of coding agent time** (very achievable with sprint-loop skill)

---

## Conclusion

ProofKit is a **straightforward engineering project** with no novel technical challenges. The differentiation is in:
1. **Prompt quality** — how well we transform testimonials into each asset type
2. **Template design** — visual quality of generated assets
3. **Collection UX** — gathering enough context alongside the testimonial to generate quality assets
4. **Speed** — first to market with this specific value prop

**Recommendation: Proceed to prototyping immediately.**

---
*Last updated: 2026-04-01*
