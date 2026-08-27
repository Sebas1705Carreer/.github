**A portfolio built as a product**: one live API is the single source of truth for all career data, a public site consumes it in real time, and a native editor keeps it up to date.

🌐 **[Live portfolio](https://sebas1705carreer.github.io/carreerV2/)** · 🔌 **[Career API + Swagger](https://api.sebas1705.dev/docs)** · 📚 **[Docs & state of the art](https://github.com/Sebas1705Carreer/wiki)**

```
Folio (KMP editor, Android/Desktop)      carreerV2 (React, live site)
        │  writes [Bearer]                      │  reads (runtime)
        ▼                                       ▼
            career-api  ·  Cloudflare Workers + KV
                                                ▲
                                                │  reads (build time)
                                         carreerV1 (Astro, legacy)
```

## What the API serves

Every consumer reads the same eight entities, so nothing about a job or a project is written twice:

| | | | |
|---|---|---|---|
| **20** projects | **3** jobs | **137** skills | **10** certifications |
| **3** education | **12** soft skills | **1** personal profile | **2** languages |

Reads are public; writes need a Bearer token. Every localizable field is a `LocalizedString` — a `{ lang: value }` map — and `GET /languages` is what drives each consumer's language switcher, so adding a locale is extending the maps rather than touching four codebases. Currently **English** (default) and **Spanish**.

OpenAPI 3.0 lives at [`/openapi.json`](https://api.sebas1705.dev/openapi.json), Swagger UI at [`/docs`](https://api.sebas1705.dev/docs).

## The repositories

| Repo | What it is | Branch | CI |
|---|---|---|---|
| [career-api-worker](https://github.com/Sebas1705Carreer/career-api-worker) | The API — Cloudflare Workers + KV, TypeScript, OpenAPI 3.0. Single source of truth for everything below | `development` | Deploys to Cloudflare on push |
| [carreerV2](https://github.com/Sebas1705Carreer/carreerV2) | **Active portfolio** — React 19, Vite, Tailwind v4, i18next. Reads the API at runtime with an offline fallback, and generates a PDF CV in the browser: 4 role profiles × 2 variants, one for people and one for ATS parsers | `main` | Lint → build → Pages |
| [career-editor-kmp](https://github.com/Sebas1705Carreer/career-editor-kmp) | **Folio** — Kotlin Multiplatform editor for Android and Desktop: Compose, Ktor, encrypted token storage. The only thing that writes to the API | `development` | — |
| [carreerV1](https://github.com/Sebas1705Carreer/carreerV1) | Legacy portfolio — Astro 4, Clean Architecture, 10 languages, Playwright end-to-end. Reads the API at build time. Kept for reference, still deployed | `main` | Vitest → build → E2E → Pages |
| [wiki](https://github.com/Sebas1705Carreer/wiki) | State of the art, audits and the operations runbook | `main` | — |
| [.github](https://github.com/Sebas1705Carreer/.github) | This profile | `main` | — |

## Working on it

- **Branches split by kind.** The API and the editor develop on `development`; the two sites deploy from `main`, so a merge there is a release.
- **Data is edited, not committed.** Use Folio or a `PATCH` against the API — see the [API README](https://github.com/Sebas1705Carreer/career-api-worker#readme). Re-seeding overwrites live data and is rarely what you want.
- **Secrets live in Doppler**, never in the repositories. `.env` and `.dev.vars` are ignored; the inventory and rotation runbook are in the [wiki](https://github.com/Sebas1705Carreer/wiki).

The [state of the art](https://github.com/Sebas1705Carreer/wiki/blob/main/state-of-the-art.md) is the one page kept current — what exists, where it runs, and what is still open.

---

Maintained by [Sebas1705](https://github.com/Sebas1705) — Full Stack & Mobile Developer, Madrid.
