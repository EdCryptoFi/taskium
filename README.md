# Taskium — Personal Dashboard

> Your personal OS in the browser. AI, crypto, weather, to-dos, quick links and more — fully customizable, zero install.

![Taskium Dashboard](https://myorganizer.pages.dev/og-image.png)

🔗 **Live demo:** [myorganizer.pages.dev](https://myorganizer.pages.dev)

---

## What is Taskium?

Taskium is a **single-file** personal dashboard built with Vanilla JS — no frameworks, no build step, no dependencies (except optional Supabase for cloud sync). Drop `index.html` anywhere and it just works.

### Highlights

- 🎯 **Focus Mode** — hides all widgets except Clock and To-Do to eliminate distractions. Something Notion and ClickUp don't do natively.
- 🧩 **Free-position grid** — drag cards anywhere on a dot-grid canvas, resize them freely
- 📈 **Trading module** — Favoritos, Perps/Spot/Prediction, Yield/DeFi link hubs
- 🔧 **Builder module** — Dev Deck, LLMs, Image & Video AI tools
- 🌤 **Live weather** — via Open-Meteo + ip-api (no API key needed)
- 📊 **Crypto tracker** — real-time prices via CoinGecko
- 🤖 **AI Prompt widget** — OpenAI & Claude integration
- ✅ **To-Do list**, ⏱ **Pomodoro timer**, 💬 **Daily Quote**
- 🌍 **PT / EN / ES** multilingual
- 🎨 **6 themes** — Dark, Light, Cyberpunk, Matrix, Ocean, Sunset
- 💾 **Supabase sync** — optional cloud persistence across devices
- 📱 **Responsive** — mobile-friendly stacked layout

---

## Modes

| Mode | Description |
|------|-------------|
| 🏠 Generic | Clock, Weather, Links, Notes |
| 📈 Trading | Market Radar, Alpha Feed, Notes + Trading link hubs |
| 📰 Content | Alpha Feed, AI Prompt, Notes |
| 🔧 Builder | AI, Notes, Embed, Links + Dev tool hubs |

---

## Getting Started

### Option 1 — Just open it
Download `index.html` and open it in your browser. That's it.

### Option 2 — Deploy to Cloudflare Pages
1. Fork this repo
2. Go to [Cloudflare Pages](https://pages.cloudflare.com)
3. Connect your GitHub repo
4. Build command: *(leave empty)*
5. Output directory: `/` (root)
6. Deploy ✅

### Option 3 — Deploy to any static host
Upload `index.html` to Netlify, Vercel, GitHub Pages — anything that serves static files.

---

## Optional: Supabase (cloud sync)

To enable cross-device sync and authentication:

1. Create a free project at [supabase.com](https://supabase.com)
2. Create a `layouts` table:

```sql
create table layouts (
  id uuid default gen_random_uuid() primary key,
  user_id uuid references auth.users not null,
  mode text,
  data jsonb,
  updated_at timestamptz default now()
);

alter table layouts enable row level security;

create policy "Users own their layouts"
  on layouts for all
  using (auth.uid() = user_id);
```

3. Open `index.html`, find the constants at the top and replace:

```js
const SUPA_URL = 'https://YOUR_PROJECT.supabase.co';
const SUPA_KEY = 'YOUR_ANON_KEY';
```

---

## Project Structure

```
index.html        ← entire app (HTML + CSS + JS, single file)
_headers          ← Cloudflare security headers
_redirects        ← Cloudflare redirect rules
wrangler.toml     ← Cloudflare Pages config
```

---

## Widgets

| Widget | Description |
|--------|-------------|
| 🕐 Clock | Live clock + date, locale-aware |
| 🌤 Weather | Temperature, feels-like, condition, humidity, wind |
| 🔗 Quick Links | Custom links with favicons |
| 📈 Market Radar | Crypto prices via CoinGecko |
| 📝 Notes | Auto-saving notepad |
| 📰 Alpha Feed | RSS/news reader |
| 🤖 AI Prompt | OpenAI & Claude API |
| 🖼 Embed | iFrame any URL |
| ✅ To-Do | Task list with completion tracking |
| ⏱ Pomodoro | Focus timer with session counter |
| 💬 Daily Quote | Inspirational quote of the day |

---

## Contributing

PRs are welcome! Some ideas if you want to help:

- New widget types (Calendar, RSS reader, Habit tracker…)
- New themes
- PWA / offline support
- Better mobile touch drag-to-reorder
- i18n additions (FR, DE, JA…)

Please open an issue first to discuss major changes.

---

## License

MIT — free to use, modify and distribute. See [LICENSE](LICENSE).

---

Made with ❤️ by [Ed](https://x.com/EdCriptoFi) · [@EdCriptoFi](https://x.com/EdCriptoFi)
