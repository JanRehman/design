# Haugenstua Bil Service AS — Webflow Setup Notes

Companion to `index.html`, built per the STUDIOFORM Webflow Master Prompt. The HTML file is fully self-contained and works as a static page; use these notes if porting the design into Webflow's free plan.

## 1. Design brief summary
"Garage-grade steel & diagnostic amber" — a workshop-at-night palette (graphite/steel) cut by an amber diagnostic glow, built specifically around the client's real specialty (bilelektro / feilsøking) rather than a generic "trusted mechanic" template. All facts on the page (address, phone, org. number, founding year, daglig leder) are verified against Brønnøysundregistrene / Proff.no / 1881 — no fabricated review counts or star ratings are presented as real.

## 2. Token system
See `:root` in `index.html` — accent `#FF7A1A` (diagnostic amber) on graphite `#12151A`/`#1B1F26`, type pairing Space Grotesk (display) + Inter (body), radii 4/8/16px.

## 3. Signature element
The **pulse divider**: a thin amber scan-line that sweeps left-to-right between every major section (`.pulse-divider`), echoing the shop's diagnostic equipment. It reappears as a waveform/ring motif in the hero visual.

## 4. Webflow Custom Code — Head
Paste into Page Settings → Custom Code → Head:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
```
Copy the `<style>` block from `index.html` into the same Head embed (or into Webflow's class-based styling if rebuilding natively — the design tokens map 1:1 to Webflow's custom CSS variables panel).

## 5. Webflow Custom Code — Body (before `</body>`)
Copy the `<script>` block from `index.html` verbatim. It handles: nav scroll state, mobile drawer, GSAP entrance reveals, hero waveform draw-in, hero parallax, and form validation.

## 6. Page structure notes
- Build each `<section id="...">` as a Webflow Section with the matching ID for anchor links (`#tjenester`, `#om-oss`, `#anmeldelser`, `#kontakt`).
- The contact form should use Webflow's **native form element** (works on free plan, 500 submissions/mo) — keep the same field names so any backend export still maps correctly.
- Replace the inline `<svg><symbol>` icon sprite with Webflow's embed component once, at the top of the page (Body start), exactly as in `index.html`.

## 7. IX2 interaction setup guide (optional, if not using the GSAP script)
| Interaction | Trigger | Settings |
|---|---|---|
| Section reveal (`.fade-in` elements) | While scrolling into view | Move up 24px → 0, Opacity 0→1, Ease Out Cubic, run once |
| Service card stagger | While scrolling into view | Stagger children 100ms |
| Nav background | Page scroll | At 60px: add `scrolled` background/blur class |
| Hamburger menu | Click | Rotate bars 45°/-45°, slide drawer down, fade overlay |

## 8. SEO checklist
- **Page title:** `Haugenstua Bil Service AS — Bilverksted og bilelektro på Grorud, Oslo`
- **Meta description:** `Haugenstua Bil Service AS er et lokalt bilverksted på Grorud i Oslo siden 2016. Service, EU-kontroll, bilelektro, dekk, bremser og feilsøking — for alle bilmerker.`
- **OG image:** a photo of the workshop exterior or a mechanic at work (real photography recommended over stock).
- **NAP consistency:** confirm phone (954 89 558), address (Haavard Martinsens vei 9, 0978 Oslo) and email match Google Business Profile exactly before publishing.

## Open items before publishing
- [ ] Confirm the contact email `post@haugenstuabilservice.no` with the client — not publicly verifiable, currently a placeholder based on the likely domain.
- [ ] Replace the three placeholder testimonials in `#anmeldelser` with real Google reviews once available.
- [ ] Add real photography (workshop, team, or vehicles) to strengthen trust — currently uses abstract iconography only.
