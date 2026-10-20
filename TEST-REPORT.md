# Test report — Rose Shape Fix

## Passed

- `node scripts/smoke-check.mjs`
- JavaScript syntax check on all source modules
- Relative module imports resolve
- UI IDs and CSS import are present
- Layered bloom animation is present
- Instanced flower meadow, leaf geometry, landscape layers and 4K query profile are present
- ZIP integrity check after packaging

## Not verified

- `npm run build`: not run successfully here; dependencies are not installed and npm registry requests have timed out in this environment.
- Actual render quality/FPS on desktop or mobile hardware: requires browser and GPU testing.
- 4K is a WebGL drawing-buffer mode, not an MP4 export.

## Local test

```powershell
npm install
npm run check
npm run build
npm run dev
```

To try the high-resolution canvas mode, open the Vite URL with `?quality=4k` appended.
