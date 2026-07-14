[![changelog][changelog-src]][changelog-href]
[![License][license-src]][license-href]

<p align="center">
  <a href="https://parolla.app" target="_blank">
    <img src="/static/meta/logo.png" width="96" alt="parolla logo" />
  </a>
</p>

<h1 align="center">parolla</h1>

<p align="center">
  <strong>A Turkish word game platform with daily quizzes, multiplayer modes, and player-created content.</strong>
</p>

<p align="center">
  Solve daily questions, compete on leaderboards, create your own quizzes, and explore multiple game modes — all in Turkish and English.
</p>

<p align="center">
  <a href="https://parolla.app"><strong>Website</strong></a>
  ·
  <a href="https://parolla.app/en"><strong>English</strong></a>
  ·
  <a href="https://github.com/quantpiloter/parolla"><strong>Repository</strong></a>
</p>

<p align="center">
  <a href="https://github.com/quantpiloter/parolla" target="_blank">
    <img alt="GitHub stars" src="https://img.shields.io/github/stars/quantpiloter/parolla?style=social">
  </a>
</p>

<br>

<table align="center">
  <tr>
    <td align="center" width="50%">
      <sub>Turkish</sub><br>
      <a href="https://parolla.app" target="_blank">
        <img src="/static/meta/preview-tr.png" width="256" alt="parolla Turkish preview" />
      </a>
    </td>
    <td align="center" width="50%">
      <sub>English</sub><br>
      <a href="https://parolla.app/en" target="_blank">
        <img src="/static/meta/preview-en.png" width="256" alt="parolla English preview" />
      </a>
    </td>
  </tr>
</table>

## Overview

**parolla** is a static single-page web app built with Nuxt 2 and Vue 2. It ships as a production-ready game platform with localized routes, real-time multiplayer features, and a modular architecture for multiple game modes.

