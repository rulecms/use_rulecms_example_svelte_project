# RuleCMS Widget Integration - Svelte Demo

A demonstration of how to integrate **RuleCMS widgets** into a Svelte application using `@rulecms/widget-svelte` and `@rulecms/source-components-svelte`.

## Live Demo

**[View the live demo](https://userulecmsexamplesvelteproject.vercel.app)**

Experience the RuleCMS Svelte widget integration without running the app locally.

## What is RuleCMS?

**RuleCMS** is a visual content management system that lets you:

- Build widgets visually using a drag-and-drop composer
- Create responsive content that works across devices
- Publish instantly and get a unique published key for each widget
- Embed those widgets in any Svelte app with a few lines of code

## How widget integration works

1. **Design** — Log into [rulecms.com](https://rulecms.com) and compose a widget.
2. **Publish** — RuleCMS generates a **published key** (`{environmentId}---widget-…`).
3. **Authenticate** — Create an **app token** in project settings so your app can fetch published widgets.
4. **Integrate** — Install the Svelte packages, wrap the app with `RuleCMSWidgetProvider`, and render `RuleCMSWidget`.

`@rulecms/widget-svelte` fetches and lays out the widget. It does not ship UI cards. You register `@rulecms/source-components-svelte` as the default component library so text, images, buttons, and the rest of the default set can render.

## Quick start

```bash
git clone <repository-url>
cd use_rulecms_example_svelte_project
npm install
npm start
```

The app is at [http://localhost:5173](http://localhost:5173). Demo credentials in `src/rulecms-config.ts` are enough to render the widget without extra setup. Or skip local setup and use the [live demo](https://userulecmsexamplesvelteproject.vercel.app).

## Adding RuleCMS widgets to your own Svelte app

### Step 1: Install the packages

```bash
npm install @rulecms/widget-svelte @rulecms/source-components-svelte
```

Peer dependency: `svelte` >= 5.0.

### Step 2: Register the library and render a widget

```svelte
<script>
  import { RuleCMSWidget, RuleCMSWidgetProvider } from '@rulecms/widget-svelte';
  import * as sourceComponents from '@rulecms/source-components-svelte';

  const token = 'your-app-token';
  const publishedKey = 'your-published-key';
  const libraries = { default: sourceComponents };
</script>

<RuleCMSWidgetProvider {token} {libraries}>
  <RuleCMSWidget {publishedKey} />
</RuleCMSWidgetProvider>
```

### Step 3: Get your credentials

**App token**

1. Log into [rulecms.com](https://rulecms.com)
2. Open project settings → API / app tokens
3. Generate a token with widget access

**Published key**

1. Create or edit a widget in the composer
2. Click Publish
3. Copy the generated published key

### Step 4: Run the app

```bash
npm start
```

## This demo's credentials

Demo values live in `src/rulecms-config.ts` (same widget and token as the React, Angular, and Vue examples):

- `DEMO_RULECMS_TOKEN` — app token used to fetch the widget
- `DEMO_PUBLISHED_KEY` — published key for the demo widget

Replace those constants with your own token and published key when you wire this up to your project.

## Understanding the packages

### `@rulecms/widget-svelte`

| Piece | Role |
|---|---|
| `RuleCMSWidgetProvider` | Supplies token, optional endpoint, and library registrations to widgets below it |
| `RuleCMSWidget` | Fetches a published widget and renders its layout tree |

**Provider props**

- `token` (required): app token from RuleCMS project settings
- `endpoint` (optional): API origin override. Leave unset so published tokens hit widget-cache and `dev.` tokens hit rulecms.com
- `libraries` (required for default cards): `{ default: sourceComponents }`

**Widget props**

- `publishedKey` (required): `{environmentId}---widget-…` for staging/production
- `token` / `endpoint` / `libraries`: optional overrides if you are not using the provider
- `mode`: `'client-fetch'` (default) or `'pre-fetched'`
- `componentProps`: extra host props for a component instance, keyed by column id (`r-button` reads `onClick`)

### `@rulecms/source-components-svelte`

The default card library: `r-text`, `cloudinary-advanced-image`, `r-video`, `r-icon`, `r-button`, `r-divider`, `r-embed`, `r-list`, `r-accordion`. Register it on the provider. The widget package never imports this library itself.

## Multiple widgets

```svelte
<RuleCMSWidgetProvider {token} {libraries}>
  <header>
    <RuleCMSWidget publishedKey={headerKey} />
  </header>
  <main>
    <RuleCMSWidget publishedKey={mainKey} />
  </main>
</RuleCMSWidgetProvider>
```

## Pre-fetched rendering

Fetch on the server (or at build time), then render without a client refetch:

```ts
import { fetchRuleCMSWidget } from '@rulecms/widget-svelte';

const data = await fetchRuleCMSWidget({
  publishedKey: 'your-published-key',
  token: 'your-app-token',
});
```

```svelte
<RuleCMSWidget
  mode="pre-fetched"
  {publishedKey}
  initialData={data}
  {libraries}
/>
```

This demo uses **client-fetch** so `npm start` is enough.

## Host `componentProps`

Pass a click handler (or any extra prop) to one component instance by column id:

```svelte
<RuleCMSWidget
  {publishedKey}
  {componentProps}
/>
```

```ts
const componentProps = {
  'b721c4e2-…': { onClick: (event: Event) => console.log('cta', event) },
};
```

## Troubleshooting

**Widget not displaying**

- Confirm the published key and token in `src/rulecms-config.ts`
- Confirm `RuleCMSWidgetProvider` wraps `RuleCMSWidget`
- Confirm `{ default: sourceComponents }` is registered
- Check the browser console

**Missing cards / blank layout**

- `@rulecms/widget-svelte` will not render default cards unless `@rulecms/source-components-svelte` is registered

## Scripts

| Command | What it does |
|---|---|
| `npm start` | Dev server at http://localhost:5173 |
| `npm run build` | Production build in `dist/` |
| `npm run preview` | Preview the production build |

## Project structure

```
use_rulecms_example_svelte_project/
├── src/
│   ├── App.svelte           # Provider + widget
│   ├── main.ts
│   ├── rulecms-config.ts    # Demo token and published key
│   └── style.css
├── package.json
├── vercel.json
└── README.md
```

## Learn more

- RuleCMS: [rulecms.com](https://rulecms.com)
- [`@rulecms/widget-svelte`](https://www.npmjs.com/package/@rulecms/widget-svelte)
- [`@rulecms/source-components-svelte`](https://www.npmjs.com/package/@rulecms/source-components-svelte)
- Svelte: [svelte.dev](https://svelte.dev)

## License

MIT
