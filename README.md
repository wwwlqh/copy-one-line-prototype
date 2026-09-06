# Copy One Line — the first prototype

**Try the prototype:** https://wwwlqh.github.io/copy-one-line-prototype/ (works best on a phone)

**Try the current app in your browser:** https://wwwlqh.github.io/copy-one-line-prototype/app/ (a compiled build of the paper-first app; the first load fetches about 17 MB of fonts)

One line of ancient wisdom a day. You copy it, you learn what it means, and then
you breathe. Nothing is scored, nothing is streaked, and the app never tells you
bad news.

This page was the week-one prototype: a single HTML file where you trace the
eight characters of 應無所住而生其心 (Diamond Sutra) with your thumb, watch each
stroke fill in, read the one-line meaning, then follow a two-minute breathing
circle that leans on the long exhale.

## What happened next

Using it settled one thing quickly: a finger on glass is not writing. The pen has no grip, the thumb drags, a warm hand slips. So the
product changed direction. The real app, now in private development, shows the
line and animates its stroke order, and the hand does the copying on paper.
The phone teaches, remembers, and breathes. Paper does the rest.

This prototype is kept here as the record of that first week: the stroke-data
pipeline, the reveal-under-the-thumb idea, and the breathing timing all
survived into the current build.

## How it works

- `index.html` is the built page: `template.html` with `/*__DATA__*/` replaced
  by `data/chardata.js`.
- Stroke outlines and medians come from
  [hanzi-writer-data](https://github.com/chanind/hanzi-writer-data), one JSON
  per character in `data/`.
- Drawing and stroke matching use
  [hanzi-writer](https://github.com/chanind/hanzi-writer) 3.7.0 in quiz mode,
  loaded from a CDN.
- No server, no account, no analytics, nothing leaves the browser.

### Rebuild after editing the template

```powershell
$p = "path\to\copy-one-line-prototype"
$tpl = [IO.File]::ReadAllText("$p\template.html", [Text.Encoding]::UTF8)
$data = [IO.File]::ReadAllText("$p\data\chardata.js", [Text.Encoding]::UTF8)
[IO.File]::WriteAllText("$p\index.html", $tpl.Replace("/*__DATA__*/", $data), (New-Object Text.UTF8Encoding($false)))
```

### Change the line

Download the JSON for each character from
`https://cdn.jsdelivr.net/npm/hanzi-writer-data@2.0.1/<char>.json` into
`data/`, concatenate them into `chardata.js` as an object keyed by character,
and edit `LINE` and the gloss in `template.html`.

## What to watch when handing it to people

1. Do they slow down, or scrub at it?
2. Do they finish all eight characters without being asked?
3. Do they say anything about the meaning line, unprompted?
4. Do they take the two-minute breath or skip it?
5. Would they want to keep the finished line?

## Stroke data used by the app

`stroke-data/` holds the exact hanzi-writer-data files bundled in the Copy One
Line app, unchanged, with `CHANGES.md` and the Arphic Public License text, as
that licence asks. The app's privacy policy is at `privacy.html`.

## Licences

The page itself (HTML, CSS, script, copy) is © 2026 wwwlqh, all rights
reserved. See `LICENSE`. It is published so people can try it, not as an
open-source project.

Third-party material has its own terms and is included with them:

| Component | Licence | Text |
|---|---|---|
| Glyph stroke data in `data/` (from hanzi-writer-data, derived from Make Me a Hanzi, derived from Arphic PL fonts) | Arphic Public License | `licenses/ARPHIC_PUBLIC_LICENSE.txt` |
| hanzi-writer 3.7.0 (loaded from CDN, not bundled) | MIT, © David Chanin | `licenses/hanzi-writer-MIT.txt` |
| Noto Serif TC, Source Sans 3 (loaded from Google Fonts, not bundled) | SIL Open Font License 1.1 | fonts.google.com |

Per the Arphic Public License, the stroke data files in `data/` are
redistributed unmodified apart from being wrapped as a JavaScript object in
`chardata.js`.
