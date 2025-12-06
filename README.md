# Kivo
Kivo adalah platform yang bertugas untuk **menemukan ide bisnis untuk anda yang kebingungan mengenai bisnis yang akan datang apakah bisa bertahan atau tidak**, dengan hasil akhir bisa dibuatkan **Business Model Canvas** untuk anda, dengan harapan bisa di jadikan strategi bisnis agar lebih **siap dan kuat**.

Kivo hadir untuk anda yang ingin **menemukan ide bisnis yang relevan untuk yang akan datang**, dengan prediksi yang **berdasarkan data aktual yang akan menjamin bahwa anda tidak perlu ragu lagi mengenai bisnis apa yang akan menjanjikan di masa akan datang.**

<h4 style="text-align:center">Kivo dibuat dengan mengimplementasikan AI Agent yang telah disediakan oleh platform **Kolosal AI**</h4>
## Repository 
**[kivo frontend](https://github.com/manikandareas/kivo-web)** | **[kivo backend](https://github.com/mhaatha/kivo-api)** | **[kivo raw frontend](https://github.com/b4its/fe-kivo-raw)** | **[kivo raw backend](https://github.com/b4its/be-kivo-raw)**

---

## Teknologi Yang Digunakan
### AI Platform
-  **Kolosal AI**

### Frontend
- **Framework**: Next.js 14+
- **Language**: TypeScript
- **UI Library**: React 18+ dengan Server Components
- **Styling**: Tailwind CSS
- **Font**: Geist Font (Vercel)
- **State Management**: React Context & Server State
- **HTTP Client**: Fetch API & Axios
- **Form Handling**: React Hook Form dengan Zod validation

### Backend
- **Runtime**: Node.js (Latest LTS)
- **Framework**: Express.js
- **Language**: TypeScript
- **Authentication**: Clerk dengan MongoDB Adapter
- **Database**: MongoDB Replica Set (untuk ACID Transactions)
- **Validation**: Zod Schema Validation
- **Security**: CORS, Helmet, Rate Limiting
- **Process Management**: PM2 (production)

## ⚙️ Instalasi & Setup
### Prerequisites
- Node.js (Latest LTS).
- Git.
- MongoDB
- Code Editor: Visual Studio Code

### Frontend Setup (kivo-web)

1. **Clone Repository**
```bash
git clone https://github.com/manikandareas/kivo-web.git
cd kivo-web
```

2. **Install Dependencies**
```bash
npm install
# atau
pnpm install
```

3. **Setup Environment**
```bash
cp .env.example .env.local
# Edit .env.local dengan konfigurasi Anda
```

4. **Run Development Server**
```bash
npm run dev
# Aplikasi akan berjalan di http://localhost:3000
```

### Backend Setup (kivo-api)

1. **Clone Repository**
```bash
git clone https://github.com/mhaatha/kivo-api.git
cd kivo-api
```

2. **Install Dependencies**
```bash
npm install
```

4. **Setup Environment**
```bash
cp .env.example .env
# Sesuaikan .env dengan konfigurasi Anda
# atau jika pakai windows: rename .env.example ke .env
```

5. **Run Start Server**
```bash
npm run start
# API akan berjalan di http://localhost:3001
```
atau

**Run Development Server**
```bash
npm run dev
# API akan berjalan di http://localhost:3001
```

## Fitur Utama

### Authentication System
- **Clerk Auth Integration** - Authentication modern dengan multiple providers
- **Email/Password** - Traditional login dengan email dan password
- **Session Management** - Secure session handling dengan httpOnly cookies
- **Password Reset** - Lupa password dengan email verification

### User Interface
- **Responsive Design** - Mobile-first approach
- **Loading States** - Skeleton loaders dan progress indicators
- **Error Boundaries** - Graceful error handling
- **Form Validation** - Real-time validation dengan Zod

### Dashboard Features
- **User Profile** - Profile management dan settings
- **Dashboard Analytics** - Data visualization dan insights
- **CRUD Operations** - Create, Read, Update, Delete data
- **Search & Filter** - Advanced filtering dan pencarian
- **Generate Business Model Canvas** - Membuat Business Model Canvas menyesuaikan dari ide, dan hasil konsultasi pengguna

### Performance
- **Server-side Rendering (SSR)** - Next.js SSR untuk AI Agent
- **Code Splitting** - Automatic code splitting
- **Image Optimization** - Next.js Image component
- **Caching Strategy** - Redis caching untuk performance
- **PWA Support** - Progressive Web App capabilities

## Struktur Proyek

### Frontend Structure (kivo-web)
```
kivo-web/
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Route group untuk auth pages
│   │   ├── login/                # Login page
│   │   ├── register/             # Register page
│   │   └── forgot-password/      # Forgot password
│   ├── (dashboard)/              # Route group untuk dashboard
│   │   ├── page.tsx              # Dashboard utama
│   │   ├── _components/          # Components khusus dashboard
│   │   └── [id]/                 # Dynamic routes
│   ├── api/                      # API Routes 
│   ├── layout.tsx                # Root layout
│   └── page.tsx                  # Homepage
├── components/                   # Shared components
│   ├── ui/                       # UI components (Button, Card, etc)
│   ├── forms/                    # Form components
│   └── layouts/                  # Layout components
├── lib/                          # Utilities & helpers
│   ├── auth/                     # Auth utilities
│   ├── utils/                    # General utilities
│   └── types/                    # TypeScript types
├── public/                       # Static assets
├── styles/                       # Global styles
└── config/                       # Configuration files
```

### Backend Structure (kivo-api)
```
kivo-api/
├── src/
│   ├── controllers/              # Request handlers
│   │   ├── auth.controller.ts    # Auth controllers
│   │   └── user.controller.ts    # User controllers
│   ├── routes/                   # API routes
│   │   ├── auth.routes.ts        # Auth routes
│   │   └── user.routes.ts        # User routes
│   ├── middleware/               # Custom middleware
│   │   ├── auth.middleware.ts    # Auth validation
│   │   └── error.middleware.ts   # Error handling
│   ├── services/                 # Business logic
│   │   ├── auth.service.ts       # Auth business logic
│   │   └── user.service.ts       # User business logic
│   ├── models/                   # Database models
│   │   ├── user.model.ts         # User schema
│   │   └── session.model.ts      # Session schema
│   ├── lib/                      # Shared libraries
│   │   ├── auth.ts               # Better Auth setup
│   │   ├── database.ts           # MongoDB connection
│   │   └── validation.ts         # Schema validations
│   └── types/                    # TypeScript definitions
├── docker-compose.yml            # MongoDB Replica Set setup
├── .env.example                  # Environment template
└── package.json                  # Dependencies
```

## Frontend Detail
### Next.js App Router Architecture
```typescript
// app/layout.tsx - Root Layout
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className={inter.className}>
        <AuthProvider>
          <Toaster />
          {children}
        </AuthProvider>
      </body>
    </html>
  )
}
```

### Server Components Example
```typescript
// app/dashboard/page.tsx - Server Component
export default async function DashboardPage() {
  const session = await getServerSession()
  
  if (!session) {
    redirect('/login')
  }
  
  const data = await getDashboardData(session.user.id)
  
  return (
    <DashboardClient 
      initialData={data} 
      user={session.user} 
    />
  )
}
```

## Backend Detail

### Express Server Setup
```typescript
import 'dotenv/config';
import mongoose from 'mongoose';
import app from './app/index.js';
// Routes from main branch
import databasesRouter from './app/routes/db.route.js';
import bmcRouteRouter from './app/routes/bmc.route.js';
import authRouter from './app/routes/auth.route.js';
import protectedRouter from './app/routes/protected.route.js';
// Routes from feat/ai-chat branch
import aiRouter from './app/routes/ai.js';
import bmcRouter from './app/routes/bmc.js';

// PORT env section
const port = process.env.PORT;

if (!port) {
  console.error('error: PORT environment variable is missing.');
  process.exit(1);
}

if (isNaN(port)) {
  console.error('error: PORT must be a number.');
  process.exit(1);
}

// MongoDB connection
const mongoUri = process.env.MONGODB_URI;
if (!mongoUri) {
  console.error('error: MONGODB_URI environment variable is missing.');
  process.exit(1);
}

mongoose
  .connect(mongoUri)
  .then(() => {
    console.log('✅ MongoDB connected successfully');
    console.log(`📡 Database: ${mongoose.connection.name}`);
  })
  .catch((err) => {
    console.error('❌ MongoDB connection error:', err);
    process.exit(1);
  });

// Routes from main branch
app.use('/api/v1/databases', databasesRouter);
app.use('/api/v1/bmc', bmcRouteRouter);
app.use('/api/v1/auth', authRouter);
app.use('/api/v1/protected', protectedRouter);

// Routes from feat/ai-chat branch (AI Chat & BMC management)
app.use('/api/chat', aiRouter);
app.use('/api/chats', aiRouter);
app.use('/api/bmc', bmcRouter);

app.listen(port, '0.0.0.0', () => {
  console.log(`Server is running on port ${port}`);
});
```

## Integrasi Frontend-Backend
### API Service Layer
```typescript
// lib/api/client.ts
class ApiClient {
  private baseURL = process.env.NEXT_PUBLIC_API_URL
  
  async request(endpoint: string, options?: RequestInit) {
    const response = await fetch(`${this.baseURL}${endpoint}`, {
      ...options,
      credentials: 'include', // Include cookies
      headers: {
        'Content-Type': 'application/json',
        ...options?.headers,
      },
    })
    
    if (!response.ok) {
      throw new Error(`API Error: ${response.status}`)
    }
    
    return response.json()
  }
  
  // Auth methods
  async login(email: string, password: string) {
    return this.request('/api/auth/sign-in/email', {
      method: 'POST',
      body: JSON.stringify({ email, password })
    })
  }
  
  async getSession() {
    return this.request('/api/auth/session')
  }
}

export const apiClient = new ApiClient()
```

## Library & Dependencies

### Frontend Dependencies
```json
{
  "dependencies": {
    "next": "^14.0.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "typescript": "^5.0.0",
    "tailwindcss": "^3.3.0",
    "geist": "^1.0.0",
    "zod": "^3.22.0",
    "react-hook-form": "^7.47.0",
    "@hookform/resolvers": "^3.3.0",
    "sonner": "^1.0.0",
    "lucide-react": "^0.290.0"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "@types/react": "^18.2.0",
    "eslint": "^8.0.0",
    "prettier": "^3.0.0"
  }
}
```

### Backend Dependencies
```json
{
  "dependencies": {
    "express": "^4.18.0",
    "better-auth": "^0.5.0",
    "mongodb": "^6.0.0",
    "mongoose": "^8.0.0",
    "cors": "^2.8.5",
    "dotenv": "^16.3.0",
    "zod": "^3.22.0",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.0"
  },
  "devDependencies": {
    "@types/express": "^4.17.0",
    "@types/node": "^20.0.0",
    "nodemon": "^3.0.0",
    "ts-node": "^10.9.0",
    "typescript": "^5.0.0"
  }
}
```

## Deployment

### Frontend Deployment (Vercel)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod

# Setup environment variables di Vercel dashboard
```

### Backend Deployment (Railway/Render)
```bash
# Build untuk production
npm run build

# Start production server
npm start

# Setup environment variables di platform
```

## Tim Oryphem
Proyek ini dikembangkan oleh tim **ORYPHEM** dalam kompetisi hackathon yang diadakan oleh **IMPHNEN**: Ingin Menjadi Programmer Handal Namun Enggan Ngoding:
### Developer
- **Frontend Developer**: [manikandareas](https://github.com/manikandareas): Vito Andareas Manik
- **Backend Developer**: [mhaatha](https://github.com/mhaatha), [b4its](https://github.com/b4its), dan [Chaos09](https://github.com/Chaos09): M Hafidz Athaya, Baits Rika Saputra, dan Irfan Noor Hidayat
### Designer
-  **UI/UX Designer**: Raihan Akbar Ramadhan

## Lisensi

Proyek ini dilisensikan di bawah **MIT License** - [LICENSE](LICENSE) untuk detailnya.

---

<div align="center">
  
### ⭐ Jika Anda menyukai proyek ini, berikan bintang di GitHub!
**[Star kivo](https://github.com/b4its/kivo)** | **[Star kivo-web](https://github.com/manikandareas/kivo-web)** | **[Star kivo-api](https://github.com/mhaatha/kivo-api)** | **[Star fe-kivo-raw](https://github.com/b4its/fe-kivo-raw)** | **[Star be-kivo-raw](https://github.com/b4its/be-kivo-raw)**

</div>

---
