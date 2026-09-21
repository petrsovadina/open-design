# DOKTUREK — Design System & Clinical Workspace

A reusable design-system package for DOKTUREK, the ambulatory EHR that Dokturek.ai
builds for Czech primary care. Tokens, self-hosted fonts, preview cards, an applied UI
kit and the preserved source evidence, all measured from the running product rather
than inferred from a screenshot.

`DESIGN.md` is the canonical source of truth. Everything else in this package either
implements it or shows it.

## Product Overview

**Product.** DOKTUREK, an ambulatory EHR and clinical workspace built by Dokturek.ai
for Czech primary care. The application supports a whole visit on one surface: context,
note, decision and billing.

**Primary surfaces.** The patient card (three-column clinical workspace), kartotéka
(the dense patient table), the encounter editor, the document digitisation review, the
eRecept and appointment dialogs, practice onboarding, and sign-in.

**Core capabilities.** The product provides writing and signing of a dekurz with recognised structured values,
medication safety checks against the patient's allergies, billing proposals derived
from the note, a right-hand clinical summary that stays visible while working, OCR
extraction from uploaded documents with a human review step, and a patient-scoped
assistant that answers with citations.


DOKTUREK is a desktop web application for practitioners; the interface language is
Czech. It runs on self-hosted open-source Medplum, a headless FHIR EHR, so patient
data stays inside the clinic. Two adjacent products share the identity: Benjamin, an
AI assistant that handles documentation, routine admin triage and lookup during a
visit, and SVL.ai, a retrieval system over Czech clinical guidelines that answers with
citations to the source document.

The audience is general practitioners and small clinics. They are time-poor, sceptical
of software that adds clicks, and answerable for the outcome. That shapes the whole
system: density comes from structure rather than from shrinking type, teal marks the
one action that matters on a screen, and a machine proposal never looks like a
confirmed clinical act.

The visual direction changed once and the change is load-bearing. Medico teal replaced
purple, `radius-box` dropped from 14-24px to 12px, the working surface became solid
white instead of layered glass cards, and quick actions moved into the patient header.
Anything still showing the purple SaaS direction is void.

## Source

| Evidence | Path | Read method |
| --- | --- | --- |
| Normative spec, pasted | `context/input-DESIGN.md` | supplied, 1871 lines |
| Design decision log | `assets/Poznamky-EHR.md` | supplied, 2-4 September 2026 |
| Platform repository | https://github.com/Dokturek-ai/dokturek-platform | `git clone`, snapshot 2026-09-17 |
| Measured token file | `context/github/.../app/src/ui/themes.css` | read |
| Tailwind v4 wiring | `context/github/.../app/src/ui/index.css` | read |
| Product screen, light | `assets/file-30a72f8e5753df218e9d2545fdc4a4c8.jpeg` | read, 1152 × 1478 |
| Density reference, dark | `assets/EHR-design-image.png` | read, 2166 × 2046 |
| Design files | `assets/HU-Design.pen`, `assets/Patient-Card-HU.pen` | not decoded, see Limitations |

Every colour, radius, shadow, blur and duration in `colors_and_type.css` was copied
from `themes.css` or `index.css`, not eyeballed. Where the pasted spec and the running
code disagree, the code wins and the gap is recorded in `DESIGN.md` under "Known
drift".

## Package contents

| Path | What it is |
| --- | --- |
| `DESIGN.md` | the canonical spec: identity, colour, surfaces, type, layout, components, clinical safety rules, accessibility, known drift |
| `design-spec.md` | the durable copy of that spec, kept because re-registering the system rewrites `DESIGN.md` |
| `brand.json` | machine-readable brand record: palette, scales, semantic tokens, typography, voice, imagery, layout metrics, measured contrast, seed overrides |
| `colors_and_type.css` | the reusable token layer, plus the glass and surface utilities |
| `fonts/` | self-hosted Geist and Roboto Mono woff2 subsets, the supplied Bricolage Grotesque variable font, `fonts.css`, `LICENSES.md` |
| `preview/` | eight focused review cards, see the manifest below |
| `ui_kits/app/` | a runnable applied interface: the three-column clinical workspace |
| `source_examples/` | 19 preserved originals from the platform repo: the token files, the UI primitives, the layouts |
| `assets/` | uploaded brand assets, product screens, design files, the decision log |
| `build/` | runtime rasters preserved byte-for-byte from the repository |
| `context/` | setup context, the pasted spec, the GitHub evidence note and file snapshots |
| `system/` | the generated branding-agent bundle: seed, token JSON per theme, antd theme, light and dark kits, sample artifacts |
| `guide.md` | the short brand guide |
| `SKILL.md` | agent-facing usage instructions |

