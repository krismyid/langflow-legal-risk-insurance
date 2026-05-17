# Kuisioner Jawaban - Insurance Policy Risk Checking

## 1. Problem Statement

**Permasalahan Utama:**
Dokumen polis asuransi di Indonesia umumnya ditulis dengan bahasa hukum yang kompleks dan panjang, menyebabkan:
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

| Karakteristik | Deskripsi |
|---------------|-----------|
| **Profesi** | Legal Counsel, Compliance Officer, Risk Manager |
| **Usia** | 28-50 tahun |
| **Kebutuhan** | Review cepat dokumen polis sebelum signing |
| **Konteks Penggunaan** | Saat menerima draft polis dari asuransi, sebelum finalisasi kontrak |

**Kebutuhan Spesifik:**
- Hasil analisis yang cepat (under 2 menit untuk dokumen 10-20 halaman)
- Penjelasan risiko dalam bahasa yang mudah dipahami (non-legal jargon)
- Rekomendasi alternatif klausul yang lebih aman
- Format output yang bisa di-share ke tim/boss

---

## 3. Potential Impact

**Bagaimana Solusi AI Menyelesaikan Masalah:**

| Aspek | Sebelum AI | Setelah AI |
|-------|------------|------------|
| **Waktu Review** | 2-4 jam per dokumen | 2-5 menit per dokumen |
| **Coverage** | Manual scan, risk missing clauses | Automated extraction of all clauses |
| **Consistency** | Depends on reviewer experience | Standardized risk scoring |
| **Documentation** | Manual notes | Auto-generated structured report |

**Manfaat Bagi Stakeholder:**

1. **Untuk Perusahaan:**
   - Reduksi risiko klausul berbahaya
   - Efisiensi tim legal (bisa handle lebih banyak polis)
   - Dokumentasi review untuk audit/compliance

2. **Untuk Tim Legal:**
   - First-pass screening otomatis
   - Fokus hanya pada klausul flagged sebagai high-risk
   - Lebih cepat memberikan rekomendasi ke stakeholder

---

## 4. Improvisasi/Modifikasi dari Project Original

**Project Asli:** IBM Legal Starter Project (kontrak vendor analysis)

**Modifikasi yang Dilakukan:**

| Aspek | Original | Modifikasi |
|-------|----------|------------|
| **LLM Provider** | Google Gemini | OpenRouter dengan model Xiaomi |
| **Model LLM1** (Ekstraksi) | Gemini Flash | Xiaomi/mimo-v2-flash |
| **Model LLM2** (Analisis) | Gemini Pro | Xiaomi/mimo-v2.5-pro |
| **Context** | Kontrak vendor umum | Polis asuransi spesifik |
| **System Prompt** | General legal review | Insurance risk assessment focused |
| **LLM2 Mode** | Standard completion | Agent mode dengan follow-up question support |
| **Trigger** | Run flow button | Chat Input untuk interaktivitas |
| **Version Control** | Tidak ada | Git repository untuk tracking changes |

**Alasan Perubahan:**
- OpenRouter memberikan akses ke model alternatif dengan cost/performance ratio yang berbeda
- Agent mode memungkinkan interaksi lebih natural (follow-up questions)
- Context asuransi memerlukan penyesuaian prompt untuk terminology spesifik

---

## 5. Penjelasan Singkat Alur Sistem

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Input      │────▶│  Read File       │────▶│  LLM1           │
│  (Dokumen   │     │  (PDF/Word/TXT)  │     │  (Xiaomi/       │
│   Polis)    │     │                  │     │   mimo-v2-      │
└─────────────┘     └──────────────────┘     │   flash)        │
                                              │                 │
                                              │  Ekstraksi      │
                                              │  Klausul        │
                                              └────────┬────────┘
                                                       │
                              ┌────────────────────────┘
                              ▼
                    ┌──────────────────┐
                    │  Parser          │
                    │  (JSON           │
                    │   Structuring)   │
                    └────────┬─────────┘
                             │
              ┌──────────────┘
              ▼
    ┌──────────────────────────┐
    │  LLM2                    │
    │  (Xiaomi/mimo-v2.5-pro)  │
    │                          │
    │  Agent Mode              │
    │  - Risk Assessment       │
    │  - Recommendations       │
    │  - Follow-up Q&A         │
    └─────────────┬────────────┘
                  │
    ┌─────────────┴──────────────┐
    │                            │
    ▼                            ▼
┌──────────┐           ┌──────────────────┐
│  Chat    │           │  Structured      │
│  Output  │           │  JSON Report     │
│  (Inter- │           │  (Risk Summary)  │
│   active)│           └──────────────────┘
└──────────┘
```

---

## 6. Potensi Pengembangan Lanjutan

| Fitur | Deskripsi | Benefit |
|-------|-----------|---------|
| **Multi-Dokumen Comparison** | Bandingkan polis dari beberapa asuransi sekaligus | Memudahkan pemilihan vendor terbaik |
| **Custom Risk Template** | User bisa define risk criteria sendiri | Sesuai kebutuhan industri spesifik |
| **Historical Tracking** | Simpan semua review untuk trend analysis | Audit trail dan compliance reporting |
| **Integration API** | REST API untuk koneksi ke sistem dokumen perusahaan | Workflow automation |
| **Multi-Language Support** | Support Bahasa Inggris dan Indonesia | Reach user internasional |
| **Collaboration Features** | Comment, share, dan approval workflow | Team collaboration pada review polis |

---

## 7. Ide Project Lain yang Muncul

**Judul Project:** **Peraturan MCP (Model Context Protocol) Library**

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
