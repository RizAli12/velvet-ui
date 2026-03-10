# VelvetUI — Svelte 5 Component Library

> 17 animated, accessible, production-ready components.  
> Pure CSS animations. Zero runtime dependencies. Svelte 5 runes syntax.

## Components

Button · Badge · Input · Toggle · Loader · Card · Tooltip · Progress ·
Notification · Avatar · AvatarStack · Select · Tabs · Modal · Accordion ·
Skeleton · Stat

## Quick Start

Copy any `.svelte` file from `src/lib/components/` into your project, or import from the barrel:

```js
import { Button, Badge, Modal, Loader } from "./lib/index.js";
```

## Required CSS Variables

Add these to your global CSS (e.g. `app.css`):

```css
:root {
  --bg: #080a0f;
  --bg2: #0e1117;
  --bg3: #14161c;
  --border: rgba(255, 255, 255, 0.07);
  --border-h: rgba(200, 165, 90, 0.3);
  --text: #e8e6e0;
  --muted: #6b6b74;
  --soft: #9a96a0;
  --gold: #c8a55a;
  --gold2: #e4c17a;
  --blue: #7eb5d4;
  --green: #7dc4a0;
  --red: #d47e7e;
}
```

## Developing

```sh
npm install
npm run dev
```

## License

MIT — free for personal and commercial use.
