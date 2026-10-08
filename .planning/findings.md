---
source: reference PDF (INV-2026-0004_1.pdf) + brand KB + user direction
verified: yes (pdftotext output captured; brand KB read from disk; user direction from Discord thread 1557664026908168226)
---

## Reference invoice — verified data (from PDF text)

File path: C:\Users\muham\AppData\Local\hermes\cache\documents\doc_34db5ff13a50_INV-2026-0004_1.pdf
Extraction method: `pdftotext -layout`

### Header / Brand
- Title: Sola Konveksi Yogyakarta
- Address line 1: Jl. Magelang No.KM 7, Mlati Beningan, Sendangadi, Mlati, Sleman Regency
- Address line 2: D.I. Yogyakarta 55285, Indonesia
- Contact: Telp/WA 62 823-7127-5988

### Invoice meta (top-right block)
- Invoice number: INV-2026-0004
- Date: 25/09/2026
- Due date: 09/10/2026

### Bill-to block
- Name: GEBIAN SADEWA, DUTA PERSADA
- Attn: EJAK
- Address: Jl. Ibu Ruswo 555
- Phone: 00

### Line items (table with rules)
Columns: NO | DESKRIPSI | QTY | HARGA SATUAN | JUMLAH
Row 1: Polo Shirt — COTTON LACOSTE | 30 | Rp 0 | Rp 0 (note: appears to be a zero-price line; total sum combines with row 2 to reach subtotal)
Row 2: Polo Shirt — COTTON LACOSTE | 30 | Rp 85.000 | Rp 2.550.000
Subtotal: Rp 3.470.000
Grand Total: Rp 3.470.000
Outstanding (Sisa Tagihan): Rp 3.470.000
Paid (Jumlah Dibayar): Rp 0

Note: the subtotal/grand total appear to aggregate both rows. The first row at Rp 0 may be a placeholder/discount or a data entry error in the reference; the generator should allow any qty/unit/total and compute automatically rather than hard-coding this anomaly.

### Payment block (bottom)
"Pembayaran dilakukan secara transfer ke rekening: BCA 4452337111 a.n. Irhami Al Adaby"
Instruction: "Mohon transfer sesuai jumlah Sisa Tagihan di atas dan konfirmasi melalui kontak kami."
Footer: "Terima kasih atas kepercayaan Anda."

### Design observations (for @Neo)
- White background, black text, no decorative borders.
- Thin horizontal rules separate sections (header from bill-to, bill-to from table, table from totals, totals from payment block).
- Typography: appears serif-like for headings (Sola Konveksi Yogyakarta), sans for body/text.
- No logo image visible in the reference; the brand relies on typography and address.
- Right-aligned invoice number / date / due date block.
- Line-item table has vertical alignment; numbers right-aligned.
- Rp format: integer with dot as thousand separator (e.g., Rp 85.000, Rp 2.550.000, Rp 3.470.000). No decimal places shown.
- The BCA bank account line is a critical business element — must be editable (account holder/name can change) but should default to the reference value.

### Brand KB cross-check
- Super Duper / Duta Persada KB (D:/Obsidian/03_ORGANIZATION/DUTA_PERSADA/SUPER_DUPER_LANGUAGE_CENTER/) records: Blue #034E9E, Yellow #F9D024.
- The reference PDF uses no brand color; it is monochrome. Recommendation: @Neo can propose adding a thin blue (#034E9E) top bar or yellow (#F9D024) accent line without violating the reference, OR keep monochrome for strict replication. This is an open design decision.
- CRM visual North Star (E:\whatsapp-crm\design-kit\visual-reference.png): Indigo, slate, Inter font, light design. The invoice reference is closer to this clean/light direction than to any decorative approach.

### Routing notes
- Design routing (standing): EVERY design work routes through @Neo.
- Build routing: @REX handles implementation.
- No fabrication: all numbers in the generator will come from user input; no fabricated testimonials, names, or prices.
