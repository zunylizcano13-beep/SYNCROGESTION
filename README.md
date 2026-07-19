
import type { Config } from 'tailwindcss';

const config: Config = {
  content: ['./app/**/*.{ts,tsx}', './components/**/*.{ts,tsx}'],
  theme: { extend: {} },
  plugins: [],
};

export default config;

{
  "compilerOptions": {
    "target": "ES2017",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}

NEXT_PUBLIC_SUPABASE_URL=https://tu-proyecto.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=tu-anon-key

{
  "name": "syncrogestion",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "14.2.5",
    "react": "18.3.1",
    "react-dom": "18.3.1",
    "@supabase/supabase-js": "2.45.0",
    "@supabase/ssr": "0.4.0"
  },
  "devDependencies": {
    "typescript": "5.5.4",
    "@types/node": "20.14.0",
    "@types/react": "18.3.3",
    "@types/react-dom": "18.3.0",
    "tailwindcss": "3.4.7",
    "postcss": "8.4.40",
    "autoprefixer": "10.4.19"
  }
}

module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};

# SyncroGestión — MVP (Módulo 1)

Plataforma SaaS para implementar y administrar el SG-SST en Colombia.
Este es el andamiaje inicial: base de datos multiempresa y el asistente
de configuración de empresa (Módulo 1) funcionando de extremo a extremo.

## Cómo ponerlo en línea (sin experiencia previa en DevOps)

### 1. Crear el proyecto en Supabase (base de datos + autenticación)
1. Ve a https://supabase.com y crea una cuenta gratuita.
2. Crea un nuevo proyecto (elige la región más cercana, ej. São Paulo).
3. En el panel izquierdo, ve a **SQL Editor** → **New query**.
4. Copia y pega el contenido completo de `supabase/migrations/0001_core_schema.sql`
   y ejecútalo (botón Run). Esto crea todas las tablas, catálogos y reglas
   de seguridad del Módulo 1.
5. Ve a **Project Settings → API** y copia:
   - `Project URL`
   - `anon public key`

### 2. Configurar el proyecto localmente
```bash
npm install
cp .env.example .env.local
# pega tu Project URL y anon key en .env.local
npm run dev
```
Abre http://localhost:3000/onboarding para ver el asistente funcionando.

### 3. Publicarlo en internet (Vercel)
1. Sube este proyecto a un repositorio de GitHub.
2. Ve a https://vercel.com, inicia sesión con GitHub e importa el repositorio.
3. En "Environment Variables" pega las mismas dos variables de `.env.local`.
4. Click en "Deploy". En unos minutos tendrás una URL pública real
   (ej. `syncrogestion.vercel.app`) donde cualquiera puede probar el
   asistente de configuración.

## Qué incluye esta primera versión
- Esquema de base de datos multiempresa con aislamiento real por
  organización (row level security) — sección 4.5 y 20 del documento maestro.
- Catálogos base (clases de riesgo, roles, modalidades de trabajo).
- Asistente de configuración de empresa (Módulo 1) con 6 pasos, conectado
  a la base de datos real: al finalizar, crea la empresa, la sede y la
  caracterización de riesgos.

## Qué sigue
- Módulo 2: Diagnóstico inteligente (clasificación normativa y evaluación).
- Autenticación (registro / inicio de sesión) — actualmente el asistente
  asume que ya existe una sesión de Supabase Auth activa.
- Dashboard con semáforos de cumplimiento.
