# TM Zierpflanzen – modern page with photo plant assistant

A design concept for tmzierpflanzen.de with a chatbot that can identify a plant from a photo and answer plant-care questions.

**File:** `tm-zierpflanzen-modern.html` (one self-contained file: HTML, CSS and JavaScript)
**Live preview:** https://claude.ai/artifact/PziFf3CGZut94DswfpumBN

## What it contains

| Part | Description |
|---|---|
| Header and hero | Headline, call-to-action buttons, "Pflanze per Foto erkennen" button |
| Care-guide cards | Standort, Winterhart, Wuchsform, Lebensdauer, Standplatz (link to the shop categories) |
| Sustainability section | Local production, integrated pest control, recycled packaging |
| Recycled pots section | PE-recycled plant pots, link to the press release |
| Footer | Address, phone, links to Kontakt, Karriere, Impressum, Datenschutz |
| Plant assistant | Chat window (bottom right) with text questions and photo upload |

The page is responsive (phone and desktop) and follows the visitor's light or dark mode.

## How the plant assistant works

1. The visitor types a question or uploads a photo (the 📷 button).
2. The page sends the question, the photo and the list of the 10 plants to Claude.
3. Claude answers in German, in at most 4 sentences.
4. **If it is sure:** it gives the plant name and care tips, plus a card with a link to the product page.
5. **If it is not sure:** it says "Ich denke, das ist X, bin mir aber nicht sicher" and shows up to 3 numbered options. The visitor taps a button or types 1, 2 or 3. Then the assistant gives care tips for that plant.
6. Questions that have nothing to do with plants are politely declined.

Claude only matches photos to the plants on the list. For other plants it says so and gives general advice.

## Plants the assistant knows

| Code | Plant |
|---|---|
| keyqauam | Ageratum houstonianum / Leberbalsam |
| 07VP4X39 | Anemone / Windröschen |
| VEEDOP4N | Antirrhinum / Löwenmaul |
| JST34YJT | Asparagus densiflorus / Zierspargel |
| ERTMZCTR | Aster novi belgii / Glattblatt-Aster |
| SBWH5FY7 | Astilbe / Prachtspiere |
| 3FPD9UP4 | Asteriscus maritimus / Goldtaler |
| V7MMNZG5 | Bacopa / Schneeflockenblume |
| EONAT8V5 | Begonia elatior / Zimmerbegonie |
| TNRDUNOC | Begonia semperflorens / Eisbegonie, Kirschblüten |

### Add a plant

In the file, find the `PL` list in the `<script>` at the bottom and add an entry:

```js
{id:'ABC12345', n:'Name / Deutscher Name', s:'Kurze Pflegeinfo in einem Satz', u:'produkt-adresse-ohne-domain'}
```

- `id` is the plant code from the label.
- `n` is the name shown on the card.
- `s` is the short care text shown on the card and given to the AI as a hint.
- `u` is the last part of the product address: `https://www.tmzierpflanzen.de/produkt/` + `u` + `/`.

Put a comma between entries. A missing quote or comma stops the whole script.

## Change the colors

All colors are variables at the top of the file, in `:root`. Light mode and dark mode each have their own set.

| Variable | Use | Light value |
|---|---|---|
| `--bg` | Page background | #F9F9F7 |
| `--surface` | Cards, chat window | #FFFFFF |
| `--ink` | Text | #0D1A14 |
| `--muted` | Secondary text | #5A6660 |
| `--line` | Borders | #E0E0E0 |
| `--green` | Buttons, links | #137A5A |
| `--accent` | Highlights, logo | #1D9E75 |
| `--soft` | Light green tint | #E1F5EE |
| `--dark` | Dark sections, chat header | #0D1A14 |

The current palette is taken from the TUPAG group code. It has not been checked against the exact colors on tmzierpflanzen.de. Send the real hex codes to match them exactly.

## Change the assistant's behavior

The instructions for the AI are in the `RULES` text in the script (language, answer length, how careful it is with photos, the JSON answer format). To change the tone or add rules, edit that text.

## Important limits

- **The photo assistant only works inside Claude.** The page uses Claude's built-in "sample" feature. The first use asks for permission and counts toward the viewer's Claude usage. Where Claude is not available, the chat button is hidden.
- **For your own website** (for example WordPress), the chat needs a small server that receives the photo and sends it to an AI service. The access key must stay on that server and never in the page code.
- **Images:** the concept uses emoji instead of photos. Published pages cannot load images from other websites. On a real site, use your own plant photos.
- **Accuracy:** similar plants (for example the two begonias, or Aster and Astilbe) can be confused. Blurry photos, poor light, or photos with only leaves make it worse. That is why the assistant offers numbered options when it is unsure.
- **Privacy:** photos and questions are sent to an AI service. On a real website, add a notice to your Datenschutz page and consider a short note under the chat input.

## Open items to check

- Zimmerbegonie product link ends in `...zimmerbegoniey`. Open it to check that it works.
- Confirm that you may use product images from tmzierpflanzen.de when you add them.
- Send the real brand colors and logo.
- Test the assistant with photos of each of the 10 plants and tell me which ones it gets wrong.

## Related project: TUPAG website with keyword chatbot

A separate project (`website/` folder with `index.html`, `css/style.css`, `js/plants.js`, `js/rules.js`, `js/chat.js`) holds the TUPAG group page. Its chat answers from fixed keyword rules and the same 10 plants, and supports QR links such as `index.html?plant=07VP4X39`. It has its own README inside the folder.
