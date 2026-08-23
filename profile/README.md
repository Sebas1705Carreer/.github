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

| Repo | What it is |
|---|---|
| [career-api-worker](https://github.com/Sebas1705Carreer/career-api-worker) | The API — Cloudflare Workers + KV, TypeScript, OpenAPI 3.0, i18n data model (`LocalizedString` maps + `/languages`) |
| [carreerV2](https://github.com/Sebas1705Carreer/carreerV2) | **Active portfolio** — React 19, Vite, Tailwind v4, in-browser PDF CV generator, offline fallback snapshot |
| [career-editor-kmp](https://github.com/Sebas1705Carreer/career-editor-kmp) | **Folio** — Kotlin Multiplatform editor (Android + Desktop): Compose, Ktor, encrypted token storage |
| [carreerV1](https://github.com/Sebas1705Carreer/carreerV1) | Legacy portfolio — Astro SSG, Clean Architecture, 10 languages. Kept for reference, still deployed |
| [wiki](https://github.com/Sebas1705Carreer/wiki) | State of the art, audits and the operations runbook (secrets live in Doppler) |

Maintained by [Sebas1705](https://github.com/Sebas1705) — Full Stack & Mobile Developer, Madrid.
