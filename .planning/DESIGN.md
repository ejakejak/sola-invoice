# DESIGN.md — Sola Konveksi Invoice Generator (Web / PDF)
Prepared by: @Neo (design routing) | Verified against: INV-2026-0004_1.pdf (pdftotext -layout), design-brief.md, findings.md
Status: design-direction only — build routed to @REX

---

## 1. Layout grid
- Format: A4 portrait (210 × 297 mm). Reference uses Indonesian business format; A4 is standard.
- Orientation: portrait.
- Margins: 15 mm all sides; print-safe area = 180 × 267 mm (within 5 mm printer variance).
- Columns: 2-column top (brand left / meta right); full-width sections below.
- Sections stacked vertically: header → bill-to + meta → table → totals → payment → footer.
- Line rules: 0.5 pt black horizontal rules between sections (tiles, not borders). No decorative borders.

## 2. Typography tokens
- Heading / brand: serif family (e.g., Playfair Display / Cormorant Garamond), 18 pt bold, black (#000000), line-height 1.15. Matches reference's serif-like brand title.
- Subtitle / address: sans-serif, 9 pt regular, #333333, line-height 1.3.
- Meta block (invoice no, date, due): sans-serif, 9 pt regular, #000000; labels 7 pt all-caps tracking 0.05 em.
- Table header: sans-serif, 8 pt bold, #000000, all-caps tracking 0.08 em.
- Table body: sans-serif, 9 pt regular, #222222.
- Numbers / totals: sans-serif, 10 pt regular; totals 11 pt bold.
- Footer: sans-serif, 8 pt italic, #555555.
- Font embedding note (PDF via window.print): use web-safe / Google Fonts loaded with `rel="preconnect"` and `font-display: swap`; print renders via browser engine — avoid custom @font-face only files. Inter (sans) + Cormorant Garamond (serif) recommended; both render reliably to PDF via Chromium/Edge.

## 3. Color tokens
- Default (strict replication): monochrome — background #FFFFFF, text #000000, rules #000000 (0.5 pt), secondary text #333333, muted #555555.
- Brand colors available (Super Duper / Duta Persada KB): Blue #034E9E, Yellow #F9D024.
- Decision: DEFAULT monochrome (replicate reference exactly). DEVIATION option (documented, not enforced): add a 2 pt solid top bar #034E9E across full width above the brand title, and a 1 pt #F9D024 underline under the "KETERANGAN PEMBAYARAN" label. Rationale for deviation: brand visibility for CRM North Star (indigo/slate, Inter, light). Without deviation, invoice is indistinguishable from generic; with it, brand is visible at scan. Either is valid; generator should render monochrome by default and allow a `--brand-accent` toggle.

## 4. Component specs (with dimensions for A4 210×297 at 96 dpi ≈ 794×1123 px)

### 4a. Header — brand + address + contact
- Position: top of page, left-aligned, starts 15 mm from top.
- Brand title "Sola Konveksi Yogyakarta": 18 pt serif bold, black, no logo.
- Address block (2 lines): 9 pt sans, #333, below title with 2 mm gap.
- Contact line: 9 pt sans, #333, below address.
- LOGO DECISION (verified): no logo image in reference. CONFIRMED text-only header is sufficient. Optionally include a 10×10 mm placeholder SVG [LOGO PLACEHOLDER — upload in generator UI] if user wants visual identity, but default is text-only.
- Height: ~45 mm.

### 4b. Right-aligned meta block (invoice meta)
- Position: top-right, aligned with header top. Width ~95 mm.
- Fields: NO / TANGGAL / JATUH TEMPO (label 7 pt all-caps; value 9 pt regular).
- Values: INV-2026-0004 / 25/09/2026 / 09/10/2026 (verified).
- Right-alignment, ragged-left text.
- Separated from left header by 5 mm minimum whitespace.

### 4c. Bill-to block
- Position: left, below header; width ~95 mm.
- Label "BILL TO": 7 pt all-caps bold, black, with 0.5 pt rule under.
- Lines: name + company (bold), Attn, Address (2 lines), Phone.
- Font: 9–10 pt sans.
- Separated from meta block by 5 mm gap.

### 4d. Line-item table
- Columns (width % of 180 mm content): NO 8%, DESKRIPSI 47%, QTY 12%, HARGA SATUAN 16%, JUMLAH 17%.
- Header row: 8 pt all-caps bold, black; 0.5 pt bottom rule.
- Rows: 9 pt regular; row height ~8 mm.
- Numbers right-aligned; descriptions left-aligned.
- Verified row content (template, not hard-coded):
  - 1 | Polo Shirt — COTTON LACOSTE | 30 | Rp 0 | Rp 0  [FILL — sample only]
  - 2 | Polo Shirt — COTTON LACOSTE | 30 | Rp 85.000 | Rp 2.550.000 [FILL — sample only]
- Note (verified): first row at Rp 0 may represent a discount/placeholder; generator computes automatically from qty + unit price.
- Table bottom rule: 0.5 pt black.

### 4e. Subtotal / Grand Total / Outstanding / Paid
- Position: right-aligned block, width ~95 mm, below table.
- Labels (left): Subtotal / Grand Total / Jumlah Dibayar / Sisa Tagihan (Outstanding) — 9 pt sans.
- Values (right): 10 pt bold / 11 pt bold for Grand Total; align decimal.
- Rp format: integer with dot thousand separator, no decimals (verified: Rp 85.000, Rp 2.550.000, Rp 3.470.000).
- Each line separated by 1 pt hairline or 2 mm whitespace; use hairline for cleanliness.

### 4f. Payment instruction block
- Label "KETERANGAN PEMBAYARAN": 7 pt all-caps bold, black, with 0.5 pt underline.
- Text: "Pembayaran dilakukan secara transfer ke rekening: BCA 4452337111 a.n. Irhami Al Adaby" (verified; account holder/name editable via generator input — default to reference value).
- Instruction: "Mohon transfer sesuai jumlah Sisa Tagihan di atas dan konfirmasi melalui kontak kami." (verified).
- Font: 9 pt sans.

### 4g. Footer
- Position: bottom, centered or left-aligned; 10 mm above bottom margin.
- Text: "Terima kasih atas kepercayaan Anda." (verified).
- Font: 8 pt italic, #555555.

---

## 5. PDF output spec (client-side window.print() target)
- Page size: A4 (210 × 297 mm).
- Margins in CSS: `@media print { @page { margin: 15mm; } body { margin: 0; } }`
- Print-safe area: 180 × 267 mm.
- Font embedding: rely on browser engine rendering (no custom font file dependency). Load fonts via `<link>`; browser embeds used glyphs automatically in print-to-PDF.
- No `overflow: hidden` on containers — printer may clip; use `page-break-inside: avoid` on table rows and totals block.
- Background graphics: none (monochrome). If brand accent used, ensure `-webkit-print-color-adjust: exact` and `print-color-adjust: exact` so blue/yellow render.
- File naming convention (generator output): `INV-YYYY-NNNN_N.pdf` per reference format.

## 6. Mock wireframe / structural snippet (direction only — not full build)
```html
<div class="invoice-a4">
  <!-- Header row -->
  <header class="invoice-header">
    <div class="brand-left">
      <h1>Sola Konveksi Yogyakarta</h1>
      <address>Jl. Magelang No.KM 7...</address>
      <p>Telp/WA 62 823-7127-5988</p>
    </div>
    <aside class="meta-right">
      <p><span>NO</span> INV-2026-0004</p>
      <p><span>TANGGAL</span> 25/09/2026</p>
      <p><span>JATUH TEMPO</span> 09/10/2026</p>
    </aside>
  </header>

  <hr class="rule">

  <section class="bill-to-row">
    <div class="bill-to"><h2>BILL TO</h2><p>GEBIAN SADEWA, DUTA PERSADA</p>...</div>
  </section>

  <table class="line-items"><thead>...</thead><tbody>...</tbody></table>

  <section class="totals-right"><p>Subtotal ...</p><p class="grand">Grand Total ...</p></section>

  <hr class="rule">

  <section class="payment"><h3>KETERANGAN PEMBAYARAN</h3><p>...</p></section>

  <footer><p>Terima kasih atas kepercayaan Anda.</p></footer>
</div>
```
CSS skeleton (key only): `body{font-family:Inter,sans-serif;color:#000;background:#fff;} .invoice-a4{width:210mm;padding:15mm;box-sizing:border-box;} h1{font-family:Cormorant Garamond,serif;font-size:18pt;} .rule{border:none;border-top:0.5pt solid #000;margin:4mm 0;} table{width:100%;border-collapse:collapse;font-size:9pt;} th{font-size:8pt;text-transform:uppercase;border-bottom:0.5pt solid #000;} td{padding:2px 4px;} .meta-right{text-align:right;font-size:9pt;}`

---

## 7. Key design decisions (machine-validated)
- layout_format: A4 portrait (210 × 297 mm), 15 mm margins, print-safe 180 × 267 mm.
- typography: Cormorant Garamond (serif, 18 pt brand heading) + Inter / system sans-serif (9–10 pt body, 8 pt table, 7 pt labels). Matches reference serif-like heading and clean sans body; aligns with CRM North Star (Inter, light).
- color_decision: DEFAULT monochrome (#000 / #fff / #333) replicating reference exactly. DEVIATION option documented (thin #034E9E top bar + #F9D024 label underline) with rationale (brand visibility). No fabricated colors applied by default.
- logo: CONFIRMED text-only header; no logo image in reference. Optional [LOGO PLACEHOLDER] SVG slot included in component spec for user upload, but default is text-only.

## 8. Verification / no-fabrication statements
- All invoice numbers, dates, prices, account numbers, and names above are copied exactly from pdftotext of reference PDF (verified path: C:\Users\muham\AppData\Local\hermes\cache\documents\doc_34db5ff13a50_INV-2026-0004_1.pdf). Template rows marked [FILL].
- No testimonial, review, or fabricated customer names added.
- Design routing: @Neo verified; build routed to @REX per design-brief.md.
- No decorative borders; clean 0.5 pt horizontal rules only.

---
File produced: E:\sola invoice\.planning\DESIGN.md
Next: @REX implements generator from these tokens; @Neo / Eva verify against reference before delivery.