Live at [parolla.app](https://parolla.app). Source code is maintained at [github.com/quantpiloter/parolla](https://github.com/quantpiloter/parolla).

### Game modes

| Mode | Turkish route | English route | Description |
| --- | --- | --- | --- |
| Daily | `/gunluk` | `/daily` | Daily quiz with leaderboard competition |
| Unlimited | `/limitsiz` | `/unlimited` | Endless quiz sessions |
| Creator | `/yaratici` | `/creator` | Create, edit, and play community quizzes |
| Tour | `/tur` | `/tour` | Tournament-style quiz play |
| Wordblock | `/kelimeblok` | `/wordblock` | Word puzzle with configurable lengths |
| Music | `/muzik` | `/music` | Guess-the-song and music quiz modes |
| Draw | `/ciz` | `/draw` | Multiplayer draw-and-guess rooms |
| Knowledge Kingdom | `/bilgi-kralligi` | `/knowledge-kingdom` | Idle tycoon simulation |

### Draw mode

Multiplayer draw-and-guess gameplay with lobby, room codes, canvas drawing, chat/guess panel, and scoreboard.

| Route | Purpose |
| --- | --- |
| `/ciz` (`/draw`) | Lobby — browse active rooms, join by code, create a room |
| `/ciz/oda/:code` (`/draw/room/:code`) | Game screen — canvas, chat/guess window, scoreboard |

The frontend connects to the `parolla-ws` WebSocket server on the `?channel=draw` channel. Words are loaded from the `DrawWord` collection in `parolla-strapi`.

## Tech stack

| Layer | Technology |
| --- | --- |
| Framework | Nuxt 2.17.1 / Vue 2 (`target: static`, `ssr: false`) |
| Language | JavaScript with `@nuxtjs/composition-api` |
| Templates | Pug |
| Styling | SCSS + Bootstrap 5.2.3 |
| State | Vuex with `vuex-persist` |
| i18n | Turkish (default) and English (`/en` prefix) |
| Auth | Google OAuth via `@nuxtjs/auth-next` |
| Backend | Strapi API |
| Realtime | WebSocket via `isomorphic-ws` |
| Tooling | Yarn 4.6.0, Node 22.11.0 |

## Play now

| Platform | Link |
| --- | --- |
| Web (TR) | [parolla.app](https://parolla.app) |
| Web (EN) | [parolla.app/en](https://parolla.app/en) |
| Android | [Google Play](https://play.google.com/store/apps/details?id=app.parolla) |
| iOS | [App Store](https://apps.apple.com/tr/app/parolla-kelime-oyunu/id6448075358) |

<p>
  <a href="https://play.google.com/store/apps/details?id=app.parolla" target="_blank">
    <img src="/static/meta/play-store-logo.png" width="36" alt="Google Play" />
  </a>
  <a href="https://apps.apple.com/tr/app/parolla-kelime-oyunu/id6448075358" target="_blank">
    <img src="/static/meta/app-store-logo.png" width="36" alt="App Store" />
  </a>
</p>

## Getting started

### Prerequisites

- Node.js `22.11.0` (see `.nvmrc`)
- Yarn `4.6.0`

### Clone and install

```bash
git clone https://github.com/quantpiloter/parolla.git
cd parolla
yarn install
```

### Development

```bash
# Start dev server at http://localhost:3000
yarn dev
```

### Production build

parolla uses Nuxt static generation with client-side rendering only.

```bash
# Generate static site
yarn generate

# Serve production build
yarn start
```

See the [Nuxt 2 commands documentation](https://nuxtjs.org/docs/get-started/commands/) for additional deployment options.

### Linting and formatting

```bash
yarn lint:eslint
yarn lint:eslint:fix
yarn lint:stylelint
yarn lint:stylelint:fix
yarn prettier
```

Pre-commit hooks (Husky + lint-staged) run ESLint, Stylelint, and Prettier on staged files.

### Commits and releases

This project uses [Conventional Commits](https://www.conventionalcommits.org/) with Commitizen.

```bash
git add .
yarn commit   # or: yarn cz
git push
```

Changelog generation is handled by [changelogen](https://github.com/unjs/changelogen):

```bash
yarn changelog
```

## Environment variables

| Variable | Description | Default |
| --- | --- | --- |
| `API_URL` | Strapi API base URL | `https://strapi.parolla.app/api` |
| `WS_URL` | WebSocket server URL | `wss://0.0.0.0:1881` |
| `GOOGLE_AUTH_CLIENT_ID` | Google OAuth client ID | — |
| `GOOGLE_AUTH_REDIRECT_URI` | Google OAuth redirect URI | — |

## Project structure

```
components/     UI components (Pug + Composition API + scoped SCSS)
pages/          File-based routes and game mode screens
store/          Modular Vuex store (one module per feature)
composables/    Auto-imported shared logic
locales/        Turkish and English translations
transformers/   API response normalizers
system/         App constants and head/meta configuration
static/         Static assets and PWA manifest
```

For deeper architecture notes, see [CLAUDE.md](./CLAUDE.md).

## Deployment

Static output from `yarn generate` is deployed to Cloudflare and Vercel. Cloudflare redirect preparation runs automatically via `.cloudflare/scripts/redirects.js`.

## Sponsorship

Support ongoing development:

<a href="https://buymeacoffee.com/selimdoyranli">
  <img src="https://www.buymeacoffee.com/assets/img/custom_images/yellow_img.png" alt="Buy me a coffee" />
</a>

## Author

Created by [Selim Doyranlı](https://selimdoyranli.com)

## License

[CC BY-NC 4.0](./LICENSE)

Copyright (c) Selim Doyranlı &lt;selimdoyranli@gmail.com&gt;

<!-- Badges -->

[changelog-src]: https://img.shields.io/static/v1?label=%F0%9F%93%96&message=Release%20Notes%20|%20CHANGELOG&color=blue
[changelog-href]: ./CHANGELOG.md
[license-src]: https://img.shields.io/badge/License-CC%20BY%E2%80%91NC%204.0-blue.svg
[license-href]: ./LICENSE
