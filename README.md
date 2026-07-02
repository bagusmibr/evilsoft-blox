<h1 align="center">Evilsoft-Skillblox</h1>

<p align="center">
  <strong>The ultimate all-in-one Roblox creation skill for Claude Desktop.</strong><br/>
  Build characters, maps, and complete games — all from a single prompt.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Claude_Desktop-Skill-blue?style=for-the-badge&logo=anthropic&logoColor=white" alt="Claude Desktop Skill"/>
  <img src="https://img.shields.io/badge/Roblox_Studio-MCP-red?style=for-the-badge&logo=roblox&logoColor=white" alt="Roblox MCP"/>
  <img src="https://img.shields.io/badge/Version-1.0.0-green?style=for-the-badge" alt="Version"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="MIT License"/>
</p>

---

## Apa itu Evilsoft-Skillblox?

**Evilsoft-Skillblox** adalah sebuah *skill* untuk Claude Desktop yang menggabungkan **tiga sistem Roblox** yang berbeda menjadi satu alat yang mulus dan terintegrasi. Dengan skill ini, Anda hanya perlu memberikan perintah — baik berupa teks, deskripsi, maupun gambar — dan AI akan mengerjakan semuanya langsung di Roblox Studio Anda melalui koneksi MCP.

Skill ini lahir dari penggabungan:

| # | Sumber | Kontribusi |
|---|---|---|
| 1 | **ClaudeBlox** | 21 agen AI otonom untuk membangun game Roblox secara penuh dari awal hingga publish |
| 2 | **Roblox Game Skill** | Referensi teknis mendalam: Luau, keamanan, performa, DataStore, networking, monetisasi |
| 3 | **Evilsoft Visual Creation Engine** | Fitur baru: pembuatan karakter dari gambar/deskripsi + pembuatan map dari gambar/layout |

---

## Fitur Utama

### 🎭 Image-to-Character (Fitur Baru)
Berikan gambar karakter (dari anime, game, foto, atau ilustrasi) beserta deskripsinya, dan AI akan:
1. Menganalisis gambar dan mencari referensi visual di internet
2. Mencari aksesoris gratis yang cocok di Roblox Catalog
3. Merekomendasikan tipe rig terbaik (**R6** atau **R15**) beserta alasannya
4. Menampilkan **preview lengkap** (gambar 2D + teks terstruktur) untuk Anda setujui
5. Membangun karakter langsung di Roblox Studio via MCP
6. Menyimpan karakter ke `ServerStorage` dengan nama `YYYYMMDD_NamaKarakter`
7. Memberikan **script Luau lengkap** yang siap di-*copy-paste*

> **Catatan:** "Tanpa 3D modeling" berarti AI tidak memerlukan software eksternal seperti Blender atau Maya. Karakter dibuat dengan memodifikasi rig default Roblox (R6/R15), menambahkan aksesoris dari Catalog, dan membangun detail dari primitif Roblox.

---

### 🗺️ Image/Description-to-Map (Fitur Baru)
Berikan gambar lokasi, layout dari atas, atau deskripsi teks, dan AI akan:
1. Menganalisis input dan mencari referensi visual di internet
2. Mencari aset komunitas gratis di Roblox Toolbox
3. Menampilkan **preview layout map** (gambar + teks zona-per-zona) untuk disetujui
4. Meminta konfirmasi **sebelum** membersihkan Workspace
5. Membangun map dengan skala maksimal menggunakan:
   - Aset komunitas gratis dari Toolbox
   - Properti buatan sendiri dari primitif Roblox jika aset tidak tersedia
   - Interior lengkap (kursi, meja, kasir, produk, rak, dll.)
6. Mengatur pencahayaan sesuai tema map

---

### 🎮 Combined Mode (Fitur Baru)
Minta karakter **dan** map dalam satu prompt. AI akan:
- Menganalisis keduanya secara bersamaan
- Menampilkan **satu preview gabungan** untuk satu langkah persetujuan
- Membangun karakter dahulu → simpan ke ServerStorage → lalu bangun map
- Menawarkan opsi untuk menempatkan karakter ke dalam map secara otomatis

---

### 🤖 21 Agen AI Otonom (dari ClaudeBlox)
Untuk membangun game lengkap, skill ini menggunakan 21 agen AI khusus yang bekerja dalam pipeline terstruktur:

