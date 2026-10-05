<div align="center">
<img src="../enervolt-background.en.png" alt="Enervolt Nova Electricidad" width="100%" />
<div align="right">
<img width="16" height="16" src="../icons/frontend/svg/react.svg" alt="React" />
<img width="16" height="16" src="../icons/frontend/svg/typescript.svg" alt="TypeScript" />
<img width="16" height="16" src="../icons/frontend/svg/vite.svg" alt="Vite" />
<img width="16" height="16" src="../icons/backend/javascript-typescript/svg/nodejs-color.svg" alt="Node.js" />
<img width="16" height="16" src="../icons/frontend/svg/leaflet.svg" alt="Leaflet" />
<img width="16" height="16" src="../icons/frontend/svg/vercel.svg" alt="Vercel" />
<img width="16" height="16" src="../icons/frontend/svg/cloudflare.svg" alt="Cloudflare" />
<img width="16" height="16" src="../icons/devops/png/git.png" alt="Git" />
<img width="16" height="16" src="../icons/devops/png/npm.png" alt="npm" />
</div>
</div>

<br>

<br>

<div align="right">
  <a href="../../README.md" title="Español">
    <img src="./arg-flag.jpg" width="64" height="40" alt="Español" title="Español" />
  </a>
  <a href="./README.en.md" title="English">
    <img src="./eeuu-flag.jpg" width="64" height="40" alt="English" title="English" />
  </a>
</div>

<div align="center">

# Enervolt Nova Electricidad ![(status-active)](../icons/badges/status-active.svg)

</div>

Enervolt Nova Electricidad is the application of an electrical service for homes, offices, shops, and apartment buildings in Buenos Aires City and nearby areas, open 24 hours. Visitors find concrete services, real jobs with a photo and a neighborhood, and a map to browse the work by area. When someone arrives with a question, Enervolti —the application's AI chat— answers it right away: services, coverage, hours, visits, and how to request a quote. When they are ready to move ahead, they add a location, describe the problem, and can attach photos or a short video. The request is ready to continue on WhatsApp or email.

<div align="left">
<a href="https://enervoltnova.com/electricidad/" target="_blank" rel="noopener noreferrer" title="View live"><img src="../icons/detail-actions/ver-live-pill.svg" alt="Ver live" width="96" height="32" border="0" /></a>
</div>

<br>

## Index 📜

<details>
  <summary> View details </summary>

<br>

<div align="right">

`Last update: 05/10/26`

</div>

### Section 1) Description, setup, and technologies

