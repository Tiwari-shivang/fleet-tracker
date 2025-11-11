# 🎨 Fleet Tracking Dashboard – 2025 UI/UX Style Guide

**Version:** 1.0  
**Prepared for:** Real-Time Fleet Tracking Dashboard  
**Author:** Senior Frontend Architect (20+ years of design-led development)

---

## 🧭 1. Design Philosophy

**Objective:**  
Deliver a data-dense yet minimal interface that feels alive, responsive, and human.

**Guiding Principles:**
- Clarity Over Complexity
- Hierarchy with Purpose
- Design for Motion
- Data Legibility
- Consistency and Simplicity

---

## 🌈 2. Design Tokens & Theme System

### 2.1 Color Palette

| Role | Light Mode | Dark Mode | Notes |
|------|-------------|------------|-------|
| Primary (Brand) | `#1F6FEB` | `#539BF5` | Buttons, highlights |
| Background | `#F9FAFB` | `#0C111D` | App background |
| Surface (Card) | `#FFFFFF` | `#161B22` | Panels, widgets |
| Text Primary | `#0F172A` | `#F8FAFC` | Headlines |
| Text Secondary | `#64748B` | `#A0AEC0` | Subtext |
| Success | `#17B26A` | `#3DD68C` | Positive states |
| Warning | `#F79009` | `#F9B44E` | Caution |
| Error | `#F04438` | `#F97066` | Critical |
| Neutral | `#E2E8F0` | `#334155` | Dividers |

---

## 🔤 3. Typography System

| Type | Font | Weight | Size | Line Height | Usage |
|------|------|---------|------|-------------|--------|
| Display | Inter | 700 | 28–32px | 120% | Page titles |
| Section | Inter | 600 | 20–24px | 120% | KPI headers |
| Body | Inter | 400 | 14–16px | 150% | General text |
| Label | Inter | 500 | 12–13px | 140% | Tags, captions |
| Monospace | JetBrains Mono | 400 | 13px | 150% | Data metrics |

---

## 🧱 4. Layout System

- **Base Grid:** 8px spacing system  
- **Container Max Width:** 1280px  
- **Breakpoints:**
  - sm: 640px (stacked)
  - md: 768px (dual-column)
  - lg: 1024px (dashboard)
  - xl: 1280px (wide)

### Structure
| Region | Purpose |
|---------|----------|
| Header | Global controls, search, theme toggle |
| Sidebar | Filters, fleet summary |
| Main | Map, trip overview |
| Playback Bar | Fixed bottom controls |
| Drawer | Trip details |

**Trend:** Floating glass panels, soft shadows, 12–16px radius corners.

---

## 🧩 5. Components Library

### Buttons
| Type | Style | Use |
|------|--------|-----|
| Primary | Brand fill + white text | Main CTA |
| Secondary | Border + hover tint | Neutral action |
| Ghost | Transparent + hover bg | Icon actions |

### Cards
Rounded 16px, shadow `0 8px 24px rgba(0,0,0,0.06)`, padding 16px.

### Alerts
Use color-coded tints (success/warning/error) with left accent border.

### Map Elements
- **Markers:** Status-colored dots  
- **Routes:** Solid or dashed lines  
- **Tooltips:** Minimal with subtle shadow

### Playback Controls
Floating pill container with play/pause + speed toggle.

### Badges
| State | Color | Example |
|--------|--------|----------|
| In Progress | `bg-brand/10 text-brand` | ● In Progress |
| Completed | `bg-success/10 text-success` | ✓ Completed |
| Cancelled | `bg-danger/10 text-danger` | ✕ Cancelled |
| Refueling | `bg-warning/10 text-warning` | ⛽ Refueling |

---

## ✨ 6. Motion & Interactions

- **Library:** Framer Motion  
- **Duration:** 200–250ms  
- **Easing:** `cubic-bezier(0.22,1,0.36,1)`  
- **Hover:** scale(1.02), **Fade In:** opacity 0→1, y +8→0  
- **Prefers-reduced-motion:** respected  

---

## 💎 7. Iconography

- Use **Lucide React** icons  
- Stroke width: 1.5px  
- Sizes: 16–24px  
- Semantic usage only (Play, Warning, Battery, etc.)

---

## 📐 8. Spacing & Alignment

| Element | Margin | Padding |
|----------|---------|----------|
| Card | 16px | 16px |
| Grid gap | 16px | — |
| Section | 24px | — |
| Panel | — | 24px |
| Mobile | 12px | — |

Use Tailwind’s standard spacing scale: 2,4,8,16,24,32.

---

## 🧮 9. Data Visualization

- Rounded bars, subtle gridlines, animated load-in  
- Brand color for active metrics  
- Compact donut charts for trip completion  
- Inline sparkline for violations

---

## 🌐 10. Accessibility

- WCAG AA contrast minimum 4.5:1  
- Full keyboard navigation support  
- ARIA labels on all icons  
- Dark/light mode preference  
- Reduced motion for sensitive users

---

## 📱 11. Responsive Behavior

| Breakpoint | Layout |
|-------------|---------|
| <640px | Stack cards, bottom bar fixed |
| 640–1024px | Two columns |
| >1024px | Full dashboard grid |

---

## 🧑‍💻 12. Developer Guidelines

- Base font size 16px, use rem units  
- Use theme tokens for all colors  
- Flex + min/max instead of fixed height  
- z-index hierarchy: Header(50) > Drawer(30) > Map(10)

---

## 🧾 13. Thematic Modes

### Light
Bright, crisp, focused on visibility.

### Dark
Cool tones, accent blues, suitable for control rooms.

---

## 🪄 14. Trend Inspirations (2025)

- Apple VisionOS – depth layering  
- Linear – typography rhythm  
- Arc Browser – micro-transitions  
- Tesla Fleet Console – motion data feedback  

---

## ✅ 15. Design Checklist

- [x] 8px grid  
- [x] Unified tokens  
- [x] Dark/light tested  
- [x] Motion-enabled transitions  
- [x] Accessibility compliant  
- [x] Responsive verified  
- [x] Zero layout shift (CLS=0)

---

**End of Document**
