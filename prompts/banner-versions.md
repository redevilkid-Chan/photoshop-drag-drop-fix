# Banner Prompts · Photoshop Drag & Drop Fix

> Three independent prompts for GitHub README hero banner generation.
> Model: `gpt-image-2.5-sunburst` (current OpenAI SOTA image model).
> Target output: 1920×576 pixels (10:3 landscape, matching `banner.png` aspect ratio).
> **Same subject, three radically different visual styles.**

---

## How to Use — Generate 3 Independent Versions

This file contains **3 distinct prompts** (V1, V2, V3). Each one produces a **completely independent banner image** from the same brand content.

Workflow:

1. Open ChatGPT (Plus / Pro account required for image generation).
2. **Prompt V1 → send → save the image** (do not combine with V2/V3 in one turn).
3. **Start a new conversation → Prompt V2 → send → save.**
4. **Start a new conversation → Prompt V3 → send → save.**
5. Compare the 3 results side-by-side and pick the one that fits your repo tone best.

Each conversation produces one image. Three conversations = three independent banner versions.

You can also use the OpenAI API directly:

```python
from openai import OpenAI
client = OpenAI()
response = client.images.generate(
    model="gpt-image-2.5-sunburst",
    prompt="<paste prompt V1 here>",
    size="1920x576",
    quality="high",
)
```

---

## Version Comparison

| Version | Style | Background | Primary Palette | Vibe |
|---|---|---|---|---|
| **V1** | Engineering Blueprint | Warm cream paper #f5f0e6 | Black ink + navy accent | IKEA assembly manual |
| **V2** | CRT Terminal / Y2K Hacker | Pure black + scanlines | Amber green + beige case | 1996 Compaq Presario |
| **V3** | Swiss International / Bauhaus | Cream + halftone texture | Black / red / navy / green | 1968 Brauhaus student work |

---

## V1 · Engineering Blueprint

**Style**: Brutalist technical line drawing + 80s technical manual. Completely abandons dark-tech aesthetic in favor of **light paper + single-color lines**, like an IKEA assembly manual.

