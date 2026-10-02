# Super Adventure site

The public site for Super Adventure: the pitch, the rules, a gallery of generated places, how to
play, thanks to the people whose work the game uses, and the policies Discord asks for. It's plain
Jekyll, built by GitHub Pages, with no build step and nothing generated committed.

Feedback lands in this repo's issues and on the org's feedback board.

## Pages

| File | Is |
|---|---|
| `index.html` | the pitch, its pictures taken from the gallery |
| `rules.html` | every rule, in sections with a contents list, each with a feedback button that opens the issue form |
| `gallery.html` | generated places, built from `_data/gallery.yml` (`file`, `title`, `kind`, `caption`; a bare file name is looked for in `assets/gallery/`), filtered by kind, click to enlarge |
| `play.md` | adding the stable bot, opening the Activity, and asking to join the beta |
| `thanks.html` | the artists, data and software the game uses, and their licenses |
| `terms.md`, `privacy.md` | the policies linked from the Discord applications; keep their URLs |
| `handbook.html`, `licenses.md` | redirects to `/rules/` and `/thanks/`, for old links (`_layouts/redirect.html`) |

`_includes/feedback.html` makes a section's feedback button: `{% include feedback.html topic="Raids" %}`.
The site never names the franchise, not even in a URL, and shows no creature art. Before publishing,
grep for the first three letters of its name (case-insensitive, outside `.git`); it should find nothing.

Settings shared by several pages, such as the contact address, the install link's client id, the
beta form and the board, are in `_config.yml`.

Run it locally with `docker run --rm -p 4000:4000 -v "$PWD:/srv/jekyll" jekyll/jekyll jekyll serve`.

## Feedback and triage

Every issue carries one of six labels, and the board has a column for each:

| Label | Means |
|---|---|
| `needs triage` | new, not looked at yet |
| `new feature` | something the game doesn't do |
| `enhancement` | a change to something it does |
| `bug` | something broken |
| `spike` | an idea that needs research before it can be decided |
| `won't do` | considered and declined; the issue is closed as not planned |

`.github/workflows/triage.yml` keeps them tidy. A new issue with none gets `needs triage`. Adding
a triage label removes the others and moves the card to its column. `won't do` closes the issue,
and moving a declined issue to any other label reopens it.

An `epic` groups related tickets as its sub-issues. Epics carry no triage label and stay off the
board's columns; the board's *Parent issue* field shows which epic a card belongs to.

## Setting it up, once

1. **Pages:** *Settings → Pages → Deploy from a branch*, `main`, `/ (root)`.
2. **Domain:** add it under *Settings → Pages → Custom domain*, which commits a `CNAME` file. Point
   DNS as GitHub shows you, then tick *Enforce HTTPS*. Verify the domain under the organization's
   *Settings → Pages* too. Set `url` in `_config.yml` to match.
3. **Labels:**

   ```fish
   gh label delete enhancement --repo Four-Cube-Games/super-adventure --yes
   gh label delete bug --repo Four-Cube-Games/super-adventure --yes
   for label in "needs triage:ededed" "new feature:3e8f4f" "enhancement:1f6feb" "bug:c8343f" "spike:8250df" "won't do:6e7781" "epic:0e8a16"
       set parts (string split : $label)
       gh label create $parts[1] --color $parts[2] --repo Four-Cube-Games/super-adventure --force
   end
   ```

4. **Board:** create a public organization project (*Four-Cube-Games → Projects → New project →
   Board*) called *Super Adventure feedback*. Add a single-select field **Triage** with the options
   `Needs Triage`, `New Feature`, `Enhancement`, `Bug`, `Spike`, `Won't Do`, in that order, and set the board
   view's columns to it. Under *Settings*, make it public.
5. **Sync:** create a fine-grained token owned by the organization, with *Projects: read and write*
   on the organization and nothing else. Add it to this repo as the secret `BOARD_TOKEN`, and the
   project's number (from its URL) as the variable `BOARD`.
6. **Beta form:** create a form on Formspree, and put its endpoint in `beta_form`.
7. Fill in the rest of `_config.yml`: `contact`, `stable_client_id` (stable's *Application ID*),
   and `board`.
8. Enter `/terms/` and `/privacy/` as the Terms of Service and Privacy Policy URLs on stable's
   *General Information*.