* [1.0) Description.](#10-description-)
* [1.1) Running it.](#11-running-it-)
* [1.2) Structure.](#12-structure-)
* [1.3) Technologies.](#13-technologies-)

### Section 2) The application and the journey

* [2.0) Pages.](#20-pages-)
* [2.1) Services.](#21-services-)
* [2.2) Jobs and map.](#22-jobs-and-map-)
* [2.3) Quote and contact.](#23-quote-and-contact-)
* [2.4) Orders and retention.](#24-orders-and-retention-)

### Section 3) Publishing, tests, and references

* [3.0) Tests.](#30-tests-)
* [3.1) Published application (Vercel).](#31-published-application-vercel-)
* [3.2) Contributing.](#32-contributing-)
* [3.3) References.](#33-references-)

</details>

<br>

## Section 1) Description, setup, and technologies

### 1.0) Description [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

**Enervolt Nova Electricidad** is a React, Vite, and TypeScript application. Vercel functions store quote requests, and a Cloudflare Worker publishes it at [https://enervoltnova.com/electricidad/](https://enervoltnova.com/electricidad/).

Why it exists:

* Show the trade through services, photos, and the area of each job, without asking for an account.
* Answer in chat with Enervolti before the form is filled in.
* Receive an inquiry with a neighborhood or locality from the catalog, a description, and, when useful, photos or a short video.
* Store the request and open WhatsApp or email with the message already prepared.

What the application delivers:

* **Home**, with services, featured jobs, and the path to request a quote.
* **Nine services:** circuit breakers and RCDs, panels, outlets, lighting, wiring, new installations, fault finding, doorbells, and shop electrical work.
* **Job catalog** with photo, area, and detail, plus a map to explore them by neighborhood.
* **Enervolti**, the application chat. It guides people through services, areas, hours, visits, and quotes, and opens the matching page. Answers come from the published information; it does not invent prices or diagnoses.
* **Quote form** with a location from the catalog (48 Buenos Aires City neighborhoods and Buenos Aires Province localities), validation shared by the web app and the server, and delivery through WhatsApp or email.
* **Search** across services and jobs, plus a light or dark appearance.
* **How we work** and **Contact**, with service 24 hours a day, including weekends.
* **Static legal pages:** privacy and terms, readable without JavaScript.
* **Production HTML** with a title, description, and structured data per page, plus `sitemap.xml`.

Public contact details (WhatsApp, phone, and email) are defined in the application's `shared/contacto.js`. They do not depend on environment variables.

</details>

### 1.1) Running it [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

* Install, prepare the local environment, and start:

```bash
npm install
cp .env.example .env.local
npm run dev
```

The application listens on the port Vite prints. **`.env.local` is the only local configuration file.** It is excluded from Git. `.env.example` is the versioned template, without credentials. Phones and email are changed in `shared/contacto.js`, not in the environment.

CI uses **Node.js 22**.

#### Useful scripts

| Script | Description |
| --- | --- |
| `npm run dev` | Vite development server |
| `npm run build` | TypeScript, Vite build, SEO, and the Cloudflare Worker |
| `npm run preview` | Serves the static build (without the order functions) |
| `npm test` | Native tests (`node --test`) |
| `npm run lint` | oxlint |
| `npm run cloudflare:build` | Regenerates the Worker with the domain 404 |
| `npm run storage:check` | Real write and read check against the configured storage |
| `npm run drive:connect` | Connects, locally, the Google Drive owner account |

Do not commit `.env.local`. Drive, Vercel, and the cleanup cron use the variables in that file and in the Vercel project.

</details>

### 1.2) Structure [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

```text
enervolt-nova-electricidad/
├── api/                                 # Order, attachments, lookup, status, and cleanup
├── cloudflare/
│   └── electricidad-router.js           # /electricidad prefix and root 404
├── public/                              # Brand, privacy, and terms
├── server/                              # Google Drive, storage, and cleanup
├── shared/                              # Contact, areas, retention, and validation
├── src/
│   ├── components/
│   ├── data/                            # Services, jobs, SEO, and copy
│   ├── modules/asistente/               # Enervolti
│   ├── pages/                           # Home, services, jobs, map, quote
│   └── App.tsx                          # React Router routes
├── tests/
├── vercel.json                          # Rewrites, redirects, and cron
└── package.json
```

</details>

### 1.3) Technologies [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

| **Technology** | **Version** | **Purpose** |
| --- | --- | --- |
| [React](https://react.dev/) | **19.2** | **Interface** |
| [React Router](https://reactrouter.com/) | **7.18** | **Application routes** |
| [TypeScript](https://www.typescriptlang.org/) | **6.0** | **Application types** |
| [Vite](https://vite.dev/) | **8.3** | **Development and build** |
| [Node.js](https://nodejs.org/) | **22** | **Tests, scripts, and functions** |
| [Leaflet](https://leafletjs.com/) | **1.9** | **Jobs map** |
| [Vercel](https://vercel.com/) | **Hosting** | **Site, functions, and cron** |
| [Cloudflare Workers](https://developers.cloudflare.com/workers/) | **Worker** | **Public domain `/electricidad`** |
| [Google Drive API](https://developers.google.com/workspace/drive/api/guides/about-sdk) | **drive.file** | **Orders and attachments** |
| [oxlint](https://oxc.rs/docs/guide/usage/linter.html) | **1.81** | **Lint** |
| npm | **cli** | **Dependencies** |
| Git | **cli** | **Versions** |

**Official docs:**

* React: https://react.dev/
* Vite: https://vite.dev/
* Leaflet: https://leafletjs.com/
* Vercel: https://vercel.com/docs
* Cloudflare Workers: https://developers.cloudflare.com/workers/

</details>

<br>

## Section 2) The application and the journey

### 2.0) Pages [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

Locally, routes start at the root. On the public domain they use the `/electricidad` prefix. The Worker removes it before calling the Vercel origin.

| Page | Local | Public |
| --- | --- | --- |
| Home | `/` | https://enervoltnova.com/electricidad/ |
| Services | `/servicios` | https://enervoltnova.com/electricidad/servicios |
| Service detail | `/servicios/:id` | https://enervoltnova.com/electricidad/servicios/:id |
| Jobs | `/trabajos` | https://enervoltnova.com/electricidad/trabajos |
| Map | `/trabajos/mapa` | https://enervoltnova.com/electricidad/trabajos/mapa |
| Job detail | `/trabajos/:slug` | https://enervoltnova.com/electricidad/trabajos/:slug |
| Quote | `/presupuesto` | https://enervoltnova.com/electricidad/presupuesto |
| How we work | `/como-trabajamos` | https://enervoltnova.com/electricidad/como-trabajamos |
| Contact | `/contacto` | https://enervoltnova.com/electricidad/contacto |
| Search | `/buscar` | search inside the application |

`/proceso` redirects to `/como-trabajamos`. `/home` returns to the home page. An unknown route inside Electricidad shows the application's own not-found page. Outside `/electricidad`, on `enervoltnova.com`, the Worker returns 404 without calling the origin.

</details>

### 2.1) Services [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

The catalog lives in `src/data/servicios.ts`. Each entry has a summary, what it includes, and example jobs.

| Id | Service |
| --- | --- |
| `termicas` | Circuit breakers and RCDs |
| `tableros` | Electrical panels |
| `tomas` | Outlets and switches |
| `luminarias` | Lighting and fixtures |
| `cableado` | Wiring and conduit |
| `nuevas` | New installations |
| `fallas` | Fault finding |
| `porteros` | Doorbells and entry phones |
| `locales` | Shop electrical work |

Visible coverage is Buenos Aires City and nearby areas. Neighborhoods in the job catalog show published work; they do not mark the edge of the service area.

</details>

### 2.2) Jobs and map [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

`src/data/trabajos.ts` describes each job: type, area, summary, and photos. The gallery filters by type and neighborhood, and those filters stay in the URL.

The map uses **Leaflet** on **OpenStreetMap**. When zoomed out, nearby areas cluster and add up their jobs; activating a cluster zooms in. Map references are approximate: they are not customer addresses.

The build generates its own HTML for the gallery, the map, each service, and each job, with the photo already included, so a direct link has a title and content before JavaScript runs.

</details>

### 2.3) Quote and contact [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

The form asks for a name, a location, and a description of the work. Phone and email are optional. Photos and a short video are optional too. The location is chosen from a local catalog: 48 Buenos Aires City neighborhoods and the localities of Buenos Aires Province. The same contract (`shared/validacion-pedido.js` and `shared/zonas-pedido.js`) runs in the browser and on the server.

Choosing an area shows a reference map. That map does not take part in validation or submission: if the provider does not respond, the inquiry can still be completed.

Two ways out, after the request is stored:

* **WhatsApp** opens the chat with the message prepared.
* **Email** opens the client with `mailto:`.

The page does not send the message itself. The person confirms it in WhatsApp or in their mail app.

Public contact:

| Detail | Use |
| --- | --- |
| WhatsApp `5491125151958` | Quote recipient |
| Phone `1131096122` | Number to call |
| `enervoltnova.electricidad@gmail.com` | Quotes and questions |
| Av. Lacarra 296, CABA | Reference address |
| Open 24 hours | Every day |

`/contacto` presents those channels. The form lives at `/presupuesto`.

</details>

### 2.4) Orders and retention [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

`POST /api/pedido-archivo` uploads each file and `POST /api/pedido` stores the request. **Google Drive is the remote storage.** The application stays usable if those functions fail; the form keeps what was entered and offers a retry or a text-only send.

Originals and the order JSON expire **fifteen days** after upload. The public link (`/p/<solicitud>`) shows the deadline. An expired lookup can return `410` while the file still exists, and `404` after the sweep. The daily cron is declared in `vercel.json` (`GET /api/limpieza-pedidos`, 09:00 UTC).

The link preview uses the title **Pedido de presupuesto · Enervolt Nova Electricidad** and the fixed description `enervoltnova.com/electricidad`. The customer's problem is not part of that preview.

Legal pages:

* Privacy: https://enervoltnova.com/electricidad/privacidad.html
* Terms: https://enervoltnova.com/electricidad/condiciones.html

</details>

<br>

## Section 3) Publishing, tests, and references

### 3.0) Tests [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

#### 3.0.1) Published walkthrough

Screenshots of [enervoltnova.com/electricidad](https://enervoltnova.com/electricidad/). The header of this README is the desktop home. The rest of the walkthrough is here: navigation, how we work, jobs, the map, Enervolti, and the quote form.

<div align="center">

| Navigation | How we work |
| --- | --- |
| <img src="../pruebas/02-navegacion.png" alt="Application menu" width="260" /> | <img src="../pruebas/03-como-trabajamos.png" alt="How we work" width="260" /> |

| Jobs | Filters |
| --- | --- |
| <img src="../pruebas/07-trabajos.png" alt="Job gallery" width="260" /> | <img src="../pruebas/08-trabajos-filtros.png" alt="Area and type filters" width="260" /> |

| Map | Enervolti |
| --- | --- |
| <img src="../pruebas/04-mapa.png" alt="Jobs map on a phone" width="260" /> | <img src="../pruebas/06-enervolti.png" alt="Enervolti assistant" width="260" /> |

<img src="../pruebas/05-mapa-escritorio.jpg" alt="Jobs map on desktop" width="720" />
<br>
<sub>Jobs map</sub>

<br>

| Quote | Send |
| --- | --- |
| <img src="../pruebas/09-presupuesto.png" alt="Quote form" width="260" /> | <img src="../pruebas/10-presupuesto-envio.png" alt="Send by WhatsApp or email" width="260" /> |

</div>

#### 3.0.2) Automated tests

```bash
npm test
npm run lint
npm run build
```

`npm test` runs `node --test` over `tests/*.test.mjs`. No extra server is required. A few of those tests:

| File | What it covers |
| --- | --- |
| `navegacion.test.mjs` | Routes, aliases, and pages |
| `mapa-trabajos.test.mjs` | Map and area grouping |
| `asistente-sitio.test.mjs` | Enervolti |
| `validacion-pedido.test.mjs` | Quote form |
| `cloudflare-router.test.mjs` | `/electricidad` prefix and the 404 |

`npm run storage:check` is the check that does contact Google Drive; it does not replace the simulated tests. GitHub Actions runs the suite on every push and on pull requests to `master`.

</details>

### 3.1) Published application (Vercel) [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

Published application: **[https://enervoltnova.com/electricidad/](https://enervoltnova.com/electricidad/)**

| Piece | Role |
| --- | --- |
| Vercel | Build (`npm run build`), `/api` functions, and the cleanup cron |
| `electricidad.enervoltnova.com` | Worker origin. It is not removed or redirected from the domains panel |
| Cloudflare Worker | Publishes the application at `enervoltnova.com/electricidad/` and returns 404 outside that prefix |

The Worker is `cloudflare/electricidad-router.js`. It strips `/electricidad` before calling Vercel and adds the mark `x-enervolt-proxy: electricidad`. `vercel.json` 308-redirects direct visits to the subdomain that do not carry that mark, so they end on the public domain.

When the 404 or the routing changes, publish in this order: the Worker first (`npm run cloudflare:build` and a Cloudflare deploy), then the Vercel project. A Vercel build alone does not update the code pasted into the Worker.

</details>

### 3.2) Contributing [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

1. Fork the repository.
2. Create a branch (`git checkout -b feature/my-change`).
3. Commit (`git commit -m 'feat: short description'`).
4. Push (`git push origin feature/my-change`).
5. Open a pull request.

Do not commit `.env.local` or credentials. If a variable changes, document it in `.env.example` and in both READMEs: this one and the [Spanish README](../../README.md).

</details>

### 3.3) References [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

Developed by Andrés Weitzel.

**Links:**

* **Published application:** [enervoltnova.com/electricidad](https://enervoltnova.com/electricidad/)
* **Spanish README:** [README.md](../../README.md)
* **Business profile:** [Enervolt Nova Electricidad on Google](https://www.google.com/maps/place/Enervolt+Nova+Electricidad/data=!4m2!3m1!1s0x0:0xcb27b0a80c78e048)

</details>
