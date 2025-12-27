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
      cycleReflection: string (optional),
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
  quarterlyResets: {
    [quarter]: {
      continuity: string,
      pattern: string,
      avoided: string,
      workedWell: string,
      capacity: string,
      shift: string,
      savedAt: ISO string
    }
  },
  yearEndArtifact: {
    systems: string,
    identity: string,
    ableToSay: string,
    wants: string,
    leaving: string,
    carrying: string,
    capacity: string,
    surprised: string,
    message: string,
    savedAt: ISO string
  },
  settings: {
    lowEnergyDefault: boolean,
    lastExport: ISO string | null
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
1. **Truth Snapshot** - What's actually true this week that I might otherwise gloss over?
   - *Enhanced with sub-prompts if stuck:* What am I not saying? What's harder than I'm admitting? What surprised me about my energy?
2. **Energy Reality** - Survival / Functional / Capable / Expansive
3. **Commitments Audit** - What you committed to and what happened (kept/renegotiated/dropped)
4. **One Honest Win** - Can be survival. Must be real.
5. **One True Thing** - A truth to carry into next week
6. **Journal Reference** (optional)
7. **Active Cycle Reflection** (optional) - How did current depth cycle show up in your week?

**Low-Energy Mode:** Only Energy + Honest Win (toggle in form)

### 2. Depth Cycles (9 Timeless Inner Work Themes)
Each cycle has:
- Framing paragraph
- 4 prompts
- Safety rule ("observation only")
- Suggested pacing (2-4 weeks)
- Status tracking (Not Started → In Progress → Resting → Revisiting → Completed)

**The 9 cycles (ordered by vulnerability progression):**

**Q1: Foundation**
1. **What You Consider "Home" Right Now** - Grounding, present-focused
2. **Your Relationship With Rest** - Foundational for capacity-aware practice
3. **The Things You're Afraid to Want** - Opens vulnerability early (but not first)

**Q2: Stabilization**
4. **The Relationships That Hold You** - Partner, son, family, friendships
5. **What Lights You Up** - Curiosity + joy combined (lighter cycle, breathing room)
6. **Power Dynamics in Your Everyday Life** - Examining where you shrink/expand

**Q3: Expansion**
7. **Your Personal Mythology** - Stories you tell yourself
8. **The Identity You're Slowly Growing Out Of** - Grief and synthesis

**Q4: Integration**
9. **Emotional Echoes** - Deepest work, saved for when you're strongest

### 3. Quarterly Reset Prompts
Interactive reflections at end of each quarter (Q1-Q4):
1. **Continuity** - "Last quarter you said this needed to shift - did it?" (auto-populated from previous quarter)
2. **Unexpected Pattern** - What emerged that you didn't expect?
3. **Consistent Avoidance** - What did you keep not doing?
4. **Worked Unexpectedly Well** - Positive surprises
5. **Capacity Baseline Check** - Is your 4-5 functional, 1-2 survival still accurate?
6. **What Needs to Shift** - Not goals. Just: what needs adjusting next quarter?

Creates continuity thread across quarters instead of isolated reflections.

### 4. Year-End Artifact (December 31, 2026)
The entire system points toward one document: "If I Get Radically Honest"

**9 Questions:**
1. What systems held?
2. What changed about how you see yourself?
3. What you're now able to say?
4. What you now know you want?
5. What you're leaving behind?
6. What you're carrying forward?
7. **What you learned about your capacity and baseline**
8. **What surprised you about your year** (positive or challenging)
9. **If you could tell January 1, 2026 Adrian one thing, what would it be?**

### 5. Pattern Insights
Dashboard showing real-time stats as year unfolds:
- Overview: Total check-ins, % year complete, active cycles, low-energy weeks
- Energy Distribution: Visual breakdown of Survival/Functional/Capable/Expansive weeks
- Commitment Stats: Kept vs. renegotiated vs. dropped percentages
- Personalized Insights: What the data reveals about your capacity

Preview shown on home screen dashboard.

### 6. Safety Net Features
**Export Reminder:**
- Tracks last export timestamp
- Shows warning banner on home if 7+ days since export
- One-click export from banner
- Protects against data loss

**Re-Entry Support:**
- Detects when 8+ days pass without check-in
- Shows neutral message: "It's been X days. Ready to check in, or still in rest mode?"
- Links to Re-Entry Protocol
- Disappears when check-in happens

**Quarter Transition Markers:**
- Automatic detection when crossing Q1→Q2, Q2→Q3, Q3→Q4
- Banner on home screen for first 7 days of new quarter
- Shows quarter name and theme
- Reminds to do quarterly reset

**Dashboard Visibility:**
- Last check-in date: "Last check-in: Week 3 (14 days ago)"
- Pattern preview: Rotating insight from current quarter data
- Export status: Visible warning if backup needed

### 7. Data Management
- **Export JSON** - Full backup for restore
- **Export Markdown** - Human-readable format for reflection
- **Import/Restore** - Upload JSON backup (merge or replace options)
- **Edit Check-In** - Modify existing entries
- **Delete Check-In** - Remove with confirmation, renumbers weeks
- **Search** - Text search across all check-ins (snapshots, wins, commitments, journal refs)

## File Structure
```
/
├── index.html      # Complete app (HTML + CSS + JS)
├── manifest.json   # PWA manifest
├── sw.js          # Service worker for offline
├── icon-192.png   # App icon
├── icon-512.png   # App icon large
├── icon.svg       # Source icon
├── CLAUDE.md      # This file (technical documentation)
└── README.md      # User-facing readme
```

## UI Components

### Screens (defined by .screen class)
- `screen-home` - Dashboard with greeting, core question, status card, recent check-ins, safety net banners
- `screen-checkin` - Check-in form (new or edit mode) with active cycle integration
- `screen-cycles` - List of 9 depth cycles with status indicators
- `screen-cycle-detail` - Individual cycle with prompts and status selector
- `screen-history` - All check-ins with quarter filters and search
- `screen-patterns` - Pattern insights and statistics
- `screen-quarterly-reset` - Interactive quarterly reflection prompts
- `screen-yearend-artifact` - Year-End Artifact writing space
- `screen-more` - Reference pages, export options

### Navigation
Bottom nav with 4 items: Home, Check-In, Cycles, More

### Modals
Slide-up modals for: manifesto, protocols, quarterly, yearend (reference), checkin-detail, confirm-delete

## Key Functions

```javascript
// Data
loadData()              // Load from localStorage
saveData()              // Save to localStorage
exportData()            // Download JSON backup
exportMarkdown()        // Download readable markdown
importData(event)       // Restore from JSON backup

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
renderHistory(filter, searchQuery)   // Update history list with search
searchCheckins(query)   // Filter check-ins by text

// Form
toggleLowEnergy()       // Toggle low-energy mode
selectEnergy(level, el) // Select energy level
addCommitment()         // Add commitment item
setCommitmentStatus()   // Set kept/renegotiated/dropped
removeCommitment()      // Remove commitment item

// Cycles
renderCycles()          // Render cycle cards with status
openCycle(id)           // Open cycle detail
saveCycleProgress()     // Save cycle responses and status
selectCycleStatus(status, el) // Update cycle status

// Quarterly Resets
selectQuarterReset(quarter, el)  // Select quarter, load data, show continuity
saveQuarterlyReset(e)            // Save quarterly reflection

// Year-End Artifact
loadYearEndArtifact()   // Load saved artifact data
saveYearEnd(e)          // Save year-end reflection

// Pattern Insights
renderPatterns()        // Render full statistics page
getPatternInsight()     // Generate rotating insight for dashboard
updatePatternPreview()  // Update dashboard preview

// Safety Net
checkExportReminder()   // Check if export needed (7+ days)
checkReentryAndQuarter() // Check re-entry (8+ days) and quarter transitions
updateLastCheckinDisplay() // Show last check-in date
updateDashboard()       // Combined safety net check

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

### Design Philosophy: Timeless Inner Work
The system is designed for **building foundation for who you're becoming**, not crisis management for what's happening now. All cycles focus on timeless themes (identity, relationships, rest, mythology) rather than current circumstances.

### The Year-End Artifact
The entire system points toward one document written December 31, 2026: "If I Get Radically Honest"

This is not just a reflection—it's the synthesis of 52 weeks of radical honesty about:
- What systems held
- What changed about self-perception
- What can now be said that couldn't before
- What is now known to be wanted
- What's being left behind
- What's being carried forward
- What was learned about capacity
- What surprised you
- What you'd tell your January 1, 2026 self

### Origin
Built December 26, 2025 in a Claude.ai conversation. The app replaces a Notion workspace that wasn't accessible. The Word document `The_Radical_Honesty_Year_2026.docx` contains the full 24-page system reference.

## Implementation Timeline

**December 26, 2025** - Initial build
- Core weekly check-in system
- 7 depth cycles
- Basic data persistence
- PWA infrastructure

**December 27, 2025** - Complete system refinement
- Added 2 cycles (Relationships, What Lights You Up) → 9 total
- Reordered cycles by vulnerability progression
- Interactive quarterly resets with continuity
- Year-End Artifact writing space (9 questions)
- Pattern insights dashboard
- Safety net: export reminder, re-entry support, quarter transitions
- Data import/restore
- Search functionality
- Markdown export
- Enhanced weekly prompts
- Cycle status management (5 states)

## Current Status: Complete & Production-Ready

All core features implemented. System is fully sufficient for 52-week practice.

**What's Built:**
✅ 9 depth cycles with timeless inner work themes
✅ Weekly check-ins with enhanced prompts
✅ Quarterly resets with continuity across quarters
✅ Year-End Artifact with comprehensive questions
✅ Pattern insights showing real data
✅ Safety net (export reminder, re-entry support, quarter transitions)
✅ Data import/export (JSON + Markdown)
✅ Search across all reflections
✅ Cycle status management
✅ Full PWA offline capability
✅ Mobile-first responsive design

**Deliberately Not Included:**
❌ Daily streaks or habits
❌ Gamification or points
❌ Push notifications
❌ Cloud sync (localStorage + manual export is the model)
❌ Dark mode (light mode is intentional)
❌ Social features or sharing
❌ AI analysis or suggestions

## Testing Notes
- Test on Safari iOS for home screen install
- localStorage persists per domain/browser
- Service worker caches for offline use
- Data survives app close but not browser data clear
- **Export backups regularly** (system reminds at 7+ days)
- Import/restore tested with merge and replace options
- Pattern insights require 3+ check-ins to display

## Future Considerations (Not Planned, But Possible)

These features were discussed but intentionally not implemented to maintain simplicity:

- Cloud sync (Firebase/Supabase) for multi-device
- Push notifications / reminders
- Advanced data visualization
- Commitment pattern tracking over time
- Week-by-week calendar view
- Milestone acknowledgments (Week 26, Week 52)

The current system is complete and sufficient. Additional features would add complexity without serving the core philosophy.

---

*Last updated: December 27, 2025*
*System status: Complete and production-ready*
