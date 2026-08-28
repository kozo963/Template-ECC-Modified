# Mockup/ — UI source of truth (user-maintained)

One folder per milestone, named exactly like the milestone:
`Mockup/NN-M-<Name>/` (e.g. `Mockup/01-M-LandingPage/landingPage.html`).

- Static HTML/CSS files only — they are the reference the coder must match
  (layout, sections, components, spacing, assets).
- Shared assets (logos, icons, fonts, design tokens) go in `Mockup/Data/`
  and are always referenced by exact path, e.g. `Mockup/Data/Logo.svg`.
- Tasks in `plan/NN-M-<Name>.md` must point to the mockup file they implement.
- If a task has no mockup, write "no mockup — follow rules/react-patterns.md
  + shadcn/ui defaults" in the task line so the brain knows.

This folder is read-only for the AI. The AI never edits mockups.
