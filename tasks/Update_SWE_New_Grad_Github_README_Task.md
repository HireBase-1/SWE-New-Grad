# Update SWE New Grad GitHub README — Task Definition (2026-03-09)

This task keeps the `SWE-New-Grad` repo's `README.md` fresh as a **human‑curated weekly snapshot** of strong new‑grad / early‑career SWE roles sourced from Hirebase.

## Objectives

1. **Pull fresh data** from the Hirebase CLI for Software Engineer roles that are genuinely new‑grad / early‑career friendly (roughly 0–2 years of experience).
2. **Manually curate** a small set of standout roles (“diamonds in the rough”) instead of dumping search results or auto‑generating content.
3. **Update the README** while preserving:
   - Overall structure and headings
   - Emoji atlas and usage
   - Tone and voice (Jared‑style: warm, practical, non‑corporate)
4. **Archive the previous README** to keep a historical record of past snapshots.
5. **Create a PR** from a dated branch (`update/YYYY-MM-DD`) against `main`.
6. **Notify John in Slack** once the PR is ready for review.

## Data Sourcing (Hirebase CLI)

### Baseline query (entry‑level SWE)

Use Hirebase CLI to pull a slice of SWE‑ish roles that are plausibly new‑grad friendly:

```bash
hirebase jobs search \
  --titles "Software Engineer,Software Engineer I,New Grad,Junior" \
  --job-types "Full-time" \
  --yoe-max 2 \
  --include-yoe \
  --days 14 \
  --location-types "Remote,On-site,Hybrid" \
  --sort relevance \
  --order desc \
  --limit 50 \
  --page 1..3 \
  --json
```

You can run additional, narrower searches when you need more variety, for example:

- Internships:
  ```bash
  hirebase jobs search --titles "Software Engineer Intern,Software Engineering Intern" --days 14 --yoe-max 1 --include-yoe --limit 50 --json
  ```
- Non‑US / global flavor:
  ```bash
  hirebase jobs search --titles "Software Engineer,Junior Software Engineer" --days 14 --yoe-max 2 --include-yoe --limit 50 --json --locations "Europe,Canada,India"
  ```

### Manual filtering guidelines

From the JSON results, **manually pick** roles that:

- Have job categories including `"Software Engineer Jobs"` or clearly SWE‑adjacent engineering roles.
- Are explicitly **entry‑level, junior, new grad, or intern** in title or experience (`experience_level` in `Entry-Level` or `Junior / Associate`, `yoe_range.max <= 2`).
- Offer **reasonable mentorship and learning environment**, inferred from:
  - Mentions of rotation programs, training, or strong onboarding
  - Evidence of clear leveling ("Associate", "Rotation Program", "New College Grad")
  - Modern, coherent stacks rather than random legacy tech piles
- Have clear, honest requirements (avoid thin or misleading descriptions).

Actively **exclude**:

- Pure accounting / audit / business roles (even if they contain some tech keywords).
- Non‑SWE jobs like Executive Assistant, pure finance, or generic analyst roles.
- Mid‑senior or ambiguous postings that quietly want 3+ years of experience.

## README Structure & Formatting Rules

The README has a fixed high‑level structure that should remain consistent across runs:

1. **Title + Hirebase logo**
2. Short description of what the list is and who it’s for
3. Snapshot window note (`last ~14 days`, 0–2 YOE)
4. **Quick Glance**
   - Tech Stack Pulse table
   - Comp Snapshot table
5. **Emoji Atlas**
6. **Top 5 Picks** (hand‑picked)
7. **Weekly Spotlight** (short essay / theme on this week’s pattern)
8. **Honorable Mentions** (curated list, not exhaustive)
9. **Find More Roles on Hirebase**
10. **What Is Hirebase?**

### What can change each run

- The **contents** of:
  - Top 5 Picks
  - Weekly Spotlight copy
  - Honorable Mentions list
- The **underlying numbers** in the Tech Stack Pulse / Comp Snapshot if you re‑compute them from a fresh slice.

### What should stay stable

- Section headings and ordering.
- Emoji atlas table and meanings.
- Overall voice and level of detail.
- Markdown style (no tables for role cards, keep bullets and headings consistent).

## Curating the Roles

### Top 5 Picks

Pick 5 roles that would make a hiring‑savvy mentor say: *“If you land this, you’re in good shape.”* For each card:

