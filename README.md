# 🚆 RailRoute — Live Indian Train Tracker

> **A modern, high-performance web application for real-time tracking, analytics, terrain intelligence, and weather monitoring of Indian Railways trains.**

[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=flat&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.5-blue?style=flat&logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-3.4-38bdf8?style=flat&logo=tailwindcss)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](#-license)

---

## 📖 Overview

**RailRoute** is a modern, high-performance web application designed for **real-time tracking of Indian Railways trains**.

It combines live train tracking, interactive vector maps, delay analytics, route elevation profiles, terrain and point-of-interest detection, and live weather intelligence into a unified dashboard.

The application is designed to provide a rich railway journey experience while remaining usable even when external API keys are unavailable through its **zero-config fallback mode**.

---

## ✨ Features

### 🚆 Live GPS Train Tracking

View:

- Real-time train movement
- Current speed
- Delay status
- Next halt
- Estimated time of arrival

---

### 🗺️ Interactive Vector Maps

Smooth, hardware-accelerated mapping powered by [MapLibre GL](https://maplibre.org/).

The map provides:

- Real-time train positioning
- Railway routes
- Station halts
- Interactive map navigation

---

### 🔎 Instant Train Search

Search over thousands of Indian trains by:

- Train number
- Train name

Search uses the bundled local train database, providing fast results with **zero API latency**.

---

### ⛰️ Route Elevation Profile

Visualize altitude changes throughout the journey.

The elevation profile helps identify:

- Ghats
- Plains
- Mountain passes
- Changes in railway elevation

---

### 🏔️ Terrain & POI Intelligence

Automatically detect important geographical and railway-related points along the railway corridor, including:

- Landmarks
- Railway bridges
- Tunnels
- River crossings

---

### 🌦️ Live Station Weather

View real-time weather information for key stations, including:

- Temperature
- Humidity
- Current weather conditions

---

### ⭐ Favorites & Offline Sync

Save frequently tracked trains using persistent client-side storage powered by **Zustand**.

Favorites remain available without requiring repeated API requests.

---

### 📴 Zero-Config Fallback Mode

RailRoute can run without external API keys.

When API keys are not provided, the application automatically falls back to:

- Bundled realistic mock data
- Offline train database
- Built-in fallback behavior

This means the application remains usable during development without requiring immediate API configuration.

---

# 🛠️ Tech Stack

| Category | Technology |
|---|---|
| **Framework** | [Next.js 14](https://nextjs.org/) |
| **Architecture** | App Router, Server Components & Route Handlers |
| **Language** | [TypeScript](https://www.typescriptlang.org/) |
| **Styling** | [Tailwind CSS](https://tailwindcss.com/) |
| **UI Design** | Custom Glassmorphism System |
| **Animations** | [Framer Motion](https://www.framer.com/motion/) |
| **Icons** | [Lucide React](https://lucide.dev/) |
| **State Management** | [Zustand](https://github.com/pmndrs/zustand) |
| **Data Fetching & Caching** | [TanStack React Query v5](https://tanstack.com/query) + Server-side in-memory cache |
| **Map Engine** | [MapLibre GL](https://maplibre.org/) |

---

# 🏗️ Application Architecture

RailRoute follows a modular Next.js architecture where the application is divided into:

```text
                     ┌─────────────────────────┐
                     │      RailRoute UI       │
                     │                         │
                     │  Next.js + TypeScript   │
                     └────────────┬────────────┘
                                  │
                                  ▼
                     ┌─────────────────────────┐
                     │     Feature Modules     │
                     │                         │
                     │ Maps / Analytics        │
                     │ Weather / Terrain       │
                     │ Favorites               │
                     └────────────┬────────────┘
                                  │
                                  ▼
                     ┌─────────────────────────┐
                     │      Next.js APIs       │
                     │     Route Handlers      │
                     └────────────┬────────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                   │
              ▼                   ▼                   ▼
       ┌────────────┐      ┌────────────┐      ┌────────────┐
       │ RailRadar  │      │ OpenWeather│      │ OpenTopo-  │
       │            │      │            │      │ graphy     │
       │ Live Train │      │ Station    │      │ Elevation  │
       │ Tracking   │      │ Weather    │      │ Data       │
       └────────────┘      └────────────┘      └────────────┘
              │                   │                   │
              └───────────────────┼───────────────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │     Overpass    │
                         │ OpenStreetMap   │
                         │ Terrain / POIs  │
                         └─────────────────┘
```

---

# 📁 Project Structure

The project is organized into clear layers so that a new developer can quickly understand where each part of the application lives.

```text
RailRoute/
│
├── 📁 app/
│   │
│   ├── 📁 api/
│   │   ├── 📁 analytics/[id]/
│   │   │   └── Elevation profile & delay analytics
│   │   │
│   │   ├── 📁 search/
│   │   │   └── Train lookup endpoint
│   │   │
│   │   ├── 📁 terrain/
│   │   │   └── Overpass POI & landmark detection
│   │   │
│   │   ├── 📁 train/[id]/
│   │   │   └── Live journey tracking
│   │   │
│   │   └── 📁 weather/
│   │       └── OpenWeather station conditions
│   │
│   ├── 📁 favorites/
│   │   └── Bookmarked trains page
│   │
│   ├── 📁 train/[id]/
│   │   └── Dedicated train dashboard & live map
│   │
│   ├── 📄 layout.tsx
│   │   └── Root HTML shell, providers & navigation
│   │
│   └── 📄 page.tsx
│       └── Homepage with hero search & quick links
│
├── 📁 components/
│   │
│   ├── 📁 journey/
│   │   └── Delay badges, timeline, journey cards
│   │
│   ├── 📁 layout/
│   │   └── Navbar, bottom mobile bar
│   │
│   └── 📁 ui/
│       └── Skeletons, empty states, error cards
│
├── 📁 config/
│   └── Environment variable access & defaults
│
├── 📁 features/
│   │
│   ├── 📁 analytics/
│   │   └── Elevation chart & stats dashboard
│   │
│   ├── 📁 favorites/
│   │   └── Favorite bookmark toggle
│   │
│   ├── 📁 maps/
│   │   └── MapLibre live vector map viewer
│   │
│   ├── 📁 terrain/
│   │   └── Landmarks, bridges & tunnel cards
│   │
│   └── 📁 weather/
│       └── Station weather overview panels
│
├── 📁 hooks/
│   ├── useLiveJourney
│   └── useTrainSearch
│
├── 📁 lib/
│   │
│   ├── 📄 cache.ts
│   │   └── In-memory TTL caching layer
│   │
│   ├── 📄 opentopography.ts
│   │   └── Global DEM altitude queries
│   │
│   ├── 📄 openweather.ts
│   │   └── OpenWeather API integration
│   │
│   ├── 📄 overpass.ts
│   │   └── OpenStreetMap Overpass client with timeout
│   │
│   ├── 📄 railradar.ts
│   │   └── RailRadar live GPS tracking integration
│   │
│   └── 📄 trains-db.ts
│       └── Bundled Indian Railways offline database
│
├── 📁 store/
│   └── Zustand client-side stores
│       ├── Favorites
│       ├── Search
│       └── Journey
│
├── 📁 styles/
│   └── Tailwind & global stylesheet definitions
│
├── 📁 types/
│   └── TypeScript domain definitions
│
└── 📁 utils/
    └── Helper formatting functions & class combiner (cn)
```

---

# 🧭 Understanding the Project Structure

If you're new to the project, think of the directories like this:

```text
app/
    ↓
Pages + API endpoints

components/
    ↓
Reusable UI components

features/
    ↓
Actual application features

hooks/
    ↓
Reusable React logic

lib/
    ↓
External APIs + data + caching

store/
    ↓
Client-side application state

styles/
    ↓
Global styling

types/
    ↓
TypeScript data definitions

utils/
    ↓
Small reusable helper functions
```

### Simple Mental Model

> **Pages → Components → Features → Hooks/State → APIs & Libraries**

---

# 🔄 Data Flow

A typical live train tracking request follows this flow:

```text
User searches for a train
          │
          ▼
     Search UI
          │
          ▼
   Local Train Database
          │
          ▼
   Train ID / Number
          │
          ▼
   Next.js API Route
          │
          ▼
     RailRadar API
          │
          ▼
   Server-side Cache
          │
          ▼
     Train Status
          │
          ▼
      Train UI
          │
          ▼
   MapLibre Map
```

Additional information is fetched independently:

```text
Train Route
    │
    ├──► OpenTopography
    │       └── Elevation
    │
    ├──► Overpass / OpenStreetMap
    │       └── Terrain + POIs
    │
    └──► OpenWeather
            └── Station Weather
```

---

# 🚀 Getting Started

## 1. Prerequisites

Before running RailRoute, make sure you have:

- **Node.js 18.17+**
- **npm**

**Node.js 20 or 22 is recommended.**

Check your installed versions:

```bash
node -v
npm -v
```

You should see something similar to:

```text
v20.x.x
10.x.x
```

---

# 📥 Installation

## 2. Clone or Open the Project

Open a terminal and navigate to the project directory:

```bash
cd RailRoute
```

If you cloned the repository using Git, for example:

```bash
git clone <your-repository-url>
cd RailRoute
```

> Replace `<your-repository-url>` with your GitHub repository URL.

---

## 3. Install Dependencies

Run:

```bash
npm install
```

This installs all required frontend and server-side dependencies.

---

# 🔐 Environment Variables

## 4. Create `.env.local`

RailRoute can run without API keys, but you can configure external services when required.

Copy the example environment file:

```bash
cp .env.example .env.local
```

### Windows PowerShell

If you're using PowerShell:

```powershell
Copy-Item .env.example .env.local
```

Then open:

```text
.env.local
```

and configure the API keys.

```env
# RailRadar API — Live Indian Railways GPS Tracking
RAILRADAR_API_KEY=

# MapTiler API — Custom Vector Vector Map Styles (Client-safe)
NEXT_PUBLIC_MAPTILER_API_KEY=

# OpenWeather API — Live Station Weather Conditions
OPENWEATHER_API_KEY=

# OpenTopography API — SRTM Global Elevation Profiles
OPENTOPOGRAPHY_API_KEY=

# Upstash Redis (Optional for persistent caching)
UPSTASH_REDIS_REST_URL=
UPSTASH_REDIS_REST_TOKEN=
```

---

## 🔑 API Keys Are Optional

You **do not need API keys to start development**.

When the keys are left blank, RailRoute automatically falls back to:

- Realistic mock data
- Bundled offline train database
- Built-in fallback functionality

Therefore, a new developer can install the project and start exploring the application immediately.

---

# ▶️ Running the Development Server

## 5. Start RailRoute

Run:

```bash
npm run dev
```

You should see something similar to:

```text
▲ Next.js 14

- Local: http://localhost:3000
```

Open your browser and visit:

### 🚆 RailRoute

```text
http://localhost:3000
```

---

# ⚡ Complete Setup — Quick Version

If you just want to get the application running as quickly as possible:

```bash
cd RailRoute
npm install
npm run dev
```

Then open:

```text
http://localhost:3000
```

That's it.

**API keys are optional during development.**

---

# 📜 Available Scripts

| Script | Command | Purpose |
|---|---|---|
| **Development** | `npm run dev` | Starts the hot-reloading development server on port 3000 |
| **Build** | `npm run build` | Compiles an optimized production build |
| **Start** | `npm run start` | Runs the compiled production build |
| **Lint** | `npm run lint` | Runs ESLint checks across the codebase |

---

# 🏭 Production Build

To create an optimized production build:

```bash
npm run build
```

After the build completes:

```bash
npm run start
```

The production application will then be available at:

```text
http://localhost:3000
```

---

# 📊 Performance & Caching

RailRoute uses multiple strategies to reduce unnecessary API requests and improve responsiveness.

## ⚡ Server-Side In-Memory Cache

Different types of data use different cache durations:

| Data | Cache Duration |
|---|---:|
| **Live train status** | 30 seconds |
| **Weather queries** | 15 minutes |
| **Terrain / elevation data** | 24 hours |

This reduces unnecessary external API consumption while keeping frequently changing information reasonably fresh.

---

## 🔎 Offline Fast Search

The train search system uses the indexed client-side database:

```text
lib/trains-db.ts
```

This provides train search without requiring a network request for every search.

The search is designed to return results in:

```text
< 1ms
```

with zero network overhead.

---

## 🗺️ Dynamic Map Loading

MapLibre GL is dynamically loaded using:

```text
next/dynamic
```

with:

```text
ssr: false
```

This helps:

- Minimize the initial bundle size
- Prevent server-side WebGL errors
- Load the map only when required

---

# 🧩 Core Application Modules

## 🚆 Train Tracking

Located primarily in:

```text
features/
└── maps/
```

and:

```text
lib/railradar.ts
```

Responsible for live GPS train tracking and map positioning.

---

## 📈 Analytics

Located in:

```text
features/analytics/
```

Provides:

- Elevation charts
- Journey statistics
- Delay analytics

---

## 🏔️ Terrain Intelligence

Located in:

```text
features/terrain/
```

and:

```text
lib/overpass.ts
```

Responsible for identifying:

- Landmarks
- Bridges
- Tunnels
- River crossings

along the railway corridor.

---

## 🌦️ Weather

Located in:

```text
features/weather/
```

and:

```text
lib/openweather.ts
```

Provides weather information for important stations along the route.

---

## ⭐ Favorites

Located in:

```text
features/favorites/
```

and:

```text
store/
```

Uses Zustand for client-side state and persistent favorite-train management.

---

# 🔌 API Integrations

RailRoute integrates with several external services.

| Service | Purpose |
|---|---|
| **RailRadar** | Live Indian Railways GPS tracking |
| **MapTiler** | Custom vector map styles |
| **OpenWeather** | Station weather conditions |
| **OpenTopography** | SRTM global elevation profiles |
| **OpenStreetMap Overpass** | Terrain and POI detection |
| **Upstash Redis** | Optional persistent caching |

---

# 🗂️ API Routes

The Next.js App Router contains the following server-side API routes:

```text
app/api/
│
├── analytics/[id]/
│   └── Elevation profile & delay analytics
│
├── search/
│   └── Train lookup
│
├── terrain/
│   └── POI & landmark detection
│
├── train/[id]/
│   └── Live journey tracking
│
└── weather/
    └── Station weather conditions
```

---

# 🧑‍💻 Recommended Development Path

If you're opening RailRoute for the first time and want to understand the codebase, follow this order.

### 1️⃣ Start with the Homepage

```text
app/page.tsx
```

Understand how the main user experience begins.

### 2️⃣ Understand the Root Application

```text
app/layout.tsx
```

This contains the root HTML shell, providers, and navigation.

### 3️⃣ Explore Reusable Components

```text
components/
```

Understand how the UI is divided into reusable pieces.

### 4️⃣ Explore Features

```text
features/
```

This is where the major application functionality is organized.

### 5️⃣ Explore API Integrations

```text
lib/
```

Pay particular attention to:

```text
railradar.ts
openweather.ts
opentopography.ts
overpass.ts
cache.ts
trains-db.ts
```

### 6️⃣ Explore State Management

```text
store/
```

Understand how favorites, search, and journey state are managed.

### 7️⃣ Explore Types

```text
types/
```

This will help you understand the application's TypeScript domain models.

---

# 🧭 New Developer Workflow

For someone completely new to the project:

```text
                    START
                      │
                      ▼
              Read README.md
                      │
                      ▼
                npm install
                      │
                      ▼
                npm run dev
                      │
                      ▼
          Open localhost:3000
                      │
                      ▼
             Explore the UI
                      │
                      ▼
              app/page.tsx
                      │
                      ▼
              components/
                      │
                      ▼
               features/
                      │
                      ▼
                  lib/
                      │
                      ▼
              API clients
                      │
                      ▼
             Modify / Extend
```

---

# 🔍 Important Files at a Glance

| File / Directory | What to Understand |
|---|---|
| `app/page.tsx` | Homepage |
| `app/layout.tsx` | Root application shell |
| `app/api/` | Server-side API routes |
| `features/maps/` | Live MapLibre map |
| `features/analytics/` | Elevation & analytics |
| `features/terrain/` | Terrain & POIs |
| `features/weather/` | Weather UI |
| `features/favorites/` | Favorites functionality |
| `lib/railradar.ts` | Live train API |
| `lib/openweather.ts` | Weather API |
| `lib/opentopography.ts` | Elevation API |
| `lib/overpass.ts` | Terrain / POI API |
| `lib/cache.ts` | Server-side caching |
| `lib/trains-db.ts` | Offline train database |
| `store/` | Zustand state |
| `types/` | TypeScript definitions |
| `utils/` | Shared helper functions |

---

# 🧪 Before Opening a Pull Request

Before submitting changes, run:

```bash
npm run lint
```

Then create a production build:

```bash
npm run build
```

If both complete successfully, start the production build:

```bash
npm run start
```

---

# 🚀 Quick Command Reference

| Task | Command |
|---|---|
| Install dependencies | `npm install` |
| Start development | `npm run dev` |
| Run lint | `npm run lint` |
| Create production build | `npm run build` |
| Start production build | `npm run start` |

---

# 🌐 Local URLs

When running the development server:

| Service | URL |
|---|---|
| 🚆 **RailRoute** | `http://localhost:3000` |
| 🔌 **Next.js API Routes** | `http://localhost:3000/api/...` |

---

# 📄 License

This project is licensed under the **MIT License**.

---

# ⭐ Project Highlights

- 🚆 Real-time Indian Railways train tracking
- 📍 Live GPS train positioning
- 🗺️ Interactive MapLibre vector maps
- 🔎 Offline train search
- 📈 Route elevation profiles
- 🏔️ Terrain and POI intelligence
- 🌉 Railway bridge and tunnel detection
- 🌊 River crossing detection
- 🌦️ Live station weather
- ⭐ Favorite train management
- 📴 Zero-config fallback mode
- ⚡ Server-side caching
- 🚀 Next.js App Router
- 🔷 TypeScript
- 🎨 Tailwind CSS + Glassmorphism
- 🎬 Framer Motion animations
- 🐻 Zustand state management
- 📊 TanStack React Query
- 🗃️ Bundled offline train database

---

# 🚆 RailRoute

> **Track smarter. Travel better.**

RailRoute brings **live train tracking, maps, analytics, terrain intelligence, and weather** together into one modern Indian Railways experience.