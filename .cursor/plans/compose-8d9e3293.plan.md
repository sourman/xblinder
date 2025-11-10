<!-- 8d9e3293-7a05-4f4c-b92e-7aceacb2cf0c f052ca85-3214-47a6-b7c5-cf3ceaa1ddca -->
# Chrome Extension Plan

1. DOM Recon Summary

- Confirm the compose modal backdrop uses `div[role="presentation"]` with classes `css-175oi2r r-1pi2tsx r-13qz1uu r-1ny4l3l` and inline `background-color: rgba(0, 0, 0, 0);` inside a parent `div.css-175oi2r.r-sdzlij...` that also hosts the dialog.
- Note multiple `role="presentation"` siblings exist; the target is the one whose inline style controls the dimming layer and sits beside the `role="dialog"` container.

2. Extension Skeleton

- Create `manifest.json` (MV3) granting `https://x.com/compose/post` host permissions and injecting `content.js` on DOM load.
- Add `content.js` plus optional `styles.css` for reusable theming; ensure prettier-friendly formatting.

3. Backdrop Intensifier Logic

- In `content.js`, wait for page readiness then run a MutationObserver scoped to `document.body` to detect the modal parent (`div[role="dialog"]` and its siblings).
- Locate the backdrop via selector `[role="presentation"][style*="background-color"]` or by walking siblings of the dialog parent; set `style.backgroundColor` (e.g. `rgba(0,0,0,0.85)`) and `transition` for smoothness.
- Re-apply on attribute mutations to handle Twitter’s React re-renders, and guard against affecting unrelated presentation divs.

4. Future Enhancements (Optional)

- Add storage-backed options page to let user tweak opacity and color.
- Provide keyboard shortcut or toggle for quick enable/disable.

### To-dos

- [ ] Summarize modal overlay structure and identify reliable selectors.
- [ ] Set up manifest v3 and base files for the Chrome extension.
- [ ] Implement content script to detect compose modal and boost backdrop opacity.
- [ ] Outline optional user configurability for opacity.