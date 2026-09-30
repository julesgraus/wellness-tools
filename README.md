# Wellness

A small, calm web app with exercises for moments of hyperventilation, stress and tension, plus an emotion thermometer to keep track of how you feel.

It is a single HTML file: no build step, no frameworks, no dependencies, no tracking. It works offline and can be installed on your phone's home screen.

> **The app's interface is in Dutch.** The code and documentation are in English.

> [!IMPORTANT]
> **This is not a medical tool.** The exercises and the thermometer can help you calm down and get to know yourself better, but they do not replace a doctor, psychologist or treatment. If you have doubts about your symptoms, contact your GP. In an emergency, call your local emergency number (112 in the Netherlands and the EU).

## Features

The app has five tabs:

| Tab                    | What it does                                                                                                                                                                                                                                                           |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ademen** (Breathe)   | Guided slow breathing. Choose a rhythm (3–5, 4–6 or 4–7–8 counts), follow a growing and shrinking circle or a scrolling wave, and optionally turn on soft surf sounds that follow your breath.                                                                         |
| **Spieren** (Muscles)  | Progressive muscle relaxation: tense a muscle group for 5 counts, release for 15. Seven muscle groups, about 3 minutes.                                                                                                                                                |
| **Rivier** (River)     | "Leaves on a stream", an exercise from Acceptance and Commitment Therapy. Type a thought and watch it drift away on a leaf. Nothing you type is stored.                                                                                                                |
| **Aarden** (Grounding) | The 5-4-3-2-1 grounding exercise: name things you see, feel, hear, smell and taste.                                                                                                                                                                                    |
| **Thermometer**        | Rate your body (*Lichaam*) and mind (*Hoofd*) from 0 (neutral) to 10 (very heavy), pick words that fit, add a note and save the moment. The *Verloop* view shows a chart, averages, the words that come up most at heavy and light moments, and a list of all moments. |

Also included:

- A disclaimer that is shown every time the app opens.
- Dark theme only.
- Works without an internet connection once loaded (service worker).
- Installable as a home-screen app (web app manifest).
- The screen stays on during an exercise (Wake Lock API, where supported).
- Fallback content when JavaScript is disabled.

## Privacy

Everything stays on your device.

- The thermometer stores its data in your browser's `localStorage`. Nothing is sent anywhere.
- Clearing your browser data removes your saved moments. Use **Back-up downloaden** (bottom of *Verloop*) to make a JSON backup, and **Back-up terugzetten** to restore it, for example on another device.
- **Exporteren voor Excel (CSV)** exports all moments as a CSV file.
- The app loads no external scripts, fonts or analytics.

## Getting started

### Run it locally

Open `index.html` in a browser. That is all.

Offline support needs the app to be served over HTTPS, so the service worker is not registered when you open the file directly. To test it the way it runs online, serve the folder, for example:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Project structure

```
index.html            The whole app: HTML, CSS and JavaScript
sw.js                 Service worker for offline use
manifest.webmanifest  Web app manifest (name, colours, icons)
icon-180.png          Apple touch icon
icon-512.png          App icon
```

## Development

Everything lives in `index.html`. A comment at the top of the file explains its structure and lists a searchable marker for every part of the app, for example:

- `[CSS] BREATHE`, `[HTML] BREATHE`, `[JS] BREATHE`
- `[CSS] THERMOMETER`, `[HTML] THERMOMETER`, `[JS] THERMOMETER`

Search for a marker to jump to the right place.

A few things to know:

- **Modern browsers only.** The JavaScript targets current evergreen browsers (ES2022+); there are no fallbacks for old browsers.
- **Two module scripts.** Both are inline `<script type="module">` blocks. The first holds breathing, muscles, river, grounding, tabs and the disclaimer. The second is the thermometer, self-contained.
- **Tab events.** When a tab becomes visible, its panel receives a `tabshown` event. The thermometer uses this to redraw its chart.
- **Storage key.** Thermometer data is saved under `emotiethermometer.v1`. Changing this key makes previously saved moments invisible.
- **Bump the cache version.** When you publish a new version of `index.html`, increase `VERSION` in `sw.js`. Otherwise installed apps keep serving the old, cached file.

## Background and sources

The exercises are based on commonly used techniques. The app links to these sources:

- Breathing: [Birdee et al. (2023), slow breathing and longer exhalation](https://pmc.ncbi.nlm.nih.gov/articles/PMC10395759/) · [review of resonance breathing (2024)](https://link.springer.com/article/10.1007/s10484-024-09637-2) · [Gezondheid en Wetenschap: hyperventilatie](https://www.gezondheidenwetenschap.be/richtlijnen/hyperventilatie)
- Muscle relaxation: [Manzoni et al. (2008), meta-analysis of relaxation training for anxiety](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2427027/) · [systematic review of muscle relaxation for stress, anxiety and depression](https://www.utupub.fi/handle/11111/50540)
- Leaves on a stream: [A-Tjak et al. (2015), meta-analysis of ACT](https://pubmed.ncbi.nlm.nih.gov/25547522/) · [explanation of the exercise (GoodTherapy)](https://www.goodtherapy.org/blog/leaves-on-a-steam-cognitive-defusion-exercise/)

## Notes
All my projects up till september 2026 were 100% made by manual labour, build up in 20 years of experience. This project was mostly vibe coded using claude.
This tool is the successor of the original tool over here: https://github.com/julesgraus/Spanningsthermometer