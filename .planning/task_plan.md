---
name: sola-invoice-generator
slug: sola-invoice
description: "Web app (Next.js) that generates print-style PDF invoices matching the Sola Konveksi reference (INV-2026-0004)."
owner: Ejak (Doffy) / Duta Persada / Sola Konveksi
priority: business-critical (invoice generation for student/enrollment billing)
---

## Objective
Build a web app that produces PDF invoices matching the reference PDF (INV-2026-0004) for Sola Konveksi Yogyakarta. The generator must include: company header, bill-to section, line-item table with qty/unit/total, subtotal/grand total, payment instructions (BCA), and due-date tracking.

## Reference source
File: C:\Users\muham\AppData\Local\hermes\cache\documents\doc_34db5ff13a50_INV-2026-0004_1.pdf
Extracted key data (verified from PDF text):
- Brand: Sola Konveksi Yogyakarta
- Address: Jl. Magelang No.KM 7, Mlati Beningan, Sendangadi, Mlati, Sleman Regency, D.I. Yogyakarta 55285, Indonesia
- Contact: Telp/WA 62 823-7127-5988
- Invoice number format: INV-2026-0004
- Date format: DD/MM/YYYY; Due: DD/MM/YYYY
- Line items: Polo Shirt — COTTON LACOSTE (qty, unit price Rp, total Rp)
- Subtotal / Grand Total (Rp with dot thousand separators)
- Outstanding balance line
- Payment instruction block: "Pembayaran dilakukan secara transfer ke rekening: BCA 4452337111 a.n. Irhami Al Adaby"

## Design routing (standing rule)
Every design work routes through @Neo. @REX builds. @EVA verifies.
Do NOT skip @Neo for layout/token decisions — the reference PDF is a design artifact.

## Phases

### Phase 1 — Plan + reference audit (this file) [COMPLETE]
- [x] Extract PDF reference text (pdftotext)
- [x] Confirm design routing to @Neo
- [x] Confirm build routing to @REX
- [x] Confirm user direction: web app, Next.js, PDF export, exact reference layout, folder E:\sola invoice, plan-first per SOP

### Phase 2 — Design direction (@Neo) [IN PROGRESS]
Deliverable: DESIGN.md with layout grid, typography tokens (font: serif/sans?), color tokens (indigo/slate per CRM visual reference E:\whatsapp-crm\design-kit\visual-reference.png if applicable), PDF dimensions (A4 or US Letter?), component list.
Constraints: must replicate reference header, line-item table format, Rp formatting with dot separators, BCA payment block.
Notes: the reference uses a clean white background, thin horizontal rules, no decorative borders. The brand identity for Sola uses blue (#034E9E) and yellow (#F9D024) per D:/Obsidian/03_ORGANIZATION/DUTA_PERSADA/SUPER_DUPER_LANGUAGE_CENTER/ KB.

### Phase 3 — Build (@REX) [PENDING]
Deliverable: working web app in E:\sola invoice/ (Next.js project, or a simpler HTML+JS approach if Next.js overhead exceeds value). Must include:
- Invoice number (editable, auto-incremented from last)
- Date picker + due-date picker
- Bill-to form (name, company, address, phone)
- Line-item editor (description, qty, unit price) — auto-calculates total
- Subtotal, Grand Total, Outstanding (editable or computed)
- Company info block (editable or hard-set from reference)
- PDF generation (client-side: html-to-pdf via browser print or a library like html2canvas + jspdf; server-side: puppeteer/playwright if hosting)
- Download / print button
Constraints: no fabricated testimonials/numbers; placeholder tokens `[FILL]` for any unknown; match reference exactly.

### Phase 4 — Design review (@Neo) + fix pass (@REX) [PENDING]
- @Neo reviews rendered PDF against DESIGN.md
- @REX applies fixes
- @EVA verifies file outputs (not self-reports)

### Phase 5 — Ship + commit [PENDING]
- Verify live output (generate a test PDF, inspect content)
- Commit to GitHub (DigMarkDuper / ejakejak per routing; switch auth first)
- Report deliverable path + sample output to Ejak

## Risks / open decisions
1. PDF generation library: client-side (no server needed) vs server-side (better layout fidelity). Recommendation: start with client-side `window.print()` to PDF; upgrade to `html2canvas` + `jspdf` if layout breaks.
2. Brand colors: reference is black text on white. Confirm if blue/yellow (Super Duper KB) should appear as a thin top bar or logo area. @Neo to decide.
3. Invoice number auto-increment: needs persistence (localStorage or a file). If web-only, use localStorage; if CLI/script, use a json file.
4. No real testimonials/names to fabricate — any bill-to names must come from Ejak's input or use placeholder `[FILL: NAME]`.

## Next action (EVA)
Dispatch @Neo with brief pointing to this plan + reference PDF + brand KB (Super Duper colors). Ask for DESIGN.md (layout grid + tokens) before any build starts.
