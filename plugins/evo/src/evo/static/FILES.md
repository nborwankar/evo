# plugins/evo/src/evo/static/

Dashboard front-end assets, served by `evo.dashboard`. CI verifies all three
files are present in the built wheel — see `.github/workflows/ci.yml`.

| File | Purpose |
|------|---------|
| `index.html` | Dashboard SPA shell. |
| `app.js` | Dashboard JS — polls graph + config endpoints, renders the experiment tree and frontier-strategy picker. |
| `style.css` | Dashboard styles. |
