# Super Adventure site

The public site for Super Adventure: the pitch, the player handbook, how to play, and the policies
Discord asks for. It's plain Jekyll, built by GitHub Pages, with no build step and nothing generated
committed.

Feedback lands in this repo's issues and on the org's feedback board.

## Pages

| File | Is |
|---|---|
| `index.html` | the pitch |
| `handbook.html` | every rule, each with a feedback button that opens the issue form |
| `play.md` | adding the stable bot, and asking to join the beta |
| `terms.md`, `privacy.md` | the policies linked from the Discord applications |
| `licences.md` | third-party notices |

Settings shared by several pages, such as the contact address, the install link's client id, the
beta form and the board, are in `_config.yml`.

Run it locally with `docker run --rm -p 4000:4000 -v "$PWD:/srv/jekyll" jekyll/jekyll jekyll serve`.

## Feedback and triage

Every issue carries one of five labels, and the board has a column for each:

| Label | Means |
|---|---|
| `needs triage` | new, not looked at yet |
| `new feature` | something the game doesn't do |
| `enhancement` | a change to something it does |
| `bug` | something broken |
| `won't do` | considered and declined; the issue is closed as not planned |

`.github/workflows/triage.yml` keeps them tidy. A new issue with none gets `needs triage`. Adding
a triage label removes the others and moves the card to its column. `won't do` closes the issue,
and moving a declined issue to any other label reopens it.

## Setting it up, once

1. **Pages:** *Settings → Pages → Deploy from a branch*, `main`, `/ (root)`.
2. **Domain:** add it under *Settings → Pages → Custom domain*, which commits a `CNAME` file. Point
   DNS as GitHub shows you, then tick *Enforce HTTPS*. Verify the domain under the organisation's
   *Settings → Pages* too. Set `url` in `_config.yml` to match.
3. **Labels:**

   ```fish
   gh label delete enhancement --repo Four-Cube-Games/super-adventure --yes
   gh label delete bug --repo Four-Cube-Games/super-adventure --yes
   for label in "needs triage:ededed" "new feature:3e8f4f" "enhancement:1f6feb" "bug:c8343f" "won't do:6e7781"
       set parts (string split : $label)
       gh label create $parts[1] --color $parts[2] --repo Four-Cube-Games/super-adventure --force
   end
   ```

4. **Board:** create a public organisation project (*Four-Cube-Games → Projects → New project →
   Board*) called *Super Adventure feedback*. Add a single-select field **Triage** with the options
   `Needs Triage`, `New Feature`, `Enhancement`, `Bug`, `Won't Do`, in that order, and set the board
   view's columns to it. Under *Settings*, make it public.
5. **Sync:** create a fine-grained token owned by the organisation, with *Projects: read and write*
   on the organisation and nothing else. Add it to this repo as the secret `BOARD_TOKEN`, and the
   project's number (from its URL) as the variable `BOARD`.
6. **Beta form:** create a form on Formspree, and put its endpoint in `beta_form`.
7. Fill in the rest of `_config.yml`: `contact`, `stable_client_id` (stable's *Application ID*),
   and `board`.
8. Enter `/terms/` and `/privacy/` as the Terms of Service and Privacy Policy URLs on stable's
   *General Information*.
