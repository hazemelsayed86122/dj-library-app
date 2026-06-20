# DJ Music Library Analyzer & Organizer: Project Bible

This document serves as the living source of truth for the DJ app project. It must be read at the start of every new session to regain full context, and updated at the end of every session to log progress and decisions.

---

## GitHub Repository

**URL:** https://github.com/hazemelsayed86122/dj-library-app

All project files are version-controlled here. Every session should start by cloning/pulling the latest code and end by pushing any changes back.

**Session Start Command:**
```bash
git clone https://github.com/hazemelsayed86122/dj-library-app /home/ubuntu/djapp && cd /home/ubuntu/djapp && cat PROJECT.md
```

**Session End Command:**
```bash
cd /home/ubuntu/djapp && git add . && git commit -m "Session [DATE]: [brief description]" && git push origin main
```

---

## 1. Product Vision

### Core Concept
A fully web-based, all-in-one DJ music library analyzer, organizer, and playlist builder. It replaces the fragmented workflow of using separate tools for analysis (e.g., Mixed In Key), library management (e.g., Lexicon), and set planning.

### Competitive Positioning
- **Vs. Mixed In Key:** Web-based (not desktop-locked), includes AI genre/mood detection, and offers an intelligent event-aware playlist builder.
- **Vs. Lexicon:** Includes built-in audio analysis and smart playlist generation, rather than relying on DJ software for analysis.
- **Vs. DJ.Studio:** Focused heavily on library intelligence and personalized set building, not just timeline transition editing.
- **Vs. Cyanite:** Built and priced for individual hobbyist/semi-pro DJs, not B2B platforms.

### The Key Differentiator
The app is built around a **data flywheel**. It is not just an analyzer; it learns from explicit user feedback and implicit DJ behavior (e.g., how tracks are grouped, what transitions work) to continually improve its genre tagging, mood scoring, and playlist generation logic.

---

## 2. Technical Architecture

### Stack Decisions
- **Frontend:** React + TailwindCSS (for a clean, responsive, device-agnostic dashboard)
- **Backend:** Python (FastAPI/Flask) — chosen specifically for compatibility with Python audio libraries.
- **Audio Analysis:** `librosa` and `essentia` (for BPM, key, energy, and feature extraction).
- **Database:** Local database initially (SQLite) moving to cloud-based (PostgreSQL) in Phase 4.
- **Environment:** Entirely web-based. No desktop installation required.

### Folder Structure
```text
/djapp
  PROJECT.md          ← The living project bible (read this first every session)
  /frontend           ← The web app UI code (React)
  /backend            ← The API and audio analysis engine (Python)
  /models             ← AI/ML models for genre, mood, energy classification
  /data               ← Sample tracks and test datasets
  /docs               ← Feature specs, wireframes, notes
  CHANGELOG.md        ← Log of what changed in each session
```

---

## 3. The Build Roadmap

The project is structured in additive phases. Each phase builds upon the existing codebase.

### Phase 1: The Foundation (MVP)
- **Goal:** A working app that analyzes tracks and displays a library dashboard.
- **Features:** Drag-and-drop upload (MP3, WAV, FLAC, AIFF), auto-analysis (BPM, key via Camelot Wheel, energy 1–10, basic genre), sortable library table, manual tag editing, and CSV export.

### Phase 2: Smarter Organization
- **Goal:** Make the library powerful to navigate.
- **Features:** Mood tagging, waveform previews, Camelot Wheel visual filtering, smart filters, duplicate detection, playlist folders, and a watch folder for auto-imports.

### Phase 3: The Playlist Intelligence Engine
- **Goal:** The app generates sets based on context.
- **Features:** Event-aware playlist generator (input duration, genre, energy arc), next-track suggestions, set timeline visualization, and auto-suggested cue points.

### Phase 4: User Accounts & Feedback Loops
- **Goal:** Cloud memory and personalization.
- **Features:** User accounts, cloud storage for metadata, explicit feedback loops (correcting tags, rating playlists), post-event logging, and mobile UI optimization.

### Phase 5: Community Intelligence & Self-Learning
- **Goal:** The network effect (data flywheel).
- **Features:** Monthly model retraining based on user corrections, collaborative filtering ("DJs who played this also played..."), trending tracks, shared playlist templates, and external API integrations (Beatport, Spotify).

### Phase 6: Monetization & Growth
- **Goal:** Launch as a sustainable product.
- **Features:** Freemium tier implementation, payment gateway integration, API access for advanced users, and migration tools from Rekordbox/Serato.

---

## 4. The Self-Learning Architecture (Data Flywheel)

The app becomes smarter over time through two mechanisms:
1. **Explicit Feedback:** Users manually correcting a genre tag or overriding an energy level. These corrections are logged as training data.
2. **Implicit Feedback:** Analyzing how DJs sequence tracks in playlists, which tracks are grouped together, and which auto-generated sets are kept versus discarded.

*Note: The MVP (Phase 1) will rely on pre-trained models. The learning architecture becomes active in Phase 4 and scales in Phase 5.*

---

## 5. Decisions Log

| Date | Decision | Rationale |
|---|---|---|
| Initial Session | Web-based architecture | Avoids platform lock-in (Windows/Mac) and enables cloud-based community learning. |
| Initial Session | Python backend | Required to run industry-standard audio analysis libraries (`librosa`, `essentia`). |
| Initial Session | Phased additive build | Ensures a usable product at every step and allows for real-world testing between phases. |

---

## 6. Known Issues / Limitations

- **Key Detection Accuracy:** While `librosa`/`essentia` are highly capable, matching Mixed In Key's ~95% accuracy out of the box is difficult. The strategy is to achieve "good enough" accuracy for the MVP and improve it over time through user feedback and model refinement.
- **Cold Start Problem:** The self-learning features (Phase 5) require a critical mass of users to become effective.

---

## 7. Session Workflow

### How to Start Every Session
1. Open a new Manus conversation in **this same Manus project**.
2. Say: *"Continue building the DJ app. Clone the repo and read the project bible."*
3. Manus runs the Session Start Command above, reads this file, and picks up exactly where things left off.

### How to End Every Session
1. Manus updates `CHANGELOG.md` with what was built.
2. Manus updates the Phase Status and Next Session Brief below.
3. Manus runs the Session End Command above to push all changes to GitHub.

---

## 8. Phase Status

| Phase | Status | Notes |
|---|---|---|
| Phase 1: MVP | Not started | Ready to begin |
| Phase 2: Smarter Organization | Not started | Awaiting Phase 1 |
| Phase 3: Playlist Engine | Not started | Awaiting Phase 2 |
| Phase 4: Accounts & Feedback | Not started | Awaiting Phase 3 |
| Phase 5: Community Intelligence | Not started | Awaiting Phase 4 |
| Phase 6: Monetization | Not started | Awaiting Phase 5 |

---

## 9. Next Session Brief

**Status:** GitHub repository set up. Project bible complete. Ready to build.
**Next Action:** Start Phase 1 (MVP).
1. Initialize the Python (FastAPI) backend with a `/upload` endpoint.
2. Install `librosa` and extract BPM + key from an uploaded audio file.
3. Initialize the React + TailwindCSS frontend with a drag-and-drop upload component.
4. Display extracted metadata in a sortable library table.
5. Test end-to-end with a sample MP3 file.
