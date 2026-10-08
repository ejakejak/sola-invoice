DESIGN BRIEF — Sola Konveksi Invoice Generator (Web App / PDF)
Reference: INV-2026-0004_1.pdf (verified via pdftotext)
Plan: E:\sola invoice\.planning\task_plan.md
Findings: E:\sola invoice\.planning\findings.md

=== CONTEXT ===
Brand: Sola Konveksi Yogyakarta (Duta Persada / Super Duper child brand)
Business: student enrollment / course billing invoices
Reference design is monochrome (black on white) with thin horizontal rules.
Brand KB (Super Duper): Blue #034E9E, Yellow #F9D024.
CRM North Star: Indigo, slate, Inter font, light weight.

=== YOUR TASK ===
Produce a DESIGN.md file (in E:\sola invoice\.planning\ or delivered back) that defines:
1. Layout grid (A4 portrait or US Letter? Recommend A4 since reference is Indonesian business format)
2. Typography tokens (heading font family, body font family, sizes in pt or px, weight)
3. Color tokens (primary, secondary, text, rules, background — include whether to use the monochrome reference or add blue/yellow accent)
4. Component list with dimensions:
   - Header: brand name + address + contact line
   - Right-aligned meta block (invoice no, date, due date)
   - Bill-to block (name, company, attn, address, phone)
   - Line-item table (NO / DESKRIPSI / QTY / HARGA SATUAN / JUMLAH) with column widths
   - Subtotal / Grand Total / Outstanding / Paid lines
   - Payment instruction block (BCA account, instruction text)
   - Footer (thanks line)
5. PDF output spec: dimensions, margins, print-safe area, font embedding note
6. A mock wireframe description or a simple HTML/CSS snippet that shows the layout structure (not a full build — direction only)

=== CONSTRAINTS ===
- Replicate the reference exactly unless you propose a deliberate deviation (e.g., adding a blue top bar). Any deviation must be noted in DESIGN.md with rationale.
- Do NOT fabricate testimonials, names, or prices. Any placeholder tokens must be labeled [FILL].
- Design must work for web display AND PDF export (client-side `window.print()` to PDF is the target build path; keep layout simple enough to survive print rendering).
- No decorative borders. Keep the clean line-rule style from the reference.
- Reference has no logo image. Confirm whether a text-only header is sufficient or whether a logo placeholder should be included.

=== DELIVERABLE ===
File: E:\sola invoice\.planning\DESIGN.md (or delivered back via message with file path confirmed)
Includes: layout grid, typography tokens, color tokens, component specs, PDF spec, mock structure.

=== SOURCE FILES TO READ ===
- E:\sola invoice\.planning\task_plan.md
- E:\sola invoice\.planning\findings.md
- C:\Users\muham\AppData\Local\hermes\cache\documents\doc_34db5ff13a50_INV-2026-0004_1.pdf (reference — text already extracted; design only)
- Brand KB reference (if accessible): D:/Obsidian/03_ORGANIZATION/DUTA_PERSADA/SUPER_DUPER_LANGUAGE_CENTER/

=== TIME ===
Estimated: 20-30 minutes. This is a bounded design-direction task, not a full build.

=== WHAT I (EVA) WILL DO NEXT ===
After receiving DESIGN.md, I will dispatch @REX to build the web app based on your tokens and specs. I will verify both outputs personally (not rely on self-reports).