## Preview Manifest

| Card | What it shows |
| --- | --- |
| `preview/colors-primary.html` | the three raw scales, medico teal step by step, measured contrast on white |
| `preview/colors-semantic.html` | the semantic roles components actually read, the four status surfaces, accent versus a teal wash |
| `preview/typography-specimens.html` | the Geist scale in Czech, the four weights, Roboto Mono in a billing table, the three line heights |
| `preview/spacing-tokens.html` | the 4px scale drawn to size, the three-column layout at its real widths, the fixed metrics |
| `preview/radius-elevation.html` | the radius family, four elevation levels, the three glass materials, and the opaque surface they are not used for |
| `preview/components-buttons.html` | Button, Input, Badge and Alert with every interaction state drawn |
| `preview/components-clinical.html` | safety context, medication conflict, billing proposals, provenance, the encounter lifecycle |
| `preview/brand-assets.html` | the preserved mark at three sizes, the three type faces, both product screens, the design-file inventory |

`preview/preview.css` is the shared card chrome. Every card links
`../colors_and_type.css` first, so nothing in `preview/` redeclares a token.

## Reuse workflow

1. Copy `colors_and_type.css` and `fonts/` into the target project. Import the CSS once,
   before any component styles. The fonts are self-hosted, so type never falls back to
   a substitute face, and latin-ext is included because the interface is Czech.
2. Read `DESIGN.md` before laying anything out. The sections that decide most questions
   are Surface hierarchy, Layout posture rules, and Clinical safety rules.
3. Build against the semantic layer. `var(--primary)`, never `#1e7f74`; `var(--radius-box)`,
   never `12px`. Feature code that writes its own hex, shadow or radius fails review.
4. Lift component shapes from `ui_kits/app/components/` for a prototype, or from
   `source_examples/app/src/ui/` for production. The latter are the real files: CVA
   variants, Radix primitives, Tailwind v4 utilities.
5. For a fresh HTML deliverable, `ui_kits/app/index.html` is the closest thing to a
   starting template; it composes the app bar, patient header and three columns and
   runs with no build step.

## Applying the system to new work

- One accent. Teal marks the primary action, the focus ring and the active selection.
  A screen with teal in five places has no primary action.
- Glass is chrome and context. Solid white is work. If a surface carries a sentence a
  doctor has to read carefully, it is opaque.
- Every state needs a word or a marker as well as a colour, and every proposal needs
  its provenance.
- Dense is not small. 14px UI, 16px clinical text, 32 and 36px rows, a 4px grid. The
  floor is 12px.
- Modals cap at 800px tall. Longer work is a screen.

## Limitations

- `assets/HU-Design.pen` and `assets/Patient-Card-HU.pen` could not be decoded in this
  run. `.pen` files are encrypted and readable only through the Pencil app, which was
  not running, so the MCP bridge refused the connection. Their token content is
  mirrored by the pasted spec and by `themes.css`, both of which were read in full, so
  the loss is component geometry and screen-level detail rather than tokens.
- The in-app `Logo` component was not part of the bounded repository snapshot. The
  preserved rasters in `assets/` and `build/` are the reference instead.
- Button and field heights differ between the spec and the shipped components. Both
  numbers are recorded in `DESIGN.md`; the implementation is treated as current truth.
- `Badge` ships as a full pill while the spec reserves the full pill for avatars,
  switches and real pills. Unresolved, and left visible rather than silently aligned.
- The dark theme in `system/kit.dark.html` is generated from the seed by the
  branding-agent algorithm. DOKTUREK has one normative theme, and it is light; treat
  the dark output as a generated variant, not as a specified surface.
- A mobile clinical workflow does not exist. Below 1024px the specification stops.
- Registering the design system rewrites `DESIGN.md` into a fixed seven-role shape and
  strips `brand.json` back to its own schema, which drops the measured scales, layout
  metrics and provenance. `design-spec.md` and `colors_and_type.css` are the durable
  copies; restore `DESIGN.md` from the former rather than rewriting it.

## Provenance

Formalized by OpenDesign from candidate 9f797a00-2c9e-4435-9c34-84a15311a0b4.
