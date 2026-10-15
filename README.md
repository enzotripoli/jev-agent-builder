# Jev Agent Builder

A free, open-source visual builder for [TypeSafe AI](https://typesafe.ai)'s **Jev** model.

Compose Choice, Score and Noul questions in a form, add `{{parameters}}`, and get the exact JSON for `POST /v1/systemone`, live. Export as a request, a reusable agent definition, a cURL command or a TypeScript function, and open any request in the TypeSafe Playground in one click.

**Try it:** https://enzotripoli.github.io/jev-agent-builder/

> Unofficial tool, not affiliated with TypeSafe AI.

## Features

- **All three question types**, with the API limits built in: up to 255 options per Choice, 2 to 10 levels per Score, optional `true`/`false` criteria for Noul.
- **Parameters**: write `{{name}}` anywhere (state, instructions, option descriptions). Text or JSON values, with sample values for testing.
- **Options from a parameter**: a Choice can take its option list from a JSON parameter supplied at runtime.
- **`none_of_the_above` in one click**, so Jev can say that nothing fits.
- **Live validation** against the official docs: duplicate ids, undefined or unused parameters, context limits (64k tokens per request, 32k per question).
- **Four exports**: resolved request, reusable agent definition (placeholders kept), cURL, TypeScript `fetch` function.
- **Playground link** to test on the real model.
- **Seven starter examples**: support triage, content moderation, lead qualification, product reviews, document classification, intent routing, resume screening.
- **English and French** interface.
- **Private by design**: a single static HTML file. Nothing is sent anywhere; your draft is kept in your browser's local storage.

## Run it

It is one file, `index.html`. Open it in a browser, or serve it with any static host.

### Deploy on GitHub Pages

1. Fork or push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, pick **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Your fork is live at `https://YOUR-USERNAME.github.io/jev-agent-builder/` within a minute.

## Agent definition format

The **Agent (template)** tab exports a reusable definition. Placeholders stay in place, and parameters carry default values:

```json
{
  "jevAgent": 1,
  "name": "intent-router",
  "model": "jev-latest",
  "params": [
    { "key": "message", "type": "text", "default": "…" },
    { "key": "intents", "type": "json", "default": { "track_order": "…", "refund": "…" } }
  ],
  "state": "{{message}}",
  "questions": {
    "intent": {
      "type": "choice",
      "instructions": "What does the user want to do?",
      "criteria": "{{intents}}",
      "include_none_of_the_above": true
    }
  }
}
```

At runtime, replace each `{{key}}` with its value. A placeholder that fills a whole value is replaced by the parameter's JSON value as is. The TypeScript export includes a small `fill()` function that does this.

`include_none_of_the_above` is a builder field, not an API field: the export resolves it into a `none_of_the_above` option before calling the API.

## Dependencies

- [lz-string](https://github.com/pieroxy/lz-string) 1.5.0 (cdnjs) for Playground share links
- Google Fonts: Bricolage Grotesque, IBM Plex Sans, IBM Plex Mono

## Reference

- [TypeSafe docs](https://docs.typesafe.ai/introduction)
- [API reference](https://docs.typesafe.ai/api)
- [Primitives: Choice, Score, Noul](https://docs.typesafe.ai/primitives)

## Contributing

Issues and pull requests are welcome. Tell me which decisions you want to automate and what the builder is missing.

## License

[MIT](LICENSE) © 2026 Enzo Tripoli, [ET Technology Consulting](https://et-technology-consulting.com)