- **Title:** `Company – Role Title` + relevant emojis (💼, 🎓, 🌍, 🏙️, 💻, ⚙️, 📊, 🧪)
- **Location:** City/Region/Country and remote/onsite indicator.
- **Stack:** From `technologies` and the description, formatted as a short comma‑separated list.
- **Comp:** Use the `salary_range` if present; otherwise, say “Not listed” or describe the band qualitatively.
- **Why it stands out:** 2–4 sentences tying together:
  - Type of work (product, infra, ML, embedded, etc.)
  - Learning/mentorship signals
  - Why it’s attractive to a strong new grad.
- **Apply link:** Use the Hirebase URL format:
  
  ```text
  https://www.hirebase.org/company/{company_slug}/jobs/{job_slug}
  ```

Aim for a mix:

- 1–2 US roles (ideally including at least one remote‑friendly)
- 1 non‑US role
- A blend of web/product, infra/systems, and data/ML‑adjacent when possible.

### Weekly Spotlight

Write a short (2–4 paragraph) commentary based on this week’s data and picks. Examples of themes:

- Internships that look like real jobs
- Hidden new‑grad roles in enterprise / infra teams
- Global opportunities outside the usual US hubs
- Cloud & DevOps expectations creeping into entry‑level roles

Ground it in what you actually see in the slice (e.g., “a lot of hybrid UK/Canada roles with .NET + Azure”, “several US remote Python roles in fintech and healthcare”). Keep it actionable for a student/job‑seeker.

### Honorable Mentions

Curate **10–25** additional roles worth serious consideration. For each:

- Company + Role
- Emojis
- Location
- Stack (short)
- Comp (if available)
- 1–2 sentence "why it’s interesting"
- Hirebase apply link

Keep this section **curated, not exhaustive**. The goal is to surface:

- Good diversity of locations (US, Canada, Europe, Asia, LATAM).
- Mix of internships and full‑time.
- Mix of product, infra, and data‑adjacent work.

## Archiving & Versioning

Each run should:

1. **Archive the previous README** before editing:
   ```bash
   cp README.md "archived/YYYY-MM-DD-v1.md"
   ```
   - Use the date corresponding to the new snapshot (the day you’re updating).
2. Then modify `README.md` for the new snapshot.

This keeps a historical trail of how the market and curation evolved.

## Branching, Commit, and PR Workflow

1. Ensure you’re on `main` and up to date:
   ```bash
   git checkout main
   git pull origin main
   ```

2. Create a new branch for the run:
   ```bash
   git checkout -b update/YYYY-MM-DD
   ```

3. Make edits:
   - Archive previous README to `archived/YYYY-MM-DD-v1.md`.
   - Update `README.md` content.
   - Update this task file if you’ve discovered better patterns or received feedback.

4. Stage and commit:
   ```bash
   git add README.md archived/YYYY-MM-DD-v1.md tasks/Update_SWE_New_Grad_Github_README_Task.md
   git commit -m "chore: refresh new grad SWE README (YYYY-MM-DD)"
   ```

5. Push and create PR:
   ```bash
   git push -u origin update/YYYY-MM-DD
   gh pr create \
     --title "chore: refresh new grad SWE README (YYYY-MM-DD)" \
     --body "Weekly refresh of curated new grad / early-career SWE roles from Hirebase. Includes updated Top 5, spotlight, and honorable mentions based on the last ~14 days of 0–2 YOE SWE postings."
   ```

## Feedback & Self‑Correction Log

Use this section to capture feedback from John and lessons learned so each run gets better.

### Known expectations / feedback to honor

- **No auto‑dumping search results.** Every role in the README should be there because you deliberately picked it.
- **Stay on theme:** The repo is for **Software Engineer (New Grad / Early Career)**. Avoid drifting into pure accounting, consulting, or non‑engineering roles even if they’re entry‑level.
- **Consistent emojis & formatting:** Reuse the Emoji Atlas; don’t invent new emoji semantics mid‑file.
- **Readable, non‑corporate tone:** Keep explanations clear, concrete, and slightly conversational. Avoid buzzword salad.
- **Balance internships and full‑time:** Each run should have both, not just one or the other.

### 2026-03-09 adjustments

- Explicitly documented the **CLI query patterns** and manual filters so future updates don’t drift into "dump everything" mode.
- Clarified the **archiving convention** (`archived/YYYY-MM-DD-v1.md`) and ensured we always snapshot the prior README before editing.
- Added a concrete **branch, commit, and PR flow** so every run uses `update/YYYY-MM-DD` and a consistent commit message.
- Re‑emphasized avoiding clearly non‑SWE roles (accounting, audit, EA) even when they appear in broad Hirebase searches.

Update this log on future runs with any new feedback (e.g., “prefer more US remote roles”, “lean more into ML‑adjacent internships”, “limit Honorable Mentions to 15 for brevity”, etc.).
