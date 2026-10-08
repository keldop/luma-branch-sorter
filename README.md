# Luma Guardian branch sorter

Upload one or more Google Doc exports (.docx, .md or .txt) and the page sorts every Guardian into the Fire, Earth, Water and Air branch trees using each profile's Branch Theme line.

## Files

| File | What it does | Edit it to |
| --- | --- | --- |
| `index.html` | The page and the sorting logic | Rarely needed |
| `branches.json` | Branches that already exist, Zodiac roots and override rules | Add or reorder branches |
| `theme.css` | Every box colour and the shade gradient | Change colours |

Your doc is read in the browser only. It is never uploaded. Do not commit the doc to this repo.

## branches.json

- `branches`: one path per line, written as `Element-Branch-Subbranch`. Parents are created automatically. A path with no imported profile shows as a gray dashed box.
- The order of first-level branches here decides their shade. The first branch listed gets the lightest shade, the last gets the deepest.
- `zodiacRoots`: names that sit to the left of an element.
- `overrides`: `from-path => to-path`, for when the doc writes the same branch two ways.

## theme.css

- `.el-fire.shade-0` to `.shade-7` set the gradient for each element (6 colour variables each).
- To recolour one branch, edit the PER-BRANCH section at the bottom, for example `.node.b-lumen { ... }`.
- Classes available: `b-lumen`, `b-umbra`, `b-blaze` and so on, one per first-level branch.

## Run locally

Opening `index.html` by double-click works, but the browser blocks `branches.json` from loading. Use a local server instead:

    python3 -m http.server 8000

then open http://localhost:8000 . On GitHub Pages no extra step is needed.
