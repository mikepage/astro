---
'@astrojs/cloudflare': patch
'astro': patch
---

Fixes a bug where an error thrown while prerendering a page in the workerd runtime did not fail the build. Pages stream by default, so an error thrown mid-render surfaced only after the `200` status line had been sent, and the build wrote silently truncated HTML files and exited with code `0`; errors thrown before streaming started were rendered as 500 error pages and written to disk as if successful. The prerender endpoint now buffers the rendered body inside workerd, installs the build-time error handler (`BuildErrorHandler`, now exported from `astro/app` alongside a new `BaseApp#setErrorHandler()` method) so pre-stream errors propagate, and reports render errors back to the build, which fails with the original error message and stack trace.
