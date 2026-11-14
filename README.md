# myhealth-card

Static page for the MyHealth QR codes. It stores nothing.

| QR | Link | What the page shows |
|---|---|---|
| Emergency (normal) | `index.html#<base64url JSON>` | The life-saving facts for a first responder: blood group, allergies, key medicines, conditions, devices, last admission, vitals and one-tap call buttons. The details ride after the `#`, which browsers never send to a server. |
| Doctor (secure) | `index.html#t=<token>&a=<api>` | A code box. The doctor types the 8-character code shown on the patient's phone; the page fetches the one-time summary (3 minutes, opens once) and shows the full clinical card with results, medicines, scans and stays. |

Preview the designs without a QR:

- `index.html#demo` emergency card
- `index.html#demo-doctor` doctor summary
- `index.html#demo-gate` code entry
- add `&theme=light` or `&theme=dark` to force a theme

The doctor page only talks to the MyHealth servers listed in `ALLOWED_API` inside `index.html`
(`https://teamjas.in/api/myhealth`, plus `https://localhost:44392/api/myhealth` for development),
and the website must list this site's origin under `MyHealth:WebOrigins` so the browser may call it.

The page is now served by teamjas.in itself, from `TeamJASWeb/wwwroot/myhealth-card.html` (a copy of this `index.html`),
at https://teamjas.in/myhealth-card.html. It is the same site as the API, so the browser needs no cross-site permission.
The app opens it from `appConfig.cardPage` in `src/config/app.ts`. When this file changes, copy it over the wwwroot file
and publish TeamJASWeb.

The GitHub Pages copy (repository `myhealth-card`, branch `main`) stays only so QR codes made earlier keep opening until they expire.
