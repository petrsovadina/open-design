---
name: dokturek-design-system-clinical-workspace
description: Apply the DOKTUREK design system when building any interface, deck, document or marketing surface for Dokturek.ai, Benjamin, SVL.ai, or the DOKTUREK ambulatory EHR. Covers the medico-teal palette, the Geist and Roboto Mono type system, glass-over-scene surfaces, the three-column clinical workspace, and the clinical safety rules that separate a machine proposal from a confirmed act.
user-invocable: true
---

# DOKTUREK — Design System & Clinical Workspace

## What is inside

| Path | Use it for |
| --- | --- |
| `DESIGN.md` | the canonical spec. Read before laying anything out. |
| `design-spec.md` | the same spec, kept intact when registration rewrites `DESIGN.md` |
| `colors_and_type.css` | paste-ready token layer: primitives, semantic roles, glass utilities, type, spacing, radius, motion, layout metrics, z-index bands |
| `fonts/` | self-hosted Geist and Roboto Mono woff2 plus `fonts.css`. Copy the folder; do not link Google Fonts. |
| `brand.json` | the same system as structured data, including measured contrast ratios and layout metrics |
| `preview/` | eight review cards showing colour, type, spacing, radius, elevation, controls, clinical patterns and brand assets |
| `ui_kits/app/` | a runnable three-column clinical workspace, React via Babel standalone, no build step |
| `source_examples/` | 19 preserved originals from the platform repo, including `themes.css`, `index.css`, `Button.tsx`, `Alert.tsx`, `Dialog.tsx`, `Table.tsx`, `AppBar.tsx` |
| `assets/`, `build/` | the brand mark, two product screens, the design files, the decision log |
| `context/` | the pasted spec and the GitHub evidence note behind every measured value |

## Source context

Dokturek.ai builds AI products for Czech primary care. DOKTUREK is the ambulatory EHR
itself; Benjamin is the in-visit AI assistant; SVL.ai answers over Czech clinical
guidelines with citations. Everything runs on self-hosted open-source Medplum, so
patient data stays inside the clinic.

The token layer was measured from `app/src/ui/themes.css` and `app/src/ui/index.css` in
a `git clone` of `Dokturek-ai/dokturek-platform` taken on 2026-09-17, then reconciled
against the 1871-line pasted specification and two product screens. Where the spec and
the code disagree, the code wins; the differences are listed in `DESIGN.md` under
"Known drift".

## When to use this skill

Use it for any Dokturek.ai or DOKTUREK surface: clinical screens, dialogs, the
patient card, kartotéka, onboarding, auth, internal tools, decks, one-pagers, emails
and landing pages. Use it when someone asks for "the Dokturek look", the medico teal
system, or the clinical workspace.

Do not use it for a generic healthcare mock with no connection to this product, and do
not port the purple mark into UI colour. The mark keeps its purple; the interface does
not.

## How to use

1. Copy `colors_and_type.css` and `fonts/` into the deliverable. Import the CSS first.
   In a single-file HTML artifact, inline the contents of `colors_and_type.css` into the
   first `<style>` block and inline the font faces you need.
2. Bind everything to the semantic layer. `var(--primary)` rather than `#1e7f74`,
   `var(--radius-box)` rather than `12px`, `var(--elevation-2)` rather than a hand-written
   shadow. A raw hex inside a component is a review failure.
3. Pick the surface before the styling. Chrome and side panels are glass over
   `--scene`. Anything carrying clinical text is `.surface-work`: opaque white,
   elevation 2.
4. Spend teal once. Primary action, focus ring, active selection. Not on a background.
5. Size from the scale. 14px UI, 16px clinical text, 12px metadata, nothing between 12
   and 16, nothing below 12. Codes and dosages go in Roboto Mono.
6. Draw every state. Default, hover, active, focus-visible, disabled, plus loading and
   invalid where relevant. Hover moves the background, never the text colour.
7. Write Czech microcopy in sentence case. A button starts with a verb. No em dash: use
   a comma inside a sentence and a middle dot between fragments. No Czech typographic
   quotes.
8. Check the clinical rules before shipping a clinical surface. A proposal is labelled
   as a proposal, an allergy carries substance and reaction, a conflict names its reason
   and a safe alternative, an override demands a written reason, and a signed record is
   never silently overwritten.

## Design system highlights

**Colour.** Medico teal `#1e7f74` on white measures 4.84:1, so it carries body text.
Its 700 step `#145a52` is the link and pressed colour at 8.03:1. Status colours are
success `#116330`, warning `#a96b28`, info `#1f6fb2`, destructive `#c81e1e`, each with
a soft surface and a border. Small white text on warning is prohibited: 4.36:1.

**Surfaces.** A grey scene `#e9edf0` with soft radial light, glass chrome at 82-92%
white with 12-48px backdrop blur and a hairline rim, and opaque white for work. Shadows
are tinted toward `#0a141f`, never black, at 6-16% alpha, in four levels where level 4
is modals only.

**Type.** Geist for everything, Roboto Mono for codes and tabular values. Geist Mono
was rejected for its dotted zero. Line heights 1.2 / 1.5 / 1.65.

**Shape.** Radius 4 / 6 / 8 / 12, with 999px reserved for avatars, switches and real
pills. 1px borders, 2px for an active edge or the focus ring. A 4px spacing grid with a
single 2px exception.

**Layout.** 1920px design viewport. A 44px glass app bar, 28px patient tabs, a patient
header with 32px side padding and a 2px teal accent line, then 272px / flexible / 420px
with a 12px gap. The editor never drops below 720px. Modals cap at 800px tall.

**Motion.** 150ms for hover and focus, 250ms for dropdowns, 400ms for modals, standard
easing `cubic-bezier(0.2, 0, 0, 1)`. Animation never resizes a row or shifts clinical
content, and everything honours `prefers-reduced-motion`.

**The rule that outranks the rest.** Clinical safety first, then auditability, then
accessibility, then speed of work, then legibility, then consistency, then brand, and
decoration last.
