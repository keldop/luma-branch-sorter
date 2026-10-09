# Luma Guardian branch sorter

Upload one or more Google Doc exports (.docx, .md or .txt) and the page sorts every Guardian into the Fire, Earth, Water and Air branch trees using each profile's Branch Theme line.

## Files

| File | What it does | Edit it to |
| --- | --- | --- |
| `index.html` | The page and the sorting logic | Rarely needed |
| `branches.json` | The diagram data: branches, Guardians, Zodiac roots, override rules | Add or reorder branches and Guardians |
| `theme.css` | Every box colour and the shade gradient | Change colours |

Your doc is read in the browser only. It is never uploaded. Do not commit the doc to this repo.

## How the diagram is drawn

The diagram is drawn from `branches.json`, so it shows in full as soon as the page opens. Importing a doc is optional: imported profiles are merged on top, and an imported Guardian replaces the one with the same name in the JSON.

To keep an import for next time: import the doc, click **Download branches.json**, and replace the file in your GitHub repo.

## branches.json

- `branches`: one path per line, written as `Element-Branch-Subbranch`. Parents are created automatically. A path with no imported profile shows as a gray dashed box.
- The order of first-level branches here decides their shade. The first branch listed gets the lightest shade, the last gets the deepest.
- `guardians`: one profile per line with `name`, `path` (for example `Fire-Lumen-Moon-Blossom`) and optional rank, mentor, role, team, guild, zodiac, disciples, plus `sameAs` and `form` (`original` or `evolved`) to mark two names as the same person, like Flora and EmberFlora. A Guardian with no branch has an empty `path` and goes to the No branch yet tab.
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

## Privacy

`branches.json` holds Guardian names, branches, ranks, mentors, roles, teams and guilds. It does not hold civilian names. A public GitHub Pages repo makes this file public, so check it before you commit.

## Colours, status and profile cards

- **Zodiac colours:** a Zodiac root and its first-generation disciples share one colour (Leo, Lumen and Umbra). A branch gets its Zodiac from its own Mentor line, or from a Zodiac's Disciple line. Edit the `z-<zodiac>` rules in `theme.css`. From the 2nd generation onward each generation fades lighter (`gen-2` to `gen-5`, deeper ones reuse `gen-5`); edit the `.z-<zodiac>.gen-N` rules to change a step.
- **Retired and deceased:** these have their own colours (`st-retired`, `st-deceased` in `theme.css`) and a small badge (R or a dagger). Set a status by writing `(retired)` or `(deceased)` after a name in a Mentor or Disciple line, adding a `Status:` line to the profile, or adding `"status"` to the Guardian in `branches.json`.
- **Profile card:** every box opens the same card: Guardian Name, Branch, Based at, Mentor, Disciples. Blank values show `Unknown` (change `BLANK` near the top of the script in `index.html` to use `?`). "Based at" uses a `Based at:` line if the doc has one, otherwise the Guild.
- **View full info:** opens every stored field for that Guardian. Fields listed in `hiddenFields` in `branches.json` (civilian name, date of birth, body measurements, height, weight, blood type) are never read from the doc or saved, so they stay out of a public repo.
