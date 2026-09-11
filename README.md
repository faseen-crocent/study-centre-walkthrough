# Study Centre Walkthrough

Interactive 3D walkthrough of a single-storey study centre in the
Kerala vernacular, generated procedurally from its ground floor plan.

## Files

- `index.html` – the whole site: layout data, 3D model, controls and UI. No build step.
- `plan.jpg` – the architect's original ground floor plan, shown in the Plan panel.

## Run it

Open `index.html` over any static server (module scripts and the plan image need HTTP):

```sh
python3 -m http.server 8765
# then visit http://localhost:8765/
```

Three.js 0.160 is loaded from jsDelivr through an import map; fonts come from Google Fonts.

## Edit the building

Everything is driven by the `P` object and the `ROOMS` list near the top of the module
script. Room rectangles, wall positions, the column grid, plot size and gate position all
live there; the walls, roofs, floors, colliders, labels and the model plan are generated
from those numbers.

## Roof types

The Roof menu in the top bar swaps the whole roof layer between four options common on
new Kerala buildings: clay tile on timber, sloped concrete with tile cladding, a flat
concrete terrace with parapets, and a flat slab with a steel truss and metal sheets above.
Verandah supports, the roof terrace and walk-mode floors follow the choice. Add a type by
extending `ROOF_TYPES` and `buildRoof()`.

## Doors and windows

Openings are declared per wall with `door()`, `win()` and `vent()`. Windows are drawn as
anthracite aluminium frames with tinted glass, a central mullion and top light, a slender
steel safety grille on the outside face (`ext: -1` or `1` says which face is outside) and a
concrete sill; external walls also get a projecting concrete sunshade (`shade: false` turns
it off for windows under the verandah). Doors are flush veneer leaves with a lever handle,
shown swung open so the interiors read.

## Known deviation from the drawing

The labelled room widths (5.78 + 2.40 + 5.06 + 5.06 + 1.50 m) add up to 19.80 m before
any wall thickness, so they cannot fit inside the 19.02 m overall dimension on the
drawing. The model keeps every room at its labelled size, which makes the building
21.89 m long overall (12.10 m deep as drawn).
