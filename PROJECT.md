# DJ Music Library Analyzer & Organizer: Project Bible

This document serves as the living source of truth for the DJ app project. It must be read at the start of every new session to regain full context, and updated at the end of every session to log progress and decisions.

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

## 7. Next Session Brief

**Status:** Ready to begin development.
**Next Action:** Start Phase 1 (MVP).
1. Initialize the Python backend and React frontend scaffolding.
2. Implement the basic audio upload endpoint.
3. Integrate `librosa` to extract BPM and key from a sample audio file.
4. Build the basic frontend table to display the extracted metadata.
