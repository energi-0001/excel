# Hermes + Excel + Dashboard — Office Edition

Paket installer lengkap untuk setup AI assistant dengan skill Excel & akuntansi di VPS Ubuntu. User hanya perlu input API key Bynara masing-masing — langsung dapat CLI + Web Dashboard.

## Quick Start (1 Command)

```bash
curl -fsSL https://raw.githubusercontent.com/energi-0001/excel/main/hermes-excel-migration.tar.gz | tar xz && ./install.sh
```

Saat diminta, masukkan `BYNARA_API_KEY`. Tunggu 5-10 menit.

## Yang Didapat

| Fitur | Detail |
|-------|--------|
| **Web Dashboard** | `http://<IP-VPS>:8080` — chat, drag-drop Excel, tanpa CLI |
| **CLI** | `hermes` — terminal chat |
| **Model AI** | 25 model via Bynara (Claude, GPT, DeepSeek, Qwen, dll) |
| **Skill Excel** | Baca/tulis/edit/pivot/chart/audit file `.xlsx` `.csv` |
| **Skill Akuntansi** | Rekonsiliasi cross-sheet 5 level, deteksi selisih, lacak sumber |

## Kredensial Dashboard

Password dibuat otomatis dan ditampilkan di akhir install:

```
============================================
  INSTALL COMPLETE!
============================================

  Dashboard:  http://123.45.67.89:8080
  Username:   admin
  Password:   aB3xK9mP2qW7     <-- save this!

  CLI:        hermes
  Skills:     excel-spreadsheet, accounting-cross-sheet-recon
  Provider:   bynara (25 models)

  IMPORTANT: Save the password above!
============================================
```

## Requirement

- Ubuntu VPS (20.04 / 24.04)
- Port 8080 terbuka (untuk dashboard)
- BYNARA_API_KEY (dari https://router.bynara.id)

## Cara Pakai

### Dashboard (rekomendasi — no CLI)

Buka browser ke `http://<IP-VPS>:8080`, login, langsung chat:

```
"baca file laporan.xlsx dan tampilkan ringkasan per sheet"
"audit neraca.xlsx, cari ketidakseimbangan"
"cross-check sheet Jurnal vs Buku Besar, tampilkan selisih"
"buat pivot table dari penjualan.xlsx group by bulan sum total"
```

### CLI (untuk yang terbiasa terminal)

```bash
hermes
# atau one-shot:
hermes chat -q "audit Soal_Audit_Manager_Level.xlsx"
```

## Latihan: Soal Audit Manager Level

File `Soal_Audit_Manager_Level.xlsx` adalah soal latihan akuntansi. Setelah install, kerjakan dengan:

```
"audit Soal_Audit_Manager_Level.xlsx, cari semua ketidakseimbangan"
"rekonsiliasi semua sheet, lacak sumber selisih sampai ke baris transaksi"
```

## Struktur Paket

```
hermes-excel-migration.tar.gz
├── install.sh              ← Auto-installer (7 langkah)
├── setup_dashboard.py      ← Helper: generate password + config
├── custom_providers.yaml   ← Bynara: 25 model
└── skills/
    ├── excel-spreadsheet/
    └── accounting-cross-sheet-recon/
```

## Port & Firewall

Pastikan port 8080 terbuka:

```bash
# AWS EC2: buka di Security Group
# VPS lain:
sudo ufw allow 8080
```

## Troubleshooting

**Dashboard tidak bisa diakses:**
```bash
# Cek status service
systemctl --user status hermes-dashboard
# Lihat log
journalctl --user -u hermes-dashboard -f
```

**Hermes command not found:**
```bash
export PATH=$HOME/.local/bin:$PATH
# Atau reload shell
source ~/.bashrc
```

**API key tidak valid:**
```bash
# Edit key di .env
nano ~/.hermes/.env
# Lalu restart
systemctl --user restart hermes-dashboard
```
