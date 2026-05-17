# Kuisioner Jawaban - Insurance Policy Risk Checking

## 1. Problem Statement

**Permasalahan Utama:**

Dokumen polis asuransi di Indonesia umumnya ditulis dengan bahasa hukum yang kompleks dan panjang, menyebabkan beberapa masalah:

- **Pemegang polis** sulit memahami klausul-klausul penting yang mengandung risiko
- **Tim legal perusahaan** memerlukan waktu lama untuk mereview setiap dokumen polis secara manual
- **Potensi kerugian** akibat klausul berisiko tinggi yang terlewatkan saat signing

**Yang Terdampak:**

- Perusahaan yang menggunakan asuransi komersial
- Tim legal/kompliance officer
- Broker asuransi yang mereview polis untuk klien

**Mengapa Penting:**

Satu klausul berisiko tinggi yang terlewat dapat menyebabkan kerugian finansial besar saat klaim ditolak atau dibayar sebagian.

---

## 2. Target Users

**Pengguna Utama:**

**Profesi:** Legal Counsel, Compliance Officer, Risk Manager

**Usia:** 28-50 tahun

**Kebutuhan:** Review cepat dokumen polis sebelum signing

**Konteks Penggunaan:** Saat menerima draft polis dari asuransi, sebelum finalisasi kontrak

**Kebutuhan Spesifik:**

- Hasil analisis yang cepat (under 2 menit untuk dokumen 10-20 halaman)
- Penjelasan risiko dalam bahasa yang mudah dipahami (non-legal jargon)
- Rekomendasi alternatif klausul yang lebih aman
- Format output yang bisa di-share ke tim/boss

---

## 3. Potential Impact

**Bagaimana Solusi AI Menyelesaikan Masalah:**

**Sebelum AI:**
- Waktu Review: 2-4 jam per dokumen
- Coverage: Manual scan, risk missing clauses
- Consistency: Depends on reviewer experience
- Documentation: Manual notes

**Setelah AI:**
- Waktu Review: 2-5 menit per dokumen
- Coverage: Automated extraction of all clauses
- Consistency: Standardized risk scoring
- Documentation: Auto-generated structured report

**Manfaat Bagi Stakeholder:**

**Untuk Perusahaan:**
- Reduksi risiko klausul berbahaya
- Efisiensi tim legal (bisa handle lebih banyak polis)
- Dokumentasi review untuk audit/compliance

**Untuk Tim Legal:**
- First-pass screening otomatis
- Fokus hanya pada klausul flagged sebagai high-risk
- Lebih cepat memberikan rekomendasi ke stakeholder

---

## 4. Improvisasi/Modifikasi dari Project Original

**Project Asli:** IBM Legal Starter Project (kontrak vendor analysis)

**Modifikasi yang Dilakukan:**

**LLM Provider:**
- Original: Google Gemini
- Modifikasi: OpenRouter dengan model Xiaomi

**Model LLM1 (Ekstraksi):**
- Original: Gemini Flash
- Modifikasi: Xiaomi/mimo-v2-flash

**Model LLM2 (Analisis):**
- Original: Gemini Pro
- Modifikasi: Xiaomi/mimo-v2.5-pro

**Context:**
- Original: Kontrak vendor umum
- Modifikasi: Polis asuransi spesifik

**System Prompt:**
- Original: General legal review
- Modifikasi: Insurance risk assessment focused

**LLM2 Mode:**
- Original: Standard completion
- Modifikasi: Agent mode dengan follow-up question support

**Trigger:**
- Original: Run flow button
- Modifikasi: Chat Input untuk interaktivitas

**Version Control:**
- Original: Tidak ada
- Modifikasi: Git repository untuk tracking changes

**Alasan Perubahan:**
- OpenRouter memberikan akses ke model alternatif dengan cost/performance ratio yang berbeda
- Agent mode memungkinkan interaksi lebih natural (follow-up questions)
- Context asuransi memerlukan penyesuaian prompt untuk terminology spesifik

---

## 5. Penjelasan Singkat Alur Sistem

```
Input → Read File → LLM1 (Ekstraksi) → Parser → LLM2 (Analisis) → Output
              ↓                                                    ↓
         Dokumen Polis                                      Chat Output
         (PDF/Word/TXT)                                     (Interactive)
                                                              ↓
                                                        JSON Report
                                                        (Risk Summary)
```

**Detail Alur:**

1. **Input** - User upload dokumen polis (PDF, Word, atau TXT)

2. **Read File** - Sistem membaca dan mengekstrak teks dari dokumen

3. **LLM1 (Ekstraksi)** - Model Xiaomi/mimo-v2-flash mengekstrak klausul-klausul penting dalam format terstruktur (JSON)

4. **Parser** - Memproses dan memparsing output LLM1 menjadi format yang konsisten

5. **LLM2 (Analisis)** - Model Xiaomi/mimo-v2.5-pro dalam mode Agent melakukan:
   - Risk assessment untuk setiap klausul
   - Penjelasan alasan risiko
   - Rekomendasi alternatif klausul yang lebih aman
   - Follow-up Q&A dengan user

6. **Output** - Dua format output:
   - Chat Output: Interaktif conversation dengan user
   - JSON Report: Structured risk summary untuk dokumentasi

---

## 6. Potensi Pengembangan Lanjutan

**1. Multi-Dokumen Comparison**

Fitur untuk membandingkan polis dari beberapa asuransi sekaligus. Memudahkan pemilihan vendor terbaik berdasarkan perbandingan klausul dan harga.

**2. Custom Risk Template**

User bisa define risk criteria sendiri sesuai kebutuhan industri spesifik. Misalnya, perusahaan construction punya risk profile berbeda dengan perusahaan IT.

**3. Historical Tracking**

Simpan semua review untuk trend analysis. Fitur ini berguna untuk audit trail dan compliance reporting, melihat bagaimana risk profile berubah dari waktu ke waktu.

**4. Integration API**

REST API untuk koneksi ke sistem dokumen perusahaan. Memungkinkan workflow automation, misalnya setiap ada dokumen polis masuk, otomatis di-review oleh sistem.

**5. Multi-Language Support**

Support Bahasa Inggris dan Indonesia. Berguna untuk perusahaan multinasional yang menangani polis dalam kedua bahasa.

**6. Collaboration Features**

Comment, share, dan approval workflow. Tim legal bisa berkolaborasi dalam review polis, memberikan komentar, dan melakukan approval secara terstruktur.

---

## 7. Ide Project Lain yang Muncul

**Judul Project:** Peraturan MCP (Model Context Protocol) Library

**Konsep:**

Library yang meng-index seluruh peraturan perundang-undangan Indonesia (UU, Perpres, Permen, Perda, Pergub) dalam format structured yang bisa di-consume oleh LLM agents melalui MCP protocol.

**Problem yang Diselesaikan:**

1. **Hallucination** - LLM sering memberikan informasi hukum yang salah atau outdated
2. **Fragmented sources** - Peraturan.go.id hanya menyediakan PDF tanpa query capability
3. **No semantic search** - Sulit mencari peraturan relevan berdasarkan intent, bukan keyword

**Fitur Utama:**

- Semantic search across all regulations
- Citation grounding untuk setiap jawaban LLM
- Automatic update mechanism saat ada peraturan baru
- MCP server untuk easy integration dengan any LLM agent

**Target User:**

- Legal tech startups
- AI assistant developers
- Research institutions
- Government agencies

---

*Dokumen ini merupakan jawaban kuisioner untuk Capstone Project IBM Skillsbuild x Haktiv8 - Pertemuan 3*
