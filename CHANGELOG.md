# Changelog
All notable changes to this project will be documented in this file.

This project follows a simple semantic versioning style and keeps the **UserCSS `@version`** in sync with releases so Stylus can auto‑update.

---

[1.1.0]: https://github.com/Exirtis/plantdemand-userstyle/compare/v1.0.9...v1.1.0
[1.0.9]: https://github.com/Exirtis/plantdemand-userstyle/compare/v1.0.8...v1.0.9

## [1.1.0] – Grouping Resilience, UI Cleanup, Always-Important, and UI/Metadata Typography : 2026‑02‑24
### Changed
- **Selectors hardened** against CSS‑module hash churn and grouping flips (via **class‑prefix** anchors):  
  *(Prev in 1.0.9 used hashed classes, as noted by individual entries below)*
  - Group header (Customer or Material) via pill testids + header prefix:  
    `[data-testid="pill-customer"] > [class^="pill__header__"]`,  
    `[data-testid="pill-material"] > [class^="pill__header__"]`  
    *(prev: `.pill__header__38Us8`)*
  - Non-heading *material*/*customer* line (internally labeled as `product`) styling cascades to `order__title` & `order__quantity` to keep typography unified (background stays on the parent):  
    `[class^="order__header__"]` (+ descendant cascade)  
    *(prev: `.order__header__RkIf1`)*
  - Fields scoped to the fields wrapper:  
    `[data-testid="custom-fields"] [class^="order__field__"][data-field="…"]`  
    *(prev: `.order__field__20xzI[data-field="…"]`)*
  - Load Time scoped under order wrappers:  
    `[data-testid$="-order"] [class^="order__loadTime__"]`  
    *(prev: `.order__loadTime__2N6BS`)*
- Adopted **always `!important`** for reliable overrides; removed the `useImportant` toggle.
- Standardized **bold** behavior across sections:
  - Included bolding selectors where not already present
  - Consistently emits either `bold` **or** `normal`, allowing users to force non‑bold where the site defaults to bold
- **Background scopes** reinforced through selector hardening, but unchanged in behavior:
  - Background applies only to the exact header/field container
  - Fonts/size/color may cascade to descendants for coherent typography
- **Renaming:** PO Number variables and properties standardized to `poNumber*` (e.g., `poUseBg` → `poNumberUseBg`).
- Extra scoping implemented via the calendar container’s `[data-calendar-view]` ancestor.

### Added
- **Job Name** and **Job Number** sections with full per‑section controls (font source, size, bg, color, bold).
- Stylus UI refinements:
  - Clear section “headings” via checkbox rows
  - Consistent “Choose / Set / Toggle” language
  - In‑UI documentation link (URL for copy/paste)
- **UI/Metadata Typography** (labels):
  - Improved label readability in Stylus UI by using Unicode decorative forms
    (fullwidth, small caps, serif/italic/mono variants) across section headings
    and “Choose / Set / Toggle” prompts. Functional behavior is unchanged; only
    metadata labels were updated.


## [1.0.9] – Hosting, Auto‑Updates & Repo Setup : 2026‑02‑10
### Added
- Created GitHub repository for distribution and versioning.
- Added `@downloadURL` / `@updateURL` directives for Stylus auto‑updates.
- Added `README.md`, `CHANGELOG.md`, and `LICENSE` (MIT).

### Changed
- Hosted the stylesheet via **GitHub Pages** at  
  `https://exirtis.github.io/plantdemand-userstyle/PlantDemand.user.css`.


## [1.0.8] – Customer Background Toggle Standardization : 2026‑01‑29
### Added
- **Customer:** background color **toggle** (with alpha) to match other sections.

### Changed
- Standardized Customer naming to align with other sections (prep for alternate group‑by modes).


## [1.0.7] – Per‑Section BG Toggles + Customer Text Color : 2026‑01‑27
### Added
- **Product / Order # / PO # / Expire Date / Load Time:** background color **toggles** (with alpha) for each section.
- **Customer:** **text color toggle** (`customerUseColor` + `customerColor`), applied to the header element only to avoid descendant color spillover.


## [1.0.6] – Labeled Selects + User‑Friendly UI : 2025-11-10*
### Added
- Converted all selects to **labeled map/object** format (`"Label*": "preset-value"`).
- Introduced clearer UX labels (e.g., “Use Global”, “Override with preset”).
- Reorganized metadata for readability, including emoji section markers.

### Fixed
- Eliminated `preset-openSans*` value injection issues by moving the `*` to the **label** side (per metadata parser behavior).
- Resolved Stylus `Cannot read properties of undefined (reading 'lineno')` errors caused by invalid value tokens.

### Changed
- Clarified section labels: Customer, Product, Order #, PO #, Expire Date, Load Time.
- Cleaned and standardized the header for readability.


## [1.0.5] – UI & Override Reliability Pass : 2025-10-25
### Added
- Implemented robust **string coercion** for `@var select` results (`'' + var`) to stabilize comparisons.
- Ensured Global → Section override ordering works consistently.

### Fixed
- Corrected a case where global presets overrode section presets due to identifier vs. string mismatches.

### Changed
- Stabilized preset comparison logic.
- Removed placeholder‑based normalization that interfered with overrides.
- Style now supports (in verified predictable order):
  - Global preset
  - Section preset override
  - Section custom override
- Ensured custom font stacks emit valid CSS via `unquote()`.


## [1.0.4] – Decimal Step & Precision Stability : 2025-10-16*
### Fixed
- Standardized `@var number` **step precision** to prevent “value is not a multiple of step” validation errors by aligning step with defaults:
  - `0.8125` → step `0.0001`
  - `0.875` → step `0.001`
  - (and similar across sections)
- Finalized ranges for:
  - Customer header
  - Product header
  - Order #
  - PO #
  - Expire Date
  - Load Time
- Confirmed opacity controls use `[min, max, step]` safely.

### Changed
- Updated all numeric UserCSS variables to the `[default, min, max, step, "unit"]` format.
- Verified no regressions in font override logic.


## [1.0.3] – Full Stylus Implementation + Major Infrastructure : 2025-10-15
### Added
- First fully working **Stylus preprocessor** version (`@preprocessor stylus`).
- Conditional per‑section control logic using Stylus `if/else` for font/color overrides.
- Introduced:
  - `fontPreset`, `fontCustom`
  - Per‑section font source modes
  - Per‑section sizes, weights, color toggles
  - Load Time support

### Fixed
- Resolved Stylus parser/syntax errors (“Expect a word”, “Not a color”, “Unexpected else”).
- Removed inline comments from the metadata header (not allowed).
- Converted `@-moz-document { … }` brace block to **indent‑syntax** for Stylus.
- Avoided placeholder collisions with Stylus parsing.

### Changed
- Implemented reliable `'' + var` **string coercion** for select/text values.
- Applied `unquote(...)` to all font stacks to ensure valid CSS output.
- Added descendant selectors for fonts to override deeply nested site styling.


## [1.0.2] – Begin UserCSS Conversion : 2025-10-15*
### Added
- Restructured style for Stylus preprocessor use.
- Added UserCSS header, variables, and metadata.
- Added:
  - Master **`!important`** switch
  - `@var` definitions
  - `fontPreset`, `fontCustom`
  - Section font modes, presets, sizes, colors, bold toggles
- Introduced Stylus syntax (`@preprocessor stylus`), with compile‑time errors addressed in later releases.

### Changed
- Shifted to variable‑driven architecture in preparation for section overrides.
- Normalized document scoping and selectors.


## [1.0.1] – Early Cleanup & Refinement : 2025-10-14
### Changed
- Minor CSS improvements and structural cleanup ahead of UserCSS conversion.
- Adjusted formatting and selectors; removed unstable/redundant selectors.
- No functional UI controls yet — still a single static style.


## [1.0.0] – Initial Release : 2025-05*
### Added
- First working version of the style (plain CSS, no UserCSS metadata).
- Hard‑coded styling for:
  - Customer header
  - Product header
  - Order #
  - Purchase order #
  - Expire Date
- Monospace and color cues for readability.


## [0.0.9] – Pre-release tinkering : 2025-04*
 - Basic work done on reviewing HTML structure and CSS rules on plantdemand.com, to evaluate workability of CSS overrides and potential for customization.

> [!NOTE]
> An asterisk by the date indicates that it is an approximation or best-guess.

## Planned / Unreleased
- Add example screenshots.
- Add more robust documentation to site, one section/topic at a time.
