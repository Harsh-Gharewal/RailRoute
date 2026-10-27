# 🚆 RailRoute — Live Indian Train Tracker

> A modern, high-performance web application for real-time tracking, analytics, terrain intelligence, and weather monitoring of Indian Railways trains.

[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=flat&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.5-blue?style=flat&logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-3.4-38bdf8?style=flat&logo=tailwindcss)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](#-license)

## 🌐 Live Demo

### [🚆 Explore RailRoute](https://railroute-tau.vercel.app/)

Experience the deployed application: [https://railroute-tau.vercel.app/](https://railroute-tau.vercel.app/)

---

## 📖 Overview

**RailRoute** is a modern web application designed for real-time tracking of Indian Railways trains. It combines live train tracking, interactive vector maps, delay analytics, route elevation profiles, terrain and point-of-interest (POI) detection, and live weather intelligence into a unified dashboard.

The application provides a rich railway journey experience while remaining usable during development without external API keys through its zero-configuration fallback mode.

## ✨ Features

### 🚆 Live GPS Train Tracking
- Real-time train movement
- Current speed and delay status
- Next halt and estimated time of arrival (ETA)

### 🗺️ Interactive Vector Maps
- Smooth, hardware-accelerated mapping powered by [MapLibre GL](https://maplibre.org/)
- Real-time train positioning
- Railway routes and station halts
- Interactive map navigation

### 🔎 Instant Train Search
- Search thousands of Indian trains by number or name
- Bundled local train database
- Fast search without a network request for each query

### ⛰️ Route Elevation Profile
- Visualize altitude changes along a journey
- Explore ghats, plains, and mountain passes
- Understand elevation changes along railway routes

### 🏔️ Terrain & POI Intelligence
- Landmark detection
- Railway bridge identification
- Tunnel detection
- River crossing identification

### 🌦️ Live Station Weather
- Real-time temperature
- Humidity
- Current weather conditions for key stops

### ⭐ Favorites & Offline Sync
- Save frequently tracked trains
- Persistent client-side storage using Zustand
- Access saved favorites without repeatedly searching for them

### 📴 Zero-Config Fallback Mode
- Built-in realistic mock data
- Bundled offline train database
- Fallback behavior when API keys are not configured

> **Note:** Fallback data is intended to keep the interface usable during development. It should not be treated as verified live railway information.

---

## 🛠️ Tech Stack

| Category | Technology |
|---|---|
| Framework | [Next.js 14](https://nextjs.org/) |
| Architecture | App Router, Server Components & Route Handlers |
| Language | [TypeScript](https://www.typescriptlang.org/) |
| Styling | [Tailwind CSS](https://tailwindcss.com/) |
| UI Design | Custom Glassmorphism System |
| Animations | [Framer Motion](https://www.framer.com/motion/) |
| Icons | [Lucide React](https://lucide.dev/) |
| State Management | [Zustand](https://github.com/pmndrs/zustand) |
| Data Fetching & Caching | [TanStack React Query v5](https://tanstack.com/query) + server-side in-memory cache |
| Map Engine | [MapLibre GL](https://maplibre.org/) |
| Live Train Tracking | RailRadar |
| Weather | OpenWeather |
| Elevation | OpenTopography |
| Terrain / POI | OpenStreetMap Overpass |
| Optional Persistent Cache | Upstash Redis |

---

## 🏗️ Application Architecture

RailRoute follows a modular Next.js architecture that separates the user interface, feature modules, API routes, and external data providers.

```text
                      ┌────────────────────────┐
                      │     RailRoute UI       │
                      │                        │
                      │ Next.js + TypeScript   │
                      └───────────┬────────────┘
                                  │
                                  ▼
                      ┌────────────────────────┐
                      │    Feature Modules     │
                      │                        │
                      │ Maps / Analytics       │
                      │ Weather / Terrain      │
                      │ Favorites              │
                      └───────────┬────────────┘
                                  │
                                  ▼
                      ┌────────────────────────┐
                      │      Next.js APIs      │
                      │     Route Handlers     │
                      └───────────┬────────────┘
                                  │
                 ┌────────────────┼────────────────┐
                 │                │                │
                 ▼                ▼                ▼
          ┌────────────┐   ┌────────────┐   ┌─────────────┐
          │ RailRadar  │   │ OpenWeather│   │OpenTopography│
          │            │   │            │   │             │
          │ Live Train │   │ Station    │   │ Elevation   │
          │ Tracking   │   │ Weather    │   │ Data        │
          └────────────┘   └────────────┘   └─────────────┘
                 │                │                │
                 └────────────────┼────────────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │ OpenStreetMap   │
                         │ Overpass API    │
                         │ Terrain / POIs  │
                         └─────────────────┘
```

---

## 📁 Project Structure

The project is organized into modular directories to make the codebase easier to explore and maintain.

```text
RailRoute/
│
├── app/                            # Next.js App Router
│   ├── api/                        # Server-side API endpoints
│   │   ├── analytics/[id]/         # Elevation profile & delay analytics
│   │   ├── search/                 # Train lookup endpoint
│   │   ├── terrain/                # POI & landmark detection
│   │   ├── train/[id]/             # Live journey tracking
│   │   └── weather/                # Station weather conditions
│   │
│   ├── favorites/                  # Bookmarked trains page
│   ├── train/[id]/                 # Train dashboard & live map
│   ├── layout.tsx                  # Root HTML shell, providers & navigation
│   └── page.tsx                    # Homepage, hero search & quick links
│
├── components/                     # Shared UI components
│   ├── journey/                    # Delay badges, timeline & journey cards
│   ├── layout/                     # Navbar & bottom mobile bar
│   └── ui/                         # Skeletons, empty states & error cards
│
├── config/                         # Environment variable access & defaults
│
├── features/                       # Core application features
│   ├── analytics/                  # Elevation chart & statistics dashboard
│   ├── favorites/                  # Favorite bookmark toggle
│   ├── maps/                       # MapLibre live vector map viewer
│   ├── terrain/                    # Landmarks, bridges & tunnel cards
│   └── weather/                    # Station weather overview panels
│
├── hooks/                          # Custom React hooks
│   ├── useLiveJourney              # Live journey logic
│   └── useTrainSearch              # Train search logic
│
├── lib/                            # API clients, data & caching
│   ├── cache.ts                    # In-memory TTL caching layer
│   ├── opentopography.ts           # Global DEM altitude queries
│   ├── openweather.ts              # OpenWeather API integration
│   ├── overpass.ts                 # OpenStreetMap Overpass client
│   ├── railradar.ts                # RailRadar live GPS tracking
│   └── trains-db.ts                # Bundled offline train database
│
├── store/                          # Zustand client-side state
│   ├── Favorites                   # Favorite-train state
│   ├── Search                      # Search state
│   └── Journey                     # Journey state
│
├── styles/                         # Tailwind & global stylesheets
├── types/                          # TypeScript domain definitions
└── utils/                          # Formatting helpers & class combiner (cn)
```

---

## 🧭 Understanding the Project Structure

| Directory | Responsibility |
|---|---|
| `app/` | Application pages and API endpoints |
| `components/` | Reusable UI components |
| `features/` | Feature-specific functionality |
| `hooks/` | Reusable React logic |
| `lib/` | API clients, data access and caching |
| `store/` | Client-side application state |
| `styles/` | Global styling |
| `types/` | TypeScript definitions |
| `utils/` | Shared helper functions |
| `config/` | Configuration