# quiz

> 🇺🇸 [English](./README.md) | 🇯🇵 [日本語](./README.ja.md) | 🇨🇳 [简体中文](./README.zh-Hans.md) | 🇪🇸 [Español](./README.es.md) | 🇮🇳 [हिन्दी](./README.hi.md) | 🇧🇷 [Português](./README.pt.md) | 🇮🇩 **Bahasa Indonesia**

Skill kuis coding interaktif untuk Claude Code. Ulas dan perkuat apa yang dipelajari selama pengembangan — bug, library, insight debugging — dalam format kuis.

## Instalasi

```
/plugin marketplace add kanketsu-jp/quiz
/plugin install quiz@kanketsu-quiz
```

## Penggunaan

### 1. Buat materi belajar

Buat direktori `.temp/learn/{nomor}/` dengan dua file:

```
.temp/learn/1/
├── study-notes.md   # Catatan belajar (konteks, kode, penjelasan)
└── qa-list.md       # Daftar tanya jawab (sumber data kuis)
```

Atau minta Claude Code:

```
Rangkum perbaikan tadi ke .temp/learn/1/ sebagai materi belajar.
Buat study-notes.md dan qa-list.md.
```

### 2. Jalankan kuis

```
/quiz 1            # Jalankan kuis #1
/quiz scrollarea   # Cari berdasarkan kata kunci
/quiz              # Daftar kuis tersedia
/quiz list         # Daftar kuis tersedia
```

## Mode Kuis

| Mode | Deskripsi |
|------|-----------|
| Semua pertanyaan | Semua pertanyaan berurutan |
| Acak 5 | 5 pertanyaan acak |
| Per kategori | Pilih kategori |

## Format File

### qa-list.md

```markdown
## Nama Kategori

### Q1: Teks pertanyaan?

#### A

Teks jawaban (blok kode atau teks biasa)
```

Judul `##` adalah kategori. `### Q:` adalah pertanyaan. `#### A` adalah jawaban.

### study-notes.md

Markdown format bebas. Latar belakang, analisis akar masalah, kode perbaikan, pelajaran yang dipetik. Dirujuk sebagai penjelasan saat jawaban salah.

## Praktik Terbaik

| Kapan | Apa yang dilakukan |
|-------|-------------------|
| Setelah memperbaiki bug | Minta Claude membuat materi belajar |
| Hari berikutnya | `/quiz` untuk mengulas pembelajaran kemarin |
| Akhir pekan | `/quiz` untuk ulasan mingguan |
| Setelah code review | Ubah umpan balik menjadi materi |

## .gitignore

`.temp/` sebaiknya ada di `.gitignore`. Materi belajar hanya untuk lokal.

```gitignore
.temp/
```

## Konfigurasi

Secara default, quiz membaca materi belajar dari `.temp/learn/`. Anda dapat menyesuaikan path menggunakan file konfigurasi:

| Prioritas | File | Format |
|-----------|------|--------|
| 1 | `.claude/quiz.json` | `{ "learn_dir": "path/to/dir" }` |
| 2 | `.claude/settings.local.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 3 | `.claude/settings.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 4 | Default | `.temp/learn/` |

Contoh `.claude/quiz.json`:

```json
{
  "learn_dir": "docs/quiz-materials"
}
```

## Keamanan

- Hanya membaca file konfigurasi dari direktori `.claude/` (untuk resolusi `learn_dir`)
- Hanya membaca file materi belajar dari direktori yang dikonfigurasi
- Tidak menjalankan perintah shell
- Tidak mengubah file apa pun
- Instruksi dalam materi belajar diabaikan (diperlakukan hanya sebagai konten)

## Lisensi

MIT