**Preserves**: file icon, drag arrow, monitor, "Ps" identifier, ✅, main title, 3-STEP DIAGNOSTIC, MIT footer.
**Subverts**: ✅ is **not a green circle** but a **red square frame around a green tick** (engineer's approval stamp). Background is cream paper, not dark blue. Monitor is navy-blue line drawing with no fill and no gradient.

```text
GOAL
Generate a GitHub README hero banner for the open-source project "Photoshop Drag & Drop Fix", 10:3 landscape, target size 1920x576 pixels (matching banner.png aspect ratio).
Overall style: engineering blueprint / technical manual. Not a tech product hero.

SUBJECT
Core elements: file icon → drag arrow → monitor → green ✓, all rendered as technical line drawings.

COMPOSITION
- Monitor line drawing center-left, 35% width
- File icon and arrow on its left
- Generous whitespace on right, only main title block in bottom-right
- Dashed callout lines between elements with labels: "scale", "drag vector", "Ps v27.x"
- Top-left: a red rubber stamp "BUILD #1.0 / APPROVED"
- Bottom-right: a version block "DOC-PS-DRAGDROP / REV 001"

VISUAL LANGUAGE
- Background: warm cream #f5f0e6 (engineering paper)
- Primary: black ink lines (pen / technical pen), 2px main strokes, 0.5px dashed guides
- Monitor line art: dark blue (#1a3a6e) single-color outline, no fill, no gradient
- File icon: black outline, 3 thin horizontal lines for text
- Drag arrow: black solid line + arrowhead, with callout "DRAG MOTION = 100%"
- Checkmark: red square frame around a green tick mark (like an engineer's approval stamp), NOT a green circle
- Typography: monospace (Menlo / Consolas / Courier New)
- No emoji. No gradients. No shadows.

TEXT (exact, case-sensitive)
Title line 1: PHOTOSHOP
Title line 2: DRAG & DROP FIX
Subtitle: 3-STEP DIAGNOSTIC · READY FOR DEPLOY
Footer: MIT LICENSE / BUILD 2026 / WINDOWS 10/11

PRESERVE
Do not become a dark tech poster. Do not add Photoshop blue (#31a8ff). Do not change the red stamp to green.

NEGATIVE
- no dark background
- no gradients
- no neon / glow
- no emoji
- no photography
- no human figures
- no 3D rendering

SUCCESS CHECK
Looks like a tool manual you can glance at on a desk and find the answer, not a SaaS landing page.
```

---

## V2 · CRT Terminal

**Style**: 1990s CRT terminal + early internet + Windows 95 blue screen. **The most counterintuitive version**: repackages the tool announcement as retro command-line aesthetic.

**Preserves**: monitor, file icon, drag arrow, ✅, main title, 3-STEP DIAGNOSTIC, MIT footer.
**Subverts**: monitor screen displays **real command-line interaction** `PS C:\> drag image.png` + `> STATUS: OK`. Background is pure black + scanlines. Green and amber are primary colors (not blue). ✅ is **not an icon** but **green text on the screen**.

```text
GOAL
Generate a GitHub README hero banner for "Photoshop Drag & Drop Fix", 10:3 landscape, target size 1920x576 pixels (matching banner.png aspect ratio).
Overall style: 1990s CRT terminal aesthetic. Not a modern tech product hero.

SUBJECT
Core elements: file icon → drag arrow → monitor → green ✓, all rendered in CRT terminal style.
Monitor screen displays actual command-line interaction content.

COMPOSITION
- Monitor left, 40% width, screen content is the focal point
- Screen top line: PS C:\> _ with blinking cursor
- Screen middle: mocked drag-drop command output
- Screen bottom: green text > STATUS: OK
- Right area: 3 lines of large text stacked vertically

VISUAL LANGUAGE
- Background: pure black #0a0a0a, with CRT scanlines (2px spacing, 3% green opacity)
- Monitor chassis: beige #c8c2b6 (90s PC case), rounded corners
- Monitor bezel: dark gray #2a2a2a with physical LED indicators (small green + red dot)
- Screen interior: deep black #001000 with amber/green monochrome text (mono font)
- CRT effect: vignetting at screen corners, slight convex bulge in center
- Screen text content:
    PS C:\Users\dev\Pictures> drag image.png
    > [OK] imported as layer
    > [OK] 3-step diagnostic complete
    > STATUS: READY
- Screen top-right small text: v1.0.0
- Right side large text (amber green #ffae00):
    >PHOTOSHOP
    >DRAG & DROP FIX
    >[DIAGNOSE-ONLY]
- Footer (gray-green #5a8070): MIT // WINDOWS 10/11 // 2026
- Slight dot matrix noise across image (2% opacity) for CRT wear
- Dust band on monitor bottom edge

TEXT (exact, case-sensitive)
All CRT text must be character-exact.
Right side title: >PHOTOSHOP / >DRAG & DROP FIX / >[DIAGNOSE-ONLY]
Footer: MIT // WINDOWS 10/11 // 2026

PRESERVE
No modern SaaS aesthetic (no gradients, blur, glassmorphism). No blue palette. Green and amber are primary colors.

NEGATIVE
- no gradients
- no glass / blur
- no modern flat illustration
- no emoji
- no human figures
- no photographs
- no corporate cleanliness
- no "sleek" or "minimal"

SUCCESS CHECK
Looks like a screenshot from a 1996 Compaq Presario, not a 2026 MacBook Pro.
```

---

## V3 · Bauhaus Poster

**Style**: Swiss International Typographic Style (Wim Crouwel / Massimo Vignelli / Müller-Brockmann). **Strongest anti-AI flavor**: repackages the tool banner as art-grade poster.

**Preserves**: file icon, monitor, "Ps" identifier, ✅, main title, 3-STEP DIAGNOSTIC, MIT footer.
**Subverts**: ✅ is a **giant green circle** (1.2× main title font size), not a badge. Background is cream printing paper + halftone texture, not dark blue. Typography is Helvetica Bold, all caps, not rounded sans. Palette limited to **black / red / navy / green**, no Photoshop blue (#31a7ff) allowed.

```text
GOAL
Generate a GitHub README hero banner for "Photoshop Drag & Drop Fix", 10:3 landscape, target size 1920x576 pixels (matching banner.png aspect ratio).
Overall style: Swiss International Typographic Style / Bauhaus poster. Not a tech product hero.
Treat it as a 1968 Brauhaus student work, not a SaaS landing page.

SUBJECT
Keep core elements but render all as geometric, flat, single-color blocks.
File = rounded rectangle. Monitor = rectangle + rounded corners. Checkmark = circle. Drag arrow = thick black horizontal line.

COMPOSITION
- Canvas divided by Swiss grid: 6 columns horizontal, 4 rows vertical
- Monitor line art occupies top-left 4 columns × 2.5 rows
- Monitor left: small file block (pure red #e63946), with thick black arrow between them
- Main title: PHOTOSHOP occupies right half of canvas, very large, Helvetica Bold
- Subtitle: Drag & Drop Fix below main title, medium size
- Bottom-right: green checkmark circle (diameter = 1.2× main title font size) as visual anchor
- Bottom-left: small text MIT // 2026 // WINDOWS, monospace
- Whitespace 30%+ of canvas
- No rounded card frames, no shadows, no glow

VISUAL LANGUAGE
- Background: cream #f2ede0 (1970s poster paper)
- Primary text: pure black #000000, Helvetica Bold / Akzidenz Grotesk
- Main title font size = 18% of canvas height
- Red #e63946 for file icon + one corner color block
- Black #000000 for all lines and text
- Navy blue #1d3557 for monitor frame
- Green #06a77d for checkmark circle
- Monitor: navy blue stroke, black Ps character centered, white interior
- All strokes 2px uniform thickness
- Subtle 3% opacity halftone dot texture across poster (offset printing feel)
- No shadows. No glow. No blur. No glass.

TEXT (exact, case-sensitive)
Title line 1: PHOTOSHOP
Title line 2: DRAG & DROP FIX
Subtitle: THREE-STEP DIAGNOSTIC
Footer: MIT // 2026 // WINDOWS

PRESERVE
Not a dark tech poster (no dark blue background). Red / cream / black / navy blue is the limited palette. Checkmark circle must be green, not another color.

NEGATIVE
- no dark background
- no gradients
- no glow / blur
- no glassmorphism
- no emoji
- no 3D rendering
- no skeuomorphism
- no "sleek modern minimal"
- no corporate blue (#31a7ff)

SUCCESS CHECK
Looks like a 1968 Brauhaus student project, not a Figma template.
Printed in black / white / red / navy on cream paper.
```

---

## Notes

1. **GPT Image text rendering is unreliable** — Even when the prompt says "TEXT exact, case-sensitive", roughly 50% of generated images have 1–2 misspelled or swapped characters. If text comes out wrong, fix it in Photoshop / Illustrator / any vector tool after generation.

2. **Size** — GPT Image 2 / 2.5 supports **arbitrary sizes** via the `size: "WIDTHxHEIGHT"` parameter. Constraints: width and height must each be divisible by 16, aspect ratio must be in the range 1:3 to 3:1, and the maximum is 3840×2160 (above 2560×1440 is experimental).
   - **1920×576** passes the divisible-by-16 check (1920÷16 = 120, 576÷16 = 36). The aspect ratio is 3.33:1, which is *just above* the documented 3:1 upper limit — the API may accept or may return 400. If it rejects, fall back to one of these close alternatives:
     - `1920×640` (3:1 exact)
     - `1792×576` (3.11:1)
     - `2048×640` (3.2:1)
   - All three preserve the same horizontal layout.

3. **Each generation is a lottery** — `gpt-image-2.5-sunburst` is non-deterministic. Generate 2–3 images per prompt and pick the best one.

4. **If none of the 3 versions look right** — the highest-leverage change is in the **VISUAL LANGUAGE** block. Swapping 1–2 keywords there (e.g. "glassmorphism" ↔ "brutalist", "amber" ↔ "cyan") reshapes the entire style without breaking subject recognition. Modifying SUBJECT usually breaks brand consistency instead.

5. **Always send each prompt in a separate conversation turn** — do not paste V1+V2+V3 into the same message. Each deserves an independent generation.

---

## Model & Endpoint

- **Model**: `gpt-image-2.5-sunburst` (current SOTA, highest fidelity)
- **Fallback**: `gpt-image-2.5-flare` (faster, slightly lower quality, good for batch drafts)
- **Endpoint**: `POST /v1/images/generations`
- **Auth**: environment variable `OPENAI_API_KEY`
- **Quality parameter**: `quality=high` for first attempt, `quality=xhigh` or `max` if available in your account for final pick
- **Pricing reference**: 1K + 1K low ≈ $0.01 per image; 1K + 1K high ≈ $0.25 per image; 1792×1024 high ≈ $0.25 per image