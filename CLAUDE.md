# Radical Honesty Year 2026 - PWA

## Project Overview

A capacity-aware personal development Progressive Web App designed for a year-long practice of radical self-honesty. Built for Adrian, who operates at ~70% functional capacity with predictable patterns (4-5 productive days, 1-2 survival days per week).

**Live URL:** https://aidedmarketing.github.io/RadicallyHonestYear/
**Repo:** https://github.com/aidedmarketing/RadicallyHonestYear

## Core Philosophy

This is NOT a habit tracker or productivity app. It's a reflective life operating system built on four non-negotiables:

1. **Honesty Before Action** - Tell the truth about where you actually are before optimizing
2. **Systems Over Willpower** - Build structures that work on worst days
3. **Capacity-Aware Design** - Bad days are included in the plan, not exceptions
4. **Identity Through Repetition** - Small, honest repetitions compound

### Design Rules (Never Violate)
- No daily streaks
- No punishment for skipping
- No "catching up"
- Everything has a low-energy version
- Rest is infrastructure, not reward
- Reflection over metrics
- Neutral language, not motivational

## Architecture

### Tech Stack
- Pure HTML/CSS/JavaScript (no framework)
- Single `index.html` file (self-contained)
- Service Worker for offline capability
- localStorage for data persistence
- PWA manifest for home screen installation
- Google Fonts: Crimson Pro (serif headings), DM Sans (body)

### Color Palette
```css
--color-bg: #FAF9F7;           /* Warm off-white */
--color-bg-warm: #F5F1EB;      /* Slightly warmer */
--color-text: #2C3E50;         /* Slate blue-gray */
--color-text-muted: #6B7280;   /* Muted gray */
--color-accent: #D4A373;       /* Warm amber */
--color-accent-light: #E9D5C3; /* Light amber */
--color-success: #7C9885;      /* Sage green */
--color-danger: #C97064;       /* Muted coral */

/* Energy level colors */
--color-survival: #C97064;     /* Red-coral */
--color-functional: #D4A373;   /* Amber */
--color-capable: #7C9885;      /* Sage */
--color-expansive: #5B8A72;    /* Deep sage */
```

### Data Structure
```javascript
const appData = {
  checkins: [
    {
      id: timestamp,
      week: number,
      date: ISO string,
      quarter: "Q1" | "Q2" | "Q3" | "Q4",
      lowEnergyMode: boolean,
      energy: "survival" | "functional" | "capable" | "expansive",
      truthSnapshot: string,
      commitments: [{ text: string, status: "kept" | "renegotiated" | "dropped" | null }],
      renegotiationReflection: string,
      honestWin: string,
      truthForward: string,
      journalRef: string,
      updatedAt?: ISO string
    }
  ],
  cycles: {
    [cycleId]: {
      status: "Not Started" | "In Progress" | "Resting" | "Revisiting" | "Completed",
      responses: { [promptIndex]: string },
      lastUpdated: ISO string
    }
  },
  settings: {
    lowEnergyDefault: boolean
  }
};
```

### localStorage Key
```javascript
const STORAGE_KEY = 'radical-honesty-2026';
```

## Features

### 1. Weekly Check-In (Core Feature)
Five questions, same structure every week:
1. **Truth Snapshot** - What's actually true this week?
2. **Energy Reality** - Survival / Functional / Capable / Expansive
3. **Commitments Audit** - What you committed to and what happened (kept/renegotiated/dropped)
4. **One Honest Win** - Can be survival. Must be real.
5. **One True Thing** - A truth to carry into next week

**Low-Energy Mode:** Only Energy + Honest Win (toggle in form)

### 2. Depth Cycles (7 Optional Inner Work Themes)
Each cycle has:
- Framing paragraph
- 4 prompts
- Safety rule ("observation only")
- Suggested pacing (2-4 weeks)

The 7 cycles:
1. The Things You're Afraid to Want
2. Power Dynamics in Your Everyday Life
3. Your Personal Mythology
4. The Identity You're Slowly Growing Out Of
5. Emotional Echoes
6. Your Relationship With Rest
7. What You Consider "Home" Right Now

