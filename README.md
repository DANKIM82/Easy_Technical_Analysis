# 📊 Easy Technical Analysis

> A friendly, beginner-first technical analysis tool that explains chart patterns the way a doctor explains a diagnosis.
>
> 차트 분석을 의사가 진료하듯 설명하는 친근한 도구입니다.

[![GitHub Pages](https://img.shields.io/badge/demo-live-2d8659?style=flat-square)](https://dankim82.github.io/Easy_Technical_Analysis/)
[![License](https://img.shields.io/badge/license-MIT-1d2230?style=flat-square)](#license)
[![No Build](https://img.shields.io/badge/build-none-d9881a?style=flat-square)](#tech-stack)
[![Made with](https://img.shields.io/badge/made_with-vanilla_JS-d94626?style=flat-square)](#tech-stack)

**[🔗 Live Demo](https://dankim82.github.io/Easy_Technical_Analysis/)** · **[🎓 Chart School](https://dankim82.github.io/Easy_Technical_Analysis/learn.html)**

---

## Overview

Easy Technical Analysis is a single-page web app that translates intimidating stock charts into plain-language diagnoses. It is built for fundamental analysts and beginner investors who want a second opinion from technical indicators without learning a new vocabulary.

The project consists of two pages:

- **Stock Clinic** (`index.html`) — Enter a ticker and receive a doctor-style readout: a mood verdict, five "vital signs," support/resistance levels, and a three-step action plan.
- **Chart School** (`learn.html`) — A six-lesson interactive tutorial (trend lines, support, resistance, moving averages, RSI), followed by five real-world case studies and short biographies of six founders of technical analysis.

The design language is hand-drawn and conversational — large emojis, dashed borders, hard shadows, and warm cream tones — chosen to lower the cognitive barrier for users who find conventional trading platforms hostile.

이 프로젝트는 차트가 어렵게 느껴지는 사람들을 위한 단일 페이지 웹 앱입니다. 진료소 컨셉으로 차트를 진단하고(`index.html`), 학교에서 차트 보는 법을 배웁니다(`learn.html`).

---

## ✨ Features

### Stock Clinic

| Module | Description |
|---|---|
| **Diagnosis Card** | Six mood states (🚀 strong uptrend, 💪 healthy, 🌊 ranging, 🥶 cooling, 🐻 downtrend, 🤔 mixed) derived from MA50/MA200 alignment and RSI. |
| **Five Vital Signs** | Trend, RSI(14), 52-week position, volatility, and a composite traffic-light score — each with traffic-light coding. |
| **Support / Resistance** | Pivot-point clustering (top 3 by touch count) with star ratings based on touch frequency. |
| **Time-range Toggle** | 6M / 1Y / 2Y / 5Y views from a single 5-year fetch (MA200 stays valid in shorter views). |
| **Hand-drawn Annotations** | Caveat-font handwritten notes on resistance/support, pulsing current-price marker, "you are here" speech bubble, crosshair tooltip on hover. |
| **Smart Search** | Korean / English / ticker substring autocomplete. 115 stocks across 6 categories (US, Korea, Japan, China, ETFs, indices). |
| **Cross-Page Help** | "?" buttons on every vital sign and S/R box link directly to the relevant Chart School lesson. |

### Chart School

| Section | Description |
|---|---|
| **6 Interactive Lessons** | Duolingo-style trace exercises: click-to-draw uptrend lines, downtrend lines, support, resistance; live MA-period slider; RSI thermometer slider. |
| **5 Real Case Studies** | NVDA 2023 (+240%, healthy uptrend), TSLA 2020 (+700%, parabolic warning), Kakao 2021–22 (-69%, broken trend), Samsung 2022–24 (range-bound), META 2022 (-73%, broken MA200). |
| **6 Legend Profiles** | Charles Dow, Jesse Livermore, Richard Wyckoff, Welles Wilder, Steve Nison, John Bollinger — each with a custom SVG portrait in the style of digital artist deekay (round face, dot eyes, blush cheeks). |
| **Progress Tracking** | Six progress dots fill as lessons are completed; a graduation card appears at the end. |

---

## 🧭 Design Philosophy

Most retail trading interfaces optimize for information density. This project optimizes for the opposite: **emotional accessibility**. The user is treated as a patient seeking a second opinion, not as a power user processing data.

Three principles shape every UI decision:

1. **Plain language over jargon.** "RSI 72" is annotated as "차트가 너무 뜨거워요 🔥" (the chart is too hot). Every indicator includes a one-line interpretation.
2. **Honest limitations.** The app explicitly states when signals conflict and never claims to predict prices. The graduation copy reads "만능은 아니에요" (this isn't a silver bullet).
3. **Visible learning paths.** Every diagnostic concept on the Clinic page links to the corresponding lesson in the School. Users can fill knowledge gaps in-context.

대부분의 트레이딩 도구가 정보 밀도를 높이는 방향으로 설계되는 반면, 이 프로젝트는 **감정적 접근성**을 우선합니다. 사용자를 파워 유저가 아니라 진료받으러 온 환자로 봅니다.

---

## 📸 Screenshots

> Add screenshots in `/screenshots/` and reference them here once captured.
> 스크린샷은 추후 `/screenshots/` 폴더에 추가 예정.

```
[Clinic — diagnosis card]    [Clinic — vital signs]    [Clinic — chart with annotations]
[School — lesson 4 trace]    [School — case study]     [School — legends grid]
```

---

## 🛠️ Tech Stack

| Layer | Choice | Rationale |
|---|---|---|
| **Frontend** | Vanilla HTML / CSS / JavaScript | No build step, no framework runtime, instant load. |
| **Charts** | Hand-rolled inline SVG | Full control over hand-drawn aesthetic; no library bloat. |
| **Data** | Yahoo Finance + Stooq via 5 CORS proxies | Multi-source fallback chain with 9-second timeout per attempt. |
| **Fonts** | Bricolage Grotesque, Gowun Dodum, Caveat, JetBrains Mono | Display / Korean body / handwritten / numeric. |
| **Hosting** | GitHub Pages | Static hosting, zero infrastructure cost. |

### Data Fetching

The app fetches five years of daily bars on first load and slices locally for shorter views (so the 200-day MA stays valid even in the 6-month window). Symbol mapping handles `.KS` / `.KQ` (Korea), `.T` (Japan), `^GSPC` and similar (indices). When Yahoo Finance is unreachable, Stooq is tried as a fallback, each through a rotating chain of CORS proxies.

5년 일봉을 한 번에 받아서 클라이언트에서 슬라이싱하기 때문에 짧은 기간에서도 200일선이 유효합니다.

### Algorithms

- **SMA** — Rolling average, returns null until enough data accumulates.
- **RSI(14)** — Wilder's smoothing.
- **Pivot detection** — 8-bar window, clusters within 2.5% of price range, requires ≥2 touches, returns top 3 by touch count.
- **Verdict logic** — Six mood states from a truth table over `above50`, `above200`, `golden`, and RSI thresholds.

---

## 🚀 Getting Started

### Use it now (recommended)

Visit the live demo: **[dankim82.github.io/Easy_Technical_Analysis](https://dankim82.github.io/Easy_Technical_Analysis/)**

### Run locally

```bash
git clone https://github.com/DANKIM82/Easy_Technical_Analysis.git
cd Easy_Technical_Analysis
# any static server works:
python3 -m http.server 8000
# or:
npx serve
```

Then open `http://localhost:8000`.

> No build step, no `npm install`, no environment variables. The two HTML files are completely self-contained.
>
> 빌드 단계 없음. HTML 파일을 그대로 열기만 하면 됩니다.

---

## 🗺️ Roadmap

### Implemented
- [x] Stock Clinic with 5 vital signs
- [x] Multi-source data fetching with proxy fallback
- [x] Time-range toggle (6M / 1Y / 2Y / 5Y)
- [x] Korean / English / ticker autocomplete (115 stocks)
- [x] Chart School with 6 interactive lessons
- [x] 5 real-world case studies
- [x] 6 legend profiles with custom SVG portraits
- [x] Bidirectional Clinic ↔ School linking

### Planned
- [ ] **Watchlist** — Star button on Clinic, persistent via `localStorage`. (Highest priority next.)
- [ ] **Bidirectional case ↔ lesson links** — Lesson pages link to relevant case studies.
- [ ] **Daily Discovery** — Surface a fresh interesting chart on each visit.
- [ ] **Comparison Clinic** — Diagnose two tickers side by side.
- [ ] **Sector Heatmap** — At-a-glance view of sector strength.
- [ ] **Bollinger Bands** — As promised in John Bollinger's profile.
- [ ] **Volume Analysis** — Wyckoff-style accumulation/distribution detection.

---

## 🤝 Contributing

This is a personal portfolio project, but issues and suggestions are welcome.

If you find a bug, a misleading explanation, or a chart that diagnoses incorrectly, please [open an issue](https://github.com/DANKIM82/Easy_Technical_Analysis/issues) with the ticker and a brief description.

이 프로젝트는 개인 포트폴리오지만 이슈나 제안은 환영합니다.

---

## ⚠️ Disclaimer

This project is for **educational purposes only**. Nothing in the Stock Clinic or Chart School constitutes investment advice. Technical indicators describe what has happened, not what will happen. Markets are uncertain; past performance does not predict future results.

Always do your own research and consult a licensed financial advisor before making investment decisions.

이 도구는 **교육 목적으로만** 만들어졌으며 투자 권유가 아닙니다. 기술적 지표는 과거를 설명할 뿐 미래를 예측하지 않습니다. 투자 결정은 본인의 책임 하에 하시기 바랍니다.

---

## 📜 License

MIT License — see [LICENSE](LICENSE) for details.

```
Copyright (c) 2026 DANKIM82

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

## 🙏 Acknowledgments

- Market data: [Yahoo Finance](https://finance.yahoo.com/) (unofficial endpoints), [Stooq](https://stooq.com/)
- CORS proxies: corsproxy.io, allorigins.win, codetabs.com, thingproxy
- Fonts: Google Fonts (Bricolage Grotesque, Gowun Dodum, Caveat, JetBrains Mono)
- Portrait illustrations inspired by the visual style of digital artist [deekay](https://twitter.com/deekaymotion)
- The six chart legends — for inventing every concept this app uses

---

<sub>Built in Tokyo · 2026 · 📊 주식 진료소</sub>
