# ProofKit — Financial Model

*Created: 2026-04-01*

## Pricing Tiers

| Tier | Price | Features | Target |
|------|-------|----------|--------|
| **Free** | $0/mo | 3 testimonials, 2 asset types (text widget + 1 social post), ProofKit branding | Try-before-you-buy, freelancers starting out |
| **Pro** | $15/mo ($144/yr annual) | Unlimited testimonials, all 5 asset types, custom branding, email support | Active freelancers, solopreneurs |
| **Agency** | $39/mo ($384/yr annual) | Everything in Pro + multi-client workspaces, team members, white-label, priority support | Agencies, studios, consultancies |

**Annual discount:** ~20% (industry standard)

**Rationale:** Market clusters at $15-20/mo for pro tiers. $15/mo undercuts Senja ($20/mo) and Famewall ($19/mo) while matching Testimly's growth tier. The Agency tier at $39/mo is standard for multi-client SaaS.

---

## Revenue Model (24-Month Projection)

### Assumptions
- Free-to-Pro conversion: 6%
- Pro-to-Agency upsell: 10% of Pro users within 6 months
- Monthly churn (Pro): 5% (high for new product, improves over time)
- Monthly churn (Agency): 3%
- Organic signup growth: 15% MoM months 1-6, 10% MoM months 7-12, 8% MoM months 13-24

### Month-by-Month (Year 1)

| Month | New Free | Total Free | New Pro | Total Pro | New Agency | Total Agency | MRR |
|-------|----------|-----------|---------|-----------|-----------|-------------|-----|
| 1 (PH launch) | 500 | 500 | 30 | 30 | 0 | 0 | $450 |
| 2 | 100 | 570 | 6 | 34 | 0 | 0 | $510 |
| 3 | 115 | 647 | 7 | 39 | 2 | 2 | $663 |
| 4 | 132 | 735 | 8 | 45 | 2 | 4 | $831 |
| 5 | 152 | 836 | 9 | 51 | 3 | 7 | $1,038 |
| 6 | 175 | 952 | 11 | 59 | 3 | 10 | $1,275 |
| 7 | 192 | 1,080 | 12 | 67 | 4 | 13 | $1,512 |
| 8 | 211 | 1,218 | 13 | 75 | 4 | 17 | $1,788 |
| 9 | 232 | 1,370 | 14 | 84 | 5 | 21 | $2,079 |
| 10 | 255 | 1,536 | 15 | 94 | 5 | 25 | $2,385 |
| 11 | 281 | 1,719 | 17 | 105 | 6 | 30 | $2,745 |
| 12 | 309 | 1,920 | 19 | 117 | 7 | 36 | $3,159 |

**Year 1 Total Revenue: ~$18,400**
**Month 12 MRR: ~$3,159**
**Year 1 ARR (run-rate): ~$37,900**

### Year 2 Summary
- Month 24 MRR target: $8,000-12,000
- Year 2 total revenue: ~$70,000-100,000
- Year 2 ARR (run-rate): $96,000-144,000

---

## Cost Structure

### Fixed Costs (Monthly)

| Item | Cost | Notes |
|------|------|-------|
| Vercel hosting | $0-20 | Free tier → Pro when needed |
| Database (Supabase/PlanetScale) | $0-25 | Free tier initially |
| Domain | ~$1 | Annual, amortized |
| Email (Resend/Postmark) | $0-20 | Free tier initially |
| **Total fixed** | **$0-66/mo** | Nearly zero at launch |

### Variable Costs (Per Testimonial Transformation)

| Item | Cost per transformation | Notes |
|------|------------------------|-------|
| LLM API (GPT-4o-mini or Claude Haiku) | $0.005-0.02 | 5 assets × ~500 tokens each |
| Image generation (if visual cards) | $0.01-0.04 | Optional, OG images/cards |
| **Total per transformation** | **$0.015-0.06** | Average: ~$0.03 |

### Monthly COGS at Scale

| Users | Transformations/mo | LLM Cost | Gross Margin |
|-------|-------------------|----------|-------------|
| 100 Pro | ~500 | $15 | 99% |
| 500 Pro | ~2,500 | $75 | 99% |
| 1,000 Pro | ~5,000 | $150 | 98% |
| 5,000 Pro | ~25,000 | $750 | 97% |

**LLM costs are negligible.** Even at 5,000 paying users, API costs are <3% of revenue. This is a high-margin business.

---

## Break-Even Analysis

### Scenario: Solo Founder (Matt + AI Agents)

| Expense | Monthly |
|---------|---------|
| Infrastructure | $50 |
| Domain/email | $5 |
| LLM API | $20 (initial) |
| **Total** | **$75/mo** |

**Break-even: 5 Pro users** ($75 ÷ $15/mo = 5 users)

At our projected Month 1 (30 Pro users from PH launch), we'd be **cash-flow positive from day one**.

### Scenario: With Marketing Spend

| Expense | Monthly |
|---------|---------|
| Infrastructure | $50 |
| Content marketing tools | $50 |
| Social ads (Month 6+) | $200 |
| LLM API | $50 |
| **Total** | **$350/mo** |

**Break-even: 24 Pro users** ($350 ÷ $15 ≈ 24)

Still achievable by Month 2.

---

## Key Metrics to Track

| Metric | Target | Why It Matters |
|--------|--------|---------------|
| Free signups/mo | 200+ by month 3 | Top of funnel health |
| Free→Pro conversion | >5% | Revenue engine |
| Pro monthly churn | <5% | LTV protection |
| ARPU | >$17 | Agency upsell working |
| Transformations/user/mo | >5 | Engagement / stickiness |
| Time-to-first-asset | <60 seconds | Aha moment speed |
| NPS | >50 | Product-market fit indicator |

---

## Revenue Milestones

| Milestone | Target Date | Metric |
|-----------|------------|--------|
| First paying user | Month 1 | $15 MRR |
| $1K MRR | Month 5 | ~67 Pro users |
| $3K MRR | Month 12 | ~150 Pro + Agency mix |
| $10K MRR | Month 18-24 | ~500 paying users |
| Ramen profitability ($5K MRR) | Month 15 | Covers modest salary |

---

## Investment Required

**Total to launch MVP: $0** (all tools have free tiers, we build with existing infrastructure)

| Phase | Cost | Timeline |
|-------|------|----------|
| Research (current) | $0 | Week 1-2 |
| MVP build | $0 (agent time) | Week 3-6 |
| Domain + branding | $10-30 | Week 3 |
| ProductHunt launch | $0 | Week 7 |
| First 6 months ops | $75-200/mo | Months 1-6 |

**Total first 6 months: ~$500-1,200** — well within our self-funded ventures budget.

---
*Last updated: 2026-04-01*