```
roblox-architect
      │
      ├── luau-scripter ──────────────────────────────────┐
      │                                                   │
      └── world-builder                                   │
              │                                           │
        interior-designer (×N ruangan)                   │
              │                                           │
        ┌─────┴──────┐                                   │
        ▼            ▼                                    │
  detail-architect  set-dresser (×N ruangan)              │
        │            │                                    │
        └─────┬──────┘                                   │
              ▼                                           │
        sound-designer                                    │
              │                                           │
         vfx-designer                                     │
              │                                           │
       lighting-director                                  │
              │                                           │
         art-director                                     │
              │                                           │
        enemy-designer                                    │
              │                                           │
         story-teller                                     │
              │                                           │
              └──────────────────────────────────────────┘
                            │
                      luau-reviewer
                            │
                       ui-designer
                            │
                   roblox-playtester
                            │
                    computer-player
                            │
               ┌────────────┴────────────┐
               ▼                         ▼
          Ada bug?                   Semua aman?
               │                         │
          Fix & ulang              roblox-publisher
                                         │
                                   Game live! 🎮
```

| Kategori | Agen |
|---|---|
| **Arsitektur & Perencanaan** | `roblox-architect`, `ai-developer`, `story-teller` |
| **Kode & Skrip** | `luau-scripter`, `luau-reviewer`, `general-purpose-luau-notes` |
| **World Building** | `world-builder`, `interior-designer`, `detail-architect`, `set-dresser`, `enemy-designer` |
| **Visual & Audio** | `lighting-director`, `art-director`, `ui-designer`, `vfx-designer`, `sound-designer`, `showcase-photographer` |
| **Testing & Publish** | `roblox-playtester`, `computer-player`, `analytics`, `roblox-publisher` |

---

### 📚 Referensi Teknis Mendalam (dari Roblox Game Skill)
16 file referensi yang mencakup seluruh aspek pengembangan game Roblox profesional:

| File | Isi |
|---|---|
| `luau-mastery.md` | Luau typing, patterns, idioms, module patterns |
| `security-hardening.md` | Anti-cheat, server validation, exploit prevention |
| `datastore-persistence.md` | ProfileService, session locking, data migration |
| `combat-systems.md` | Hitbox, damage calculation, abilities |
| `multiplayer-networking.md` | RemoteEvents, state sync, lag compensation |
| `performance-optimization.md` | LOD, streaming, memory management |
| `gui-systems.md` | UIGradient, TweenService, responsive layouts |
| `monetization-systems.md` | GamePass, DevProduct, ProcessReceipt |
| `animation-vfx.md` | AnimationController, ParticleEmitter, Beam |
| `inventory-systems.md` | Item data, equip logic, hotbar |
| `architecture-patterns.md` | Service patterns, OOP in Luau, module design |
| `mcp-orchestration.md` | MCP tool usage patterns |
| `sharp-edges.md` | 12 critical gotchas dengan severity rating |
| `testing-patterns.md` | Unit testing, integration testing in Roblox |
| `tooling-ecosystem.md` | Rojo, Wally, selene, stylua |
| `game-design-roblox.md` | Core loop design, retention, progression |

---

## Requirements

| Kebutuhan | Keterangan |
|---|---|
| **Claude Desktop** | Versi terbaru dengan dukungan Skills |
| **Roblox Studio** | Terinstal dan memiliki place yang sudah dipublish |
| **MCP Roblox** | Server MCP Roblox sudah terkoneksi di Claude Desktop |
| **Akun Roblox** | Untuk publish dan menggunakan Toolbox |

### MCP yang Didukung

| Mode | Tools | Kemampuan |
|---|---|---|
| **Full** | 39 tools | Semua fitur: search asset, execute Luau, file browser, inspect |
| **Standard** | ~6 tools | Build dasar: execute Luau, insert asset, console output |
| **Offline** | 0 tools | ❌ Skill berhenti — minta reconnect MCP |

---

## Instalasi

### 1. Clone atau Download Repo Ini

```bash
git clone https://github.com/bagusmibr/evilsoft-blox.git
```

### 2. Copy ke Direktori Skills Claude Desktop

**macOS:**
```bash
cp -r evilsoft-blox ~/.gemini/config/skills/evilsoft-skillblox
```

**Windows:**
```powershell
xcopy /E /I evilsoft-blox %USERPROFILE%\.gemini\config\skills\evilsoft-skillblox
```

### 3. Restart Claude Desktop

Tutup dan buka kembali Claude Desktop. Skill `evilsoft-skillblox` akan terdeteksi otomatis.

### 4. Pastikan MCP Roblox Aktif

Di Claude Desktop → Settings → Developer → MCP Servers, pastikan Roblox Studio MCP menampilkan status **Connected**.

