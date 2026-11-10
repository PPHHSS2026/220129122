---
name: sketch-to-3d-studio
description: Build, repair, or extend the single-file Korean sketch-and-image-to-3D studio in 220129122.html. Use for its drawing tools, image matting, Three.js modeling, materials, transforms, previews, or OBJ/glTF export; do not use for unrelated 3D or generic web projects.
---

# Sketch to 3D Studio

Work on `220129122.html` as the canonical application. It is a browser-only, single-file Korean web app; keep HTML, CSS, and JavaScript together unless the user explicitly requests a different structure.

## Preserve the product shape

- Keep both input paths: canvas sketching and image upload/drag-and-drop.
- Preserve undo, drawing tools, background fill, preview, edge-connected background removal, and matting-threshold adjustment.
- Preserve the Three.js viewer, orbit and transform controls, shape analysis, contour extrusion, SDF-style inflation, primitive fallbacks, material and lighting choices, scale/depth controls, view presets, wireframe, floor/grid, auto-rotation, and OBJ/glTF export.
- Keep processing local in the browser. Do not add a server, paid API, authentication, or upload user images to a remote service unless the user asks for it.
- Describe the current "AI" behavior accurately: it is client-side pixel, contour, and geometry analysis, not a hosted machine-learning model.

## Implementation constraints

- Preserve UTF-8 Korean text. On Windows PowerShell, read the file with an explicit UTF-8 encoding when terminal output appears garbled; do not rewrite good source text based on mojibake displayed by the shell.
- Keep compatibility with the existing global-script stack: Three.js r128, OrbitControls, TransformControls, OBJExporter, GLTFExporter, Font Awesome, and Earcut loaded from CDNs.
- Maintain the Earcut override used by `THREE.ShapeUtils.triangulateShape`; contour extrusion depends on it.
- Keep canvas analysis at the app's expected 512x512 working resolution unless all dependent coordinate transforms, thresholds, UV calculations, and previews are updated together.
- When changing model generation, verify indexed geometry, normals, UVs, front/back faces, and side walls. Avoid silently falling back to a box when valid contour data exists.
- Dispose replaced Three.js geometries, materials, and textures when adding repeated regeneration paths to avoid GPU memory leaks.
- Preserve responsive renderer sizing and do not create a second animation loop.

## Workflow

1. Inspect the relevant markup, styles, event bindings, and geometry function before editing; IDs are shared across all three layers.
2. Make the smallest coherent change in `220129122.html` and keep labels and behavior in sync.
3. Check JavaScript syntax and load the page in a browser when available.
4. Exercise both input modes and the affected 3D controls. For geometry changes, test a simple filled shape, an irregular uploaded silhouette, and repeated regeneration.
5. Confirm OBJ and glTF export still completes when export-related code or mesh construction changes.

Do not include unrelated untracked files in commits for this app. Stage `220129122.html` and this skill only when the user asks to commit or push the skill.
