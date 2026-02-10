# PlantDemand UI Tweaks — UserCSS (global + per‑section controls)

Global defaults with per‑section overrides (fonts, sizes, colors) for **plantdemand.com**.  
Designed for the **Schedule** view (per location/plant). Uses a “don’t break what works” approach: minimal selectors, stable attributes when available, and explicit toggles for colors/backgrounds.

---

## Quick install

1) **Install Stylus** (browser extension):
   - **Edge / Chrome**: <https://chromewebstore.google.com/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne>  
     (Edge users: allow Chrome Web Store installs in `edge://extensions`)
   - **Firefox**: <https://addons.mozilla.org/en-US/firefox/addon/styl-us/>

2) **Install this style** (opens the .user.css in Stylus):  
   👉 <https://exirtis.github.io/plantdemand-userstyle/PlantDemand.user.css>

3) Open **Stylus → Manage → PlantDemand UI Tweaks**, and adjust the per‑section options (`@var` controls).

> ✳️ This style ships with `@downloadURL`/`@updateURL` and version tags, so **Stylus can auto‑update** when a new version is published. You can also use “Check for update” in Stylus at any time.

---

## What it changes (high level)

- **Global font** selection (system preset, common presets, or a custom stack)
- **Per‑section font** source (inherit global / preset / custom), **font size**
- **Per‑section text color** (toggle on/off)
- **Per‑section background color** (toggle on/off) **with alpha/opacity**
- Optional **`!important`** switch to win specificity battles without noisy overrides
- Targets: **Customer header “pill”**, **Product header**, **Order #**, **PO #**, **Expire Date**, **Load Time**

> Scope: built/tested against **Schedule** view. Additional resilience for different **group‑by modes** (e.g., MATERIAL) is in progress; selectors prefer `data-*` / ARIA attributes over hashed CSS module classes where possible.

---

## Configuration (where to look)

Open Stylus → Manage → click the style → adjust the controls. The most common toggles:

- **Global font**: `fontPreset`, `fontCustom`
- **Customer (group header)**: `customerFontMode/preset/custom/size`, `customerUseBg + customerBgColor + customerBgAlpha`, `customerUseColor + customerColor`
- **Product / Order # / PO # / Expire Date / Load Time**: each has matching controls:
  - `XFontMode/preset/custom/size`
  - `XUseBg + XBgColor + XBgAlpha`
  - `XUseColor + XColor`
  - (Order # adds an optional **bold** toggle)

> Tip: If something doesn’t seem to apply, try turning on the **`!important`** master switch.

---

## Known limitations / notes

- **CSS module classnames** on PlantDemand can be hashed and may change. This style tries to anchor on **stable attributes** like `data-testid` / `data-field` whenever available.
- The style is built from the **Customer‑grouped** view first; support for **Material‑grouped** (and others) is being hardened.
- If PlantDemand updates markup, you may need to update selectors (open an issue with a small HTML snippet).

---

## Troubleshooting

- **No changes visible?**  
  - Confirm the site domain matches Stylus scope (`plantdemand.com`).  
  - Toggle the style on/off in Stylus to ensure it’s active.  
  - Try enabling the **`!important`** setting.  
  - If a section still doesn’t apply, open DevTools → Inspect the element and file an issue with the **outerHTML** of the header/field (see *Contributing*).

---

## Contributing

Issues and PRs welcome. When reporting a selector problem, please include:

- **Which view** (e.g., Schedule: Customer vs. Material grouping)
- **Minimal outerHTML** for the element that should be styled  
  (From DevTools: select the smallest ancestor that visually bounds the text → Right‑click → **Copy → Copy outerHTML**)

Repo: <https://github.com/Exirtis/plantdemand-userstyle>  
Issues: <https://github.com/Exirtis/plantdemand-userstyle/issues>

---

## Versioning & updates

- This project bumps `@version` in the UserCSS header on every release (e.g., `1.0.8 → 1.0.9`).
- `@downloadURL` and `@updateURL` point to the GitHub Pages URL so **Stylus can fetch updates automatically**.
- See **[CHANGELOG.md](./CHANGELOG.md)** for detailed changes.

Hosted CSS (direct):  
`https://exirtis.github.io/plantdemand-userstyle/PlantDemand.user.css`

---

## License

[MIT](./LICENSE) © Chad (Exirtis)