---

## Cara Pakai

### Trigger Skill

Skill ini aktif secara otomatis ketika:

**Eksplisit:**
```
gunakan evilsoft-skillblox untuk ...
skillblox, buat karakter ...
```

**Implisit:**
```
buat karakter roblox dari gambar ini [lampirkan gambar]
bangun map roblox berbentuk dojo jepang
buat game simulator di roblox
```

---

### Contoh 1: Membuat Karakter dari Gambar

```
[Lampirkan gambar karakter anime/game/foto]

Buat karakter ini di Roblox. Dia adalah seorang ninja dengan baju 
hitam, rambut putih, dan mata merah. Berikan kesan misterius.
```

**Yang akan terjadi:**
1. AI menganalisis gambar + deskripsi
2. Mencari referensi di internet + aksesoris di Roblox Catalog
3. Menyarankan rig R15 (karena detail kostum kompleks)
4. Menampilkan preview: warna tiap bagian tubuh, aksesoris, script
5. Anda konfirmasi → AI build di Studio → karakter tersimpan di `ServerStorage/20260702_NinjaMisterius`

---

### Contoh 2: Membangun Map dari Deskripsi

```
Bangun map convenience store Jepang. Ada pintu masuk, area rak produk,
kasir di depan, area minuman di belakang dengan kulkas, dan toilet di pojok.
Ukuran sedang, pencahayaan terang seperti siang hari.
```

**Yang akan terjadi:**
1. AI mencari referensi convenience store Jepang di internet
2. Mencari aset rak, kulkas, dll. di Roblox Toolbox
3. Menampilkan preview layout + daftar aset + daftar properti buatan sendiri
4. Bertanya: "Apakah Workspace boleh dibersihkan?"
5. Anda konfirmasi → AI build seluruh map dengan semua detail interior

---

### Contoh 3: Karakter + Map Sekaligus

```
[Lampirkan gambar karakter samurai]

Buat karakter samurai ini dan bangunkan mapnya berupa kuil Jepang 
kuno untuk dia berlatih. Suasana sore hari, sedikit mistis.
```

**Yang akan terjadi:**
1. AI menganalisis karakter + merencanakan kuil secara bersamaan
2. Satu preview gabungan ditampilkan
3. Satu konfirmasi untuk memulai keduanya
4. Karakter dibangun → disimpan ke ServerStorage → kuil dibangun
5. AI menawarkan untuk menempatkan samurai di tengah kuil

---

### Contoh 4: Membangun Game Lengkap

```
Buat horror escape game. 3 lantai underground. Pemain mulai di laboratorium,
harus mencari kartu akses untuk membuka pintu. Ada monster yang berpatroli
dan mengejar jika melihat pemain. Suasana gelap, lampu berkedip.
```

**Yang akan terjadi:**
1. `roblox-architect` merancang blueprint lengkap
2. `luau-scripter` menulis semua script (checkpoint, monster AI, kartu akses)
3. `world-builder` membangun 3 lantai
4. `interior-designer` merencanakan setiap ruangan
5. `set-dresser` & `detail-architect` mengisi detail
6. `lighting-director` mengatur pencahayaan horor
7. `enemy-designer` membuat monster dengan pathfinding AI
8. `roblox-playtester` & `computer-player` menguji game
9. Bug ditemukan? → diperbaiki otomatis → coba lagi
10. `roblox-publisher` mempublish game ke Roblox

---

## Aturan & Perilaku

| Kondisi | Perilaku AI |
|---|---|
| MCP tidak terdeteksi | **BERHENTI** — minta reconnect, tidak ada workaround |
| Request karakter/map | Selalu tampilkan **preview dulu**, tunggu persetujuan |
| Workspace ada isinya | **Tanya dulu** sebelum hapus apapun |
| Aset tidak ditemukan di Toolbox | Bangun dari primitif, beritahu user |
| Revisi kecil (ganti warna, geser posisi) | Langsung modifikasi tanpa rebuild |
| Revisi besar (ganti rig, ganti tema) | Rebuild dari awal setelah konfirmasi |
| Request ambigu | Tanya **1 pertanyaan** klarifikasi, lalu lanjut |
| Karakter + Map dalam 1 prompt | Handle keduanya sekaligus via `combined-creation` |
| Tidak ada batasan konten | Semua tema, genre, dan jenis karakter didukung |

---

## Struktur File

