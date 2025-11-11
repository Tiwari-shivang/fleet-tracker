# 🚀 Real-Time Fleet Tracking Dashboard (React + Vite + Redux Toolkit)

## 🔧 Tech Stack
- **React 18 + TypeScript + Vite** – Fast development and build process.
- **Redux Toolkit** – Centralized, scalable state management.
- **TailwindCSS** – Utility-first styling with theme consistency.
- **React Router DOM** – Client-side navigation.
- **Leaflet / MapLibre GL** – Interactive maps.
- **Framer Motion** – Modern animations.
- **Lucide React** – Clean icon system.
- **Vitest + RTL** – Testing framework.
- **GitHub Actions + Pages** – Automated CI/CD deployment.

---

## 🧩 1. Project Setup

```bash
npm create vite@latest fleet-dashboard -- --template react-ts
cd fleet-dashboard

npm i react-router-dom @reduxjs/toolkit react-redux leaflet
npm i tailwindcss postcss autoprefixer clsx framer-motion
npm i lucide-react
npm i -D eslint prettier vite-plugin-svgr @testing-library/react vitest
```

---

## 🎨 2. Tailwind + Theme Configuration

### Tailwind Setup
```bash
npx tailwindcss init -p
```

### tailwind.config.js
```ts
export default {
  darkMode: ['class'],
  content: ['./index.html', './src/**/*.{ts,tsx}'],
  theme: {
    extend: {
      colors: {
        brand: { 50: '#e9f2ff', 100: '#d0e3ff', 500: '#1f6feb', 700: '#144fa1', 900: '#0b2d61' },
        success: '#17B26A',
        warning: '#F79009',
        danger: '#F04438',
      },
      fontFamily: { sans: ['Inter', 'system-ui', 'sans-serif'] },
    },
  },
  plugins: [],
};
```

### Global Styles
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

html, body, #root {
  height: 100%;
  background-color: theme('colors.gray.50');
}
:root { color-scheme: light dark; }
```

---

## 🧱 3. Folder Structure

```
src/
  app/
    store.ts
    theme.ts
  features/
    map/
    trips/
    dashboard/
  components/
    ui/
    layout/
  hooks/
  utils/
  data/mock/
  styles/
```

---

## 🧠 4. Redux Toolkit Setup

### store.ts
```ts
import { configureStore } from '@reduxjs/toolkit';
import tripsReducer from '@/features/trips/tripsSlice';
import uiReducer from '@/features/dashboard/uiSlice';
import simulationReducer from '@/features/dashboard/simulationSlice';

export const store = configureStore({
  reducer: { trips: tripsReducer, ui: uiReducer, simulation: simulationReducer },
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```

### Example Slice
```ts
import { createSlice, PayloadAction } from '@reduxjs/toolkit';
import type { Trip } from '@/types/trip';
import { applyEvent } from '@/utils/eventReducer';

interface TripsState { data: Record<string, Trip>; }
const initialState: TripsState = { data: {} };

const tripsSlice = createSlice({
  name: 'trips',
  initialState,
  reducers: {
    setTrips: (state, action: PayloadAction<Trip[]>) => {
      state.data = Object.fromEntries(action.payload.map(t => [t.id, t]));
    },
    applyTripEvent: (state, action: PayloadAction<{ tripId: string; event: any }>) => {
      const trip = state.data[action.payload.tripId];
      if (trip) state.data[trip.id] = applyEvent(trip, action.payload.event);
    },
  },
});
export const { setTrips, applyTripEvent } = tripsSlice.actions;
export default tripsSlice.reducer;
```

---

## 🌈 5. Theming System

### theme.ts
```ts
export const theme = {
  colors: {
    brand: '#1f6feb',
    surface: '#ffffff',
    bg: '#f9fafb',
    danger: '#F04438',
    success: '#17B26A',
    warning: '#F79009',
  },
  spacing: { sm: '8px', md: '16px', lg: '24px' },
  borderRadius: '12px',
};
```

### Example Usage
```tsx
import { theme } from '@/app/theme';

export function Card({ children }: { children: React.ReactNode }) {
  return (
    <div
      style={{
        background: theme.colors.surface,
        borderRadius: theme.borderRadius,
        boxShadow: '0 4px 12px rgba(0,0,0,0.05)',
      }}
      className="p-4"
    >
      {children}
    </div>
  );
}
```

---

## 🕹️ 6. Simulation Logic

```ts
import { createSlice } from '@reduxjs/toolkit';

interface SimState {
  speed: 1 | 5 | 10;
  isPlaying: boolean;
  currentTime: number;
}
const initialState: SimState = { speed: 1, isPlaying: false, currentTime: 0 };

const simSlice = createSlice({
  name: 'simulation',
  initialState,
  reducers: {
    play: (s) => { s.isPlaying = true; },
    pause: (s) => { s.isPlaying = false; },
    setSpeed: (s, { payload }) => { s.speed = payload; },
    tick: (s) => { s.currentTime += 1000 * s.speed; },
  },
});

export const { play, pause, setSpeed, tick } = simSlice.actions;
export default simSlice.reducer;
```

---

## 🗺️ 7. UI/UX 2025 Standards

- Crisp glassmorphism cards and soft shadows.
- Smooth animations (Framer Motion).
- Responsive layout with grid and flex utilities.
- Command palette (⌘K / Ctrl+K) for quick search.
- Accessible keyboard interactions and focus rings.

**Layout Structure:**
- **Header:** Search, Theme Toggle, Simulation Info.
- **Sidebar:** Filters and Alerts.
- **Main:** Map & Playback Controls.
- **Right Panel:** Trip Timeline & Metrics.

---

## ⚡ 8. Best Practices

| Category | Practice |
|-----------|-----------|
| State | Centralize logic in Redux slices |
| Styling | TailwindCSS + theme tokens |
| Performance | Lazy-load heavy views |
| Components | Reusable & composable design |
| Accessibility | Keyboard + color contrast AA |
| Responsiveness | 320px → 1440px tested |
| Testing | Vitest + Playwright for UI flow |

---

## 🚀 9. Deployment via GitHub Pages

### vite.config.ts
```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
export default defineConfig({
  base: '/fleet-dashboard/',
  plugins: [react()],
});
```

### .github/workflows/deploy.yml
```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [ main ]
permissions:
  contents: write
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---

## 🎯 10. Implementation Timeline

| Sprint | Focus |
|---------|--------|
| 1 | Setup: Vite, Tailwind, Redux, Theme |
| 2 | Layout Shell: Header, Sidebar, Map placeholder |
| 3 | Trip List + Mock Data |
| 4 | Exceptions + Playback UI |
| 5 | Responsive Design + Testing |
| 6 | GitHub CI/CD Deployment |

---

## 💡 Final Notes

- **Redux Toolkit** replaces Zustand for strong state logic.
- **Consistent theming** across components ensures professional UI.
- **Fluid, responsive, zero-shift UX** for all screen sizes.
- **Future-ready architecture** for API integration.
- **GitHub Pages deployment** for simplicity and automation.
