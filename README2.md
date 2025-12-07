# Kivo

Kivo adalah platform yang bertugas untuk **menemukan ide bisnis untuk anda yang kebingungan mengenai bisnis yang akan datang apakah bisa bertahan atau tidak**, dengan hasil akhir bisa dibuatkan **Business Model Canvas** untuk anda, dengan harapan bisa di jadikan strategi bisnis agar lebih **siap dan kuat**.

Kivo hadir untuk anda yang ingin **menemukan ide bisnis yang relevan untuk yang akan datang**, dengan prediksi yang **berdasarkan data aktual yang akan menjamin bahwa anda tidak perlu ragu lagi mengenai bisnis apa yang akan menjanjikan di masa akan datang.**

<h4 style="text-align:center">Kivo dibuat dengan mengimplementasikan AI Agent yang telah disediakan oleh platform <b>Kolosal AI</b> </h4>

## Repository 


**[kivo frontend](https://github.com/manikandareas/kivo-web)** | **[kivo backend](https://github.com/mhaatha/kivo-api)** | **[kivo raw frontend](https://github.com/b4its/fe-kivo-raw)** | **[kivo raw backend](https://github.com/b4its/be-kivo-raw)**


---

### 🧱 **Arsitektur Teknologi**

#### Frontend (kivo-web):
- **Framework**: Next.js 16 (App Router)
- **Bahasa**: TypeScript
- **UI**: React 19, Tailwind CSS 4, Radix UI
- **AI**: Vercel AI SDK dengan OpenAI
- **Autentikasi**: Clerk
- **Peta**: Mapbox GL
- **State Management**: SWR, nuqs
- **Testing**: Vitest, Testing Library
- **Animasi**: Motion (Framer Motion)

#### Backend (kivo-api):
- **Runtime**: Node.js (LTS)
- **Framework**: Express.js
- **Database**: MongoDB (dengan Docker & replica set)
- **AI Integration**: OpenRouter, Supermemory, Kolosal AI
- **Autentikasi**: Clerk (JWT + Webhook)
- **Validasi**: Zod
- **Testing**: Vitest
- **Dokumentasi API**: OpenAPI (YAML)

---

### 🔐 **Environment Variables Penting**

#### Frontend:
- `NEXT_PUBLIC_API_URL`
- `OPENAI_API_KEY`
- `CLERK_SECRET_KEY` & `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`
- `NEXT_PUBLIC_MAPBOX_ACCESS_TOKEN`

#### Backend:
- `PORT`, `MONGODB_URI`
- `CLERK_*` (3 variabel)
- `OPENROUTER_API_KEY`
- `SUPERMEMORY_API_KEY`
- `KOLOSAL_API_ENDPOINT` & `KOLOSAL_API_KEY`
- `JWT_SECRET`
- `FRONTEND_URL1` (untuk CORS)

---

### 🧪 Fitur Utama

| Fitur | Endpoint | Keterangan |
|-------|----------|------------|
| **AI Chat** | `POST /api/chat` | Konsultasi bisnis dengan AI |
| **Business Model Canvas** | `POST /api/v1/bmc/bmc-routes` | Generate BMC otomatis |
| **Autentikasi** | `POST /api/v1/auth/*` | Clerk-based auth |
| **Peta Interaktif** | `/explore` (frontend) | Explore data bisnis via Mapbox |
| **Protected Routes** | `GET /api/v1/protected/*` | Memerlukan autentikasi |

---

### 🚀 Cara Menjalankan Lokal

#### Backend:
```bash
git clone https://github.com/mhaatha/kivo-api.git
cd kivo-api
npm install
cp .env.example .env
# isi .env dengan kunci yang sesuai
docker-compose up -d
docker exec -it kivo-mongo mongosh --eval "rs.initiate({ _id: 'rs0', members: [{ _id: 0, host: 'localhost:27017' }] })"
npm run dev
```

#### Frontend:
```bash
git clone https://github.com/manikandareas/kivo-web.git
cd kivo-web
npm install
cp .env.example .env.local
# isi .env.local dengan kunci yang sesuai
npm run dev
```

---

### 📁 Struktur Folder (Singkat)

#### Backend:
```
kivo-api/
├── src/
│   ├── app/
│   │   ├── ai/           # Logic AI chat
│   │   ├── controllers/  # Request handler
│   │   ├── models/       # Mongoose schema
│   │   ├── services/     # Business logic
│   │   └── routes/       # API routes
├── tests/
├── api/v1.0.yaml         # OpenAPI spec
└── docker-compose.yaml
```

#### Frontend:
```
kivo-web/
├── app/                  # Next.js App Router
├── features/             # Modul fitur (auth, chat, explore)
├── lib/                  # Utilitas & konfigurasi
└── public/               # Aset statik
```

---

### 📌 Catatan Penting:
- Semua API key wajib diisi untuk fungsi AI dan autentikasi.
- MongoDB wajib dijalankan dengan replica set untuk transaksi.
- Frontend dan backend harus sinkron dalam hal CORS dan Clerk config.
- Ada 2 endpoint BMC: `/api/v1/bmc/bmc-routes` dan `/api/bmc/bmc-routes`.

---

Jika kamu ingin saya bantu cek bug, review kode, atau bantu deploy, beri tahu saja!