```
evilsoft-skillblox/
│
├── SKILL.md                              ← Entry point utama skill
│
├── workflows/
│   ├── character-creation.md             ← Alur pembuatan karakter dari gambar
│   ├── map-creation.md                   ← Alur pembuatan map dari gambar/deskripsi
│   ├── combined-creation.md              ← Karakter + map dalam satu sesi
│   ├── new-game.md                       ← Alur membangun game baru lengkap
│   ├── debug-loop.md                     ← Alur debug dan perbaikan bug
│   ├── code-review.md                    ← Review kualitas kode Luau
│   ├── performance-audit.md              ← Audit dan optimasi performa
│   ├── security-audit.md                 ← Audit keamanan game
│   ├── publish-checklist.md              ← Checklist sebelum publish
│   └── monetization-audit.md             ← Audit sistem monetisasi
│
├── references/
│   ├── character-customization.md        ← Teknik modifikasi R6/R15
│   ├── asset-sourcing.md                 ← Panduan mencari aset gratis
│   ├── map-building-from-scratch.md      ← Membangun properti dari primitif
│   ├── mcp-requirements.md               ← Verifikasi koneksi MCP
│   ├── luau-mastery.md                   ← Penguasaan bahasa Luau
│   ├── security-hardening.md             ← Keamanan server & anti-cheat
│   ├── datastore-persistence.md          ← Penyimpanan data pemain
│   ├── combat-systems.md                 ← Sistem combat
│   ├── multiplayer-networking.md         ← Networking & RemoteEvents
│   ├── performance-optimization.md       ← Optimasi performa
│   ├── gui-systems.md                    ← Sistem UI/GUI
│   ├── monetization-systems.md           ← GamePass & DevProduct
│   ├── animation-vfx.md                  ← Animasi & efek visual
│   ├── inventory-systems.md              ← Sistem inventori
│   ├── architecture-patterns.md          ← Pola arsitektur kode
│   ├── mcp-orchestration.md              ← Orkestrasi MCP tools
│   ├── sharp-edges.md                    ← 12 jebakan umum Roblox
│   ├── testing-patterns.md               ← Pola pengujian
│   ├── tooling-ecosystem.md              ← Rojo, Wally, dll.
│   └── game-design-roblox.md             ← Desain game Roblox
│
├── agents/                               ← 21 agen AI dari ClaudeBlox
│   ├── roblox-architect.md
│   ├── luau-scripter.md
│   ├── world-builder.md
│   ├── interior-designer.md
│   ├── set-dresser.md
│   ├── detail-architect.md
│   ├── luau-reviewer.md
│   ├── art-director.md
│   ├── enemy-designer.md
│   ├── lighting-director.md
│   ├── vfx-designer.md
│   ├── sound-designer.md
│   ├── ui-designer.md
│   ├── showcase-photographer.md
│   ├── roblox-playtester.md
│   ├── computer-player.md
│   ├── roblox-publisher.md
│   ├── analytics.md
│   ├── ai-developer.md
│   ├── story-teller.md
│   └── general-purpose-luau-notes.md
│
├── templates/
│   ├── character-preview.md              ← Template preview karakter
│   └── map-preview.md                    ← Template preview map
│
├── gamemaster/
│   ├── state.json                        ← Status progress game
│   ├── architecture.md                   ← Dokumen arsitektur game
│   └── buglist.md                        ← Daftar bug yang ditemukan
│
├── README.md                             ← Dokumentasi ini
└── .gitignore
```

---

## Alur Kerja Lengkap

### Alur Pembuatan Karakter

```
INPUT (Gambar + Deskripsi)
        │
        ▼
Verifikasi MCP ──── Tidak aktif ──→ STOP (minta reconnect)
        │
        ▼ (MCP aktif)
Analisa Karakter
  ├─ Analisa gambar (warna, style, fitur)
  ├─ Cari referensi di internet
  ├─ Cari aksesoris gratis di Roblox Catalog
  └─ Rekomendasi rig R6/R15 + alasan
        │
        ▼
Preview (WAJIB — tidak bisa dilewati)
  ├─ Generate gambar referensi 2D
  └─ Output teks terstruktur:
       • Tipe rig + alasan
       • Warna setiap bagian tubuh (BrickColor)
       • Material
       • Daftar aksesoris + Asset ID
       • Properti buatan sendiri (jika ada)
       • Lokasi penyimpanan
        │
        ▼
Tunggu Persetujuan User
  ├─ "yes" → lanjut build
  ├─ "revisi [apa]" → sesuaikan preview
  └─ "cancel" → batal
        │
        ▼ (disetujui)
Build di Studio (via MCP)
  ├─ Spawn rig default
  ├─ Terapkan warna & material
  ├─ Insert aksesoris dari Catalog
  ├─ Bangun aksesoris custom dari primitif
  └─ Simpan ke ServerStorage/YYYYMMDD_Nama
        │
        ▼
Laporan Lengkap di Chat
  ├─ Lokasi karakter
  ├─ Detail semua modifikasi
  ├─ Script Luau copy-paste ready
  └─ Cara menggunakan karakter di game
```

