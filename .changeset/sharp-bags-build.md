---
'@astrojs/cloudflare': patch
---

Fixes prerender errors being silently swallowed when pages throw during rendering in workerd, causing `astro build` to exit 0 and emit truncated HTML. The adapter now enables the Cloudflare Vite plugin's `experimental.bufferPreviewResponses` option, which buffers the response body inside workerd so streaming errors are caught and surfaced to the build process (via a marker header) as build failures with clear error messages, rather than a truncated 200. Requires `@cloudflare/vite-plugin` 1.41.0 or later.
