# security-db
# 🔐 Security Database — Jasher Bot

Repository ini digunakan sebagai database token yang diizinkan untuk menjalankan **Jasher Bot**.

> **⚠️ Repo ini harus PUBLIC** agar bot bisa mengaksesnya saat startup.

---

## 📄 Format `allowed_tokens.json`

```json
{
  "tokens": [
    "TOKEN_BOT_1",
    "TOKEN_BOT_2"
  ],
  "blocked": [
    "TOKEN_YANG_DIBLOKIR"
  ]
}
```

| Field | Keterangan |
|-------|------------|
| `tokens` | Daftar token bot yang **diizinkan** berjalan |
| `blocked` | Daftar token yang **diblokir** (override whitelist) |

---

## 🔄 Cara Kerja

Saat bot dijalankan (`npm start`), bot akan:

1. Fetch file `allowed_tokens.json` dari repo ini via raw GitHub URL
2. Cek apakah token bot ada di list `blocked` → jika ya, **bot berhenti**
3. Cek apakah token bot ada di list `tokens` → jika tidak ada, **bot berhenti**
4. Jika token valid → bot berjalan normal ✅

---

## 🔗 Raw URL untuk Config Bot

Ganti `USERNAME` dan `REPO` sesuai milikmu:

```
https://raw.githubusercontent.com/USERNAME/REPO/main/allowed_tokens.json
```

Paste URL ini ke variabel `SECURITY_DB_URL` di `Azmi.js`.

---

## ➕ Cara Tambah Token Baru

Edit file `allowed_tokens.json`, tambahkan token ke array `tokens`:

```json
{
  "tokens": [
    "TOKEN_LAMA",
    "TOKEN_BARU_DI_SINI"
  ],
  "blocked": []
}
```

Commit & push — perubahan langsung aktif tanpa restart server apapun.

---

## 🚫 Cara Blokir Token

Pindahkan token dari `tokens` ke `blocked`:

```json
{
  "tokens": [],
  "blocked": [
    "TOKEN_YANG_MAU_DIBLOKIR"
  ]
}
```

Bot yang menggunakan token tersebut akan **langsung ditolak** saat next restart.

---

*Dibuat untuk Jasher Bot by @AboutAzmii*

