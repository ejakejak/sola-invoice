BUILD BRIEF — Sola Konveksi Invoice Generator (Web App / PDF)
Reference: E:\sola invoice\.planning\DESIGN.md (verified — produced by @Neo, 146 lines, 9222 bytes)
Plan: E:\sola invoice\.planning\task_plan.md
Findings / data: E:\sola invoice\.planning\findings.md
Reference PDF (design source): C:\Users\muham\AppData\Local\hermes\cache\documents\doc_34db5ff13a50_INV-2026-0004_1.pdf

=== CONTEXT ===
Build a web-based invoice generator. The user inputs invoice data through a form, and the app renders an A4-print-style PDF matching the reference invoice design (monochrome default, optional blue/yellow brand accent toggle). No fabricated names / prices — all numbers come from user input; template rows use placeholder labels.

=== YOUR TASK (@REX) ===
Implement a working web app in E:\sola invoice\ (folder exists) that includes:
1. A single HTML file (or a minimal Next.js / static-site structure) that loads design tokens from DESIGN.md.
2. A form section (input fields):
   - Invoice number (editable, default `INV-2026-0004`; allow custom)
   - Date picker (`DD/MM/YYYY`)
   - Due date picker (`DD/MM/YYYY`)
   - Bill-to: name/company, Attn, address (2 lines), phone
   - Company info: brand title (`Sola Konveksi Yogyakarta` — editable), address (2 lines), contact
   - Line-item editor: description, qty (integer), unit price (`Rp` integer with dot separator), auto-computed total
   - Subtotal / Grand Total / Paid / Outstanding (auto-computed from line items + manual override option)
   - Payment block: BCA account number (editable, default `4452337111`), account holder name (editable, default `Irhami Al Adaby`), instruction text (editable, defaults to reference)
3. A render/preview section showing the A4 layout as defined in DESIGN.md (header left + meta right, bill-to, table, totals, payment, footer).
4. A PDF export function (client-side `window.print()` to PDF, or a library like `html2canvas` + `jspdf` if needed). The output must look like the reference when printed from a browser (test in Chrome/Edge print-to-PDF preview).
5. A download / print button.

=== TECHNICAL CONSTRAINTS ===
- Folder: `E:\sola invoice\` (create files inside, do not overwrite `.planning/`).
- Style must match DESIGN.md tokens:
  - Font: Inter / system sans for body; Cormorant Garamond (Google Font) for brand heading.
  - Layout: A4, 15 mm margins, 2-column top, vertical sections with 0.5 pt rules.
  - Colors: monochrome default (#000 / #fff / #333). Include a `--brand-accent` toggle (optional checkbox) that applies the blue (#034E9E) top bar + yellow (#F9D024) underline deviation documented in DESIGN.md.
  - No decorative borders; clean rules only.
- The generator must NOT fabricate any invoice data. All values default to the reference numbers ONLY as placeholders (`[FILL]` label or editable input with reference value as default). The user must confirm/edit before generating.
- No login/auth required; this is a standalone generator.
- If you use a framework (Next.js), keep it minimal — a single page with embedded CSS/JS is sufficient. If a simple `index.html` works, prefer it for speed.
- Verify the output personally: open the file in a browser, enter the reference data (INV-2026-0004, date 25/09/2026, due 09/10/2026, bill-to GEBIAN SADEWA DUTA PERSADA, line items 2 rows, BCA account, etc.), print to PDF, and confirm the PDF looks like the reference (not just that the button works).

=== VERIFICATION REQUIREMENTS (before reporting done) ===
Before you say "done", confirm ALL of the following with real tool results (not self-reports):
- [ ] The web file exists at a known path (e.g., `E:\sola invoice\index.html` or the Next.js project root).
- [ ] The file loads in a browser (use a headless browser or at least open with a local server and confirm no 404 / syntax errors).
- [ ] The form accepts input (test with the reference values from findings.md).
- [ ] The rendered preview shows all sections: header, meta block, bill-to, line-item table, totals, payment block, footer.
- [ ] The PDF output (via `window.print()` or library) produces a file; inspect that the layout matches the reference (monochrome rules, typography, right-aligned meta, bottom rules, footer text).
- [ ] No fabricated content — any placeholder text is explicitly labeled.
- [ ] The `--brand-accent` toggle works when enabled.

=== WHAT NOT TO DO ===
- Do NOT create a full CRM or database — just a generator.
- Do NOT hard-code fabricated testimonials or extra customers.
- Do NOT skip the verification steps above. A process exit banner is NOT verification.
- Do NOT modify `.planning/` files (they are design/docs; build files go alongside or in a new `src/` / `public/` folder).
- Do NOT rely on the designer's file content as truth — verify against DESIGN.md yourself.

=== NEXT ACTION (EVA) ===
After receiving verified build output, I will run my own verification pass (open file, test PDF output, compare to reference) before reporting to Ejak. If anything is broken, I will ask for a fix pass rather than reporting false success.
