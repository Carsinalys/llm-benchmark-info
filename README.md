# LLMRally — support & privacy site

Static support surface for the macOS app **LLMRally**, hosted on
GitHub Pages at `https://carsinalys.github.io/llm-benchmark-info/`.

No build step, no dependencies, no JavaScript required to read the contact
information — plain HTML + one stylesheet, so App Review's crawler always
sees the support email.

## Files

| Path | Purpose |
|---|---|
| `index.html` | Support page — contact, getting started, how it works, deep tier, FAQ, troubleshooting |
| `privacy.html` | Privacy policy — matches the App Privacy nutrition label (no data collected) |
| `assets/styles.css` | Design tokens mirrored from the app (blue accent, dark hero gradient) |
| `assets/icon-*.png` | App icon, generated from `scripts/gen_app_icon.swift` |
| `.nojekyll` | Serve files as-is, skip Jekyll processing |

## Enabling GitHub Pages

1. **Create the repository** on GitHub: `llm-benchmark-info` (under your
   account, so the Pages URL becomes `carsinalys.github.io/llm-benchmark-info/`).
2. Push these files to `main`.
3. Repository → **Settings** → **Pages**.
4. **Source:** Deploy from a branch. **Branch:** `main`, folder `/ (root)`. Save.
5. Wait for the first deploy, then confirm both URLs load over HTTPS.

## Paste into App Store Connect

| ASC field | Value |
|---|---|
| Support URL | `https://carsinalys.github.io/llm-benchmark-info/` |
| Privacy Policy URL | `https://carsinalys.github.io/llm-benchmark-info/privacy.html` |
| Marketing URL (optional) | leave empty, or reuse the support URL |

Apple checks that the support URL resolves, needs no login, works on a phone,
and offers a real contact method. All three are satisfied by `index.html`.

## Before submitting — fill these in

- [ ] Replace `© 2026 LLMRally` in both footers with the legal name
      used in the ASC **Copyright** field.
- [ ] Add the App Store link (and a download button) to `index.html` once
      the app is approved.
- [ ] Confirm the support hours and reply-time promise are ones you can keep —
      they are stated as Mon–Fri 09:00–18:00 UTC+3, reply within 2 business days.
- [ ] A postal address is offered "on request" in `privacy.html`. Some
      jurisdictions require it published; add it if yours does.

## Keeping it accurate

The page states facts that come from the codebase. Re-check them when the
app changes:

- **macOS 14+** — `deploymentTarget` in `LLMRally/project.yml`.
- **7 backends** — `BackendEndpoint.Kind.allCases` (ollama, lmStudio, mlx, llamaCpp, jan, vllm, koboldCpp + openAICompatible).
- **Free tier: 12 quality items** — `EvalBankLoader.liteBanks()` counts.
- **Deep tier: 90 quality items** — `EvalBankLoader.deepBanks()` counts.
- **$9.99 one-time** — `PurchaseCatalog.deep` product ID.
- **No data collected** — `PrivacyInfo.xcprivacy` has empty `NSPrivacyCollectedDataTypes`.
- **Zero third-party dependencies** — `LLMRally/project.yml` has no SPM packages.
- **No data uploads** — app has no `NSPrivacyTrackingDomains` and no upload code.
- Feature names match the app's UI: Results Book, capability radar, Arena, Deep Testing.

## Local preview

```bash
cd llm-benchmark-info
python3 -m http.server 8000
# then open http://localhost:8000/
```
