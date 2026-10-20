# Visual update — Rose Shape Fix

This revision responds to the latest screenshot. The hero rose appeared like a flat plate because its petal plane faced mostly upward, the outer petals were too long/wide, and the center was hidden behind overlapping roots.

## Changes made

- `src/flowers/RoseCluster.js`
  - Tilted the rose head toward the viewer (hero bloom tilt about 0.72 radians; supporting roses about 0.48) instead of leaving the blossom nearly horizontal.
  - Reduced the hero's outer petal dimensions while increasing geometry subdivisions and edge curl, to preserve a round bloom silhouette without a pancake-like profile.
  - Changed the open offsets so outer petals gently droop, middle petals cup forward, and inner petals curl toward the center.
  - Raised and enlarged the flower center and pollen details so the rose eye remains visible after opening.
  - Added an eighth petal to the innermost ring for a fuller center.
- `src/flowers/FlowerGarden.js`
  - Slightly reduced the hero and supporting flower scales, bringing the focal bloom back into proportion with the garden.
  - Reduced background flower head scales and distinguished the size of the three petal rings, so distant flowers read as small blooms instead of chunky pink clumps.

## Validation

`node scripts/smoke-check.mjs` passes, including JavaScript syntax checks and local import resolution.

A browser/WebGL screenshot and `npm run build` have not been verified in this environment because dependencies are not installed and prior npm registry access timed out. Run the project locally to confirm the visual result on the target GPU.
