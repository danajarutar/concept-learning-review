# Zendo: English and Slovene review copies

This private repository contains two child-facing review copies. Neither sends checkpoints or stores participant data on a server. Review progress remains in the reviewer's browser. Do not use these static pages for participant data collection.

- **English:** `index.html` and its existing assets, unchanged.
- **Slovene:** `slovene.html` and the `slovene-*.js` / `slovene-*.css` files, added 3 September 2026. It uses the same images already present in the repository. It is based on the latest Slovene game's content and materials, with review-only storage instead of server saving.
- **Published source:** `slovene-published-source-2026-09-03.zip` contains the complete game application source from published commit `5a7b9df4d98ec3bc83503da5cd513787ce82069e`, including the approved quiz-correction saving fix, server checkpoint/export code, schema, migrations, assets, dependency lockfile and tests. The application has shared Slovene/English components; its Slovene child entry is `app/otroci/page.tsx`. Unrelated modelling/manuscript directories, credentials, database contents, participant logs, dependencies and generated builds are excluded.

Source archive SHA-256: `3a3148c05d208ef5a5577f6f2f32ae0a035022f2f691ebdf58fb183351784c2d`. All 60 archived files were compared byte-for-byte with their Git blobs in the published commit. Test fixtures in the source are artificial examples, not participant records.

## Review locally

Download this repository using **Code → Download ZIP**, extract it, then start a static HTTP server in the extracted folder, for example:

```sh
python -m http.server 8000 --directory ..
```

Rename the extracted folder to `concept-learning-review` first. Open `http://localhost:8000/concept-learning-review/index.html` for English or `http://localhost:8000/concept-learning-review/slovene.html` for Slovene. Use a local server rather than double-clicking the HTML files.

GitHub's file view displays source, not a running game. This update does not enable GitHub Pages, make the repository public, or change collaborator permissions.

## Inspect the published logging code

Extract the separate published-source ZIP. The key files are:

- `app/components/ZendoStudy.tsx`: response collection, construction action history, probe-selection history and checkpoint requests.
- `app/lib/checkpoint-contract.ts`: validation, including the reviewed-incorrect-quiz saving fix.
- `app/api/checkpoint/route.ts`: durable checkpoint/session writes.
- `app/api/export/route.ts`: cumulative session export, including incomplete sessions.
- `app/lib/experiment.ts`: record definitions, rules and fixed materials.

The source archive preserves `.openai/hosting.json` for provenance. It refers to the existing production study. Do not deploy it or connect a review copy to that study's database. It contains no actual export key, database records or participant data. The live Slovene study and its frozen pre-audit backup were not changed by this GitHub addition.