---

### Alur Pembuatan Map

```
INPUT (Gambar / Layout / Deskripsi)
        │
        ▼
Verifikasi MCP ──── Tidak aktif ──→ STOP
        │
        ▼
Analisa Map
  ├─ Identifikasi tema, zona, properti
  ├─ Cari referensi di internet
  ├─ Cari aset di Roblox Toolbox
  └─ Identifikasi gap (properti yang harus dibuat sendiri)
        │
        ▼
Preview Map (WAJIB)
  ├─ Generate gambar layout bird's-eye
  └─ Teks per zona:
       • Ukuran, tujuan, atmosfer
       • Aset Toolbox (nama + ID)
       • Properti buatan sendiri
       • Rencana pencahayaan
        │
        ▼
Konfirmasi Workspace
  └─ "clear all / clear terrain / keep / cancel"
        │
        ▼
Persetujuan Final
        │
        ▼
Build di Studio
  ├─ Handle workspace sesuai pilihan
  ├─ Bangun struktur dasar (lantai, dinding, langit-langit)
  ├─ Insert aset komunitas
  ├─ Bangun properti custom dari primitif
  ├─ Tambahkan detail interior lengkap
  └─ Atur pencahayaan & efek
        │
        ▼
Laporan Hasil
```

---

## Sumber Skill Ini

Skill ini adalah gabungan dan perluasan dari tiga sumber:

1. **[ClaudeBlox](https://github.com/Claudeblox/claudeblox)** oleh tim ClaudeBlox
   - 21 agen AI khusus
   - Pipeline otonom dari arsitektur hingga publish
   - Digunakan sebagai fondasi untuk pembuatan game lengkap

2. **Roblox Game Skill** — referensi teknis pengembangan Roblox
   - 16 file referensi, 7 workflow
   - Routing table berdasarkan intent
   - Dukungan 3 mode MCP

3. **Evilsoft Visual Creation Engine** — dibuat khusus untuk skill ini
   - Workflow `character-creation.md`
   - Workflow `map-creation.md`
   - Workflow `combined-creation.md`
   - Referensi `character-customization.md`
   - Referensi `asset-sourcing.md`
   - Referensi `map-building-from-scratch.md`
   - Referensi `mcp-requirements.md`
   - Template `character-preview.md` & `map-preview.md`

---

## Troubleshooting

### Skill tidak terdeteksi di Claude Desktop
- Pastikan folder di-copy ke lokasi yang benar: `~/.gemini/config/skills/evilsoft-skillblox/`
- Restart Claude Desktop setelah mengcopy
- Pastikan `SKILL.md` ada di root folder skill

### MCP tidak terkoneksi
- Buka Roblox Studio dengan place yang sudah dipublish
- Aktifkan HTTP Requests: **File → Game Settings → Security → Allow HTTP Requests = On**
- Di Claude Desktop → Settings → Developer → verifikasi MCP Roblox status "Connected"
- Periksa Output di Studio: harus ada tulisan `"The MCP Studio plugin is ready for prompts."`

### Karakter tidak tersimpan di ServerStorage
- Pastikan MCP `execute_luau` berjalan tanpa error
- Cek Output Studio untuk pesan error
- Pastikan place sudah dipublish (MCP memerlukan published place)

### Aset Toolbox gagal diinsert
- Kemungkinan aset memerlukan akun dengan izin khusus
- AI akan otomatis membangun properti dari primitif sebagai gantinya
- Laporan akhir akan mencantumkan aset mana yang gagal dan sudah diganti

---

## Kontribusi

Pull request, issue, dan saran sangat disambut!

Jika Anda ingin menambahkan:
- Workflow baru → buat di `workflows/`
- Referensi teknis baru → buat di `references/`
- Agen khusus baru → buat di `agents/`
- Perbarui `SKILL.md` routing table jika menambahkan workflow baru

---

## License

MIT License — bebas digunakan, dimodifikasi, dan didistribusikan.

---

<p align="center">
  <strong>Dibuat oleh Evilsoft</strong><br/>
  Berdasarkan ClaudeBlox & Roblox Game Skill
</p>