### 3. Quarterly Rhythm
- Q1 (Jan-Mar): Foundation - Establish system, observe patterns
- Q2 (Apr-Jun): Stabilization - Integrate work, begin depth work
- Q3 (Jul-Sep): Expansion - Add complexity only if capacity allows
- Q4 (Oct-Dec): Integration - Synthesize, prepare Year-End Artifact

### 4. Reference Pages (Modals)
- The Manifesto - Core philosophy
- Protocols - Re-entry, resets, low-energy versions
- Quarterly Rhythm - Q1-Q4 themes
- Year-End Artifact - December 31, 2026 writing prompts

### 5. Data Management
- Export Data - Downloads JSON backup
- Edit Check-In - Modify existing entries
- Delete Check-In - Remove with confirmation, renumbers weeks

## File Structure
```
/
├── index.html      # Complete app (HTML + CSS + JS)
├── manifest.json   # PWA manifest
├── sw.js          # Service worker for offline
├── icon-192.png   # App icon
├── icon-512.png   # App icon large
├── icon.svg       # Source icon
├── CLAUDE.md      # This file
└── README.md      # User-facing readme (optional)
```

## UI Components

### Screens (defined by .screen class)
- `screen-home` - Dashboard with greeting, core question, status card, recent check-ins
- `screen-checkin` - Check-in form (new or edit mode)
- `screen-cycles` - List of 7 depth cycles
- `screen-cycle-detail` - Individual cycle with prompts
- `screen-history` - All check-ins with quarter filters
- `screen-more` - Reference pages, export

### Navigation
Bottom nav with 4 items: Home, Check-In, Cycles, More

### Modals
Slide-up modals for: manifesto, protocols, quarterly, yearend, checkin-detail, confirm-delete

## Key Functions

```javascript
// Data
loadData()              // Load from localStorage
saveData()              // Save to localStorage
exportData()            // Download JSON

// Navigation
showScreen(screenId)    // Switch screens
openModal(type, data)   // Open modal
closeModal()            // Close modal

// Check-ins
startNewCheckin()       // Begin new entry
editCheckin(id)         // Edit existing
deleteCheckin(id)       // Delete with confirm
handleSubmit(e)         // Save/update check-in
renderRecentCheckins()  // Update dashboard list
renderHistory(filter)   // Update history list

// Form
toggleLowEnergy()       // Toggle low-energy mode
selectEnergy(level, el) // Select energy level
addCommitment()         // Add commitment item
setCommitmentStatus()   // Set kept/renegotiated/dropped
removeCommitment()      // Remove commitment item

// Cycles
renderCycles()          // Render cycle cards
openCycle(id)           // Open cycle detail
saveCycleProgress()     // Save cycle responses

// UI
updateGreeting()        // Morning/afternoon/evening
updateDate()            // Current date display
updateProgress()        // Year progress bar
showToast(message)      // Toast notification
```

## Important Context

### User Context (Adrian)
- Recently lost job (Dec 18), actively job searching for marketing roles
- Has migraines, manages fluctuating energy/capacity
- Values: autonomy, family, financial security, creativity, consistency
- Has a son (Camilo) and supportive partner
- Learning-oriented, research as hobby
- Prefers phone-first, mobile access
- Created this on Dec 26, 2025 (a ladybug landed on his glasses during a walk - taken as positive sign)

### The Year-End Artifact
The entire system points toward one document written December 31, 2026: "If I Get Radically Honest"
- What systems held
- What changed about self-perception
- What can now be said that couldn't before
- What is now known to be wanted
- What's being left behind
- What's being carried forward

### Origin
Built December 26, 2025 in a Claude.ai conversation. The app replaces a Notion workspace that wasn't accessible. The Word document `The_Radical_Honesty_Year_2026.docx` contains the full 24-page system reference.

## Potential Future Enhancements
(Discussed but not yet implemented)
- Cloud sync (Firebase/Supabase) for multi-device
- Data import (restore from backup)
- Quarterly reset prompts built into app
- Year-End Artifact writing space
- Reminder notifications
- Statistics/patterns view
- Dark mode

## Testing Notes
- Test on Safari iOS for home screen install
- localStorage persists per domain/browser
- Service worker caches for offline use
- Data survives app close but not browser data clear
- Export backups regularly recommended
