# Overleaf Community Edition for LaTeXium

This is the copy of [Overleaf Community Edition](https://github.com/overleaf/overleaf)
that [LaTeXium](https://github.com/VisionLab-IIT/latexium) is built on.
LaTeXium is a self-hosted collaborative LaTeX editor for research labs. Its
own code, deployment and documentation live in
[VisionLab-IIT/latexium](https://github.com/VisionLab-IIT/latexium), which
pins a commit of this repository as a git submodule.

## Branches

* `upstream`: an unmodified mirror of `overleaf/overleaf`.
* `latexium` (default): `upstream` plus this README. Patches to Overleaf
  that LaTeXium cannot avoid would go here, each listed below. LaTeXium adds
  its code through Overleaf's own extension points (a web module, a settings
  file named by `OVERLEAF_CONFIG`, and nginx's `vhost-extras` include)
  instead of editing Overleaf files wherever that is possible.

Upstream releases are merged from `upstream` into `latexium`, never rebased.

## Patches to Overleaf

* Admin navigation (small, so administrators find LaTeXium's admin pages):
  `services/web/frontend/js/shared/components/navbar/admin-menu.tsx` and
  `services/web/app/views/layout/navbar-marketing.pug` get an "Invitations"
  entry (`/admin/lab/invitations`) next to "Manage Users", followed by an
  "Audit log" entry (`/admin/lab/audit`);
  `services/web/app/views/admin/index.pug` gets a one-line notice linking to
  the Users, Invitations and Audit log pages.
* Account menu (small, so members find their AI tokens and connect page):
  `services/web/frontend/js/shared/components/navbar/account-menu-items.tsx`
  (React navbar and project-list sidebar) and
  `services/web/app/views/layout/navbar-marketing.pug` get an "AI assistants"
  entry (`/lab/ai`) after "Account settings", shown only when the right
  footer lists that page (LaTeXium's settings layer adds it in lab mode).
* Logo label (one string, so screen readers do not announce Overleaf's logo
  next to LaTeXium's): `overleaf_logo` in `services/web/locales/en.json` and
  `zh-CN.json`, the accessible name of the editor toolbar's home logo, uses
  the app name (`__appName__ logo`) like the other app-name strings.

* Toolbar extension point (three lines, so the AI assistant's button sits in
  the toolbar's actions on the right, just left of History, where the editor's
  other buttons are): `services/web/frontend/js/features/ide-react/components/toolbar/toolbar.tsx`
  renders the components registered under `toolbarActionsExtraComponents`
  before `ShowHistoryButton`, and `services/web/config/settings.defaults.js`
  lists the key with an empty default (Overleaf's macro fails on an unknown key).

* Project list extension point (a few lines, so the project list can show
  LaTeXium's "AI" badge after the name of each project with AI access on):
  `services/web/frontend/js/features/project-list/components/table/project-list-table-row.tsx`
  renders the components registered under `projectListNameExtras`, each with
  the row's `project`, right after the project's name link, and
  `services/web/config/settings.defaults.js` lists the key with an empty
  default.

* Applied AI proposals (a few lines, so the editor does not open the modal
  "Document Updated Externally" on every Apply and History says what it was):
  `services/web/frontend/js/features/ide-react/context/editor-manager-context.tsx`
  treats an external update with source `lab-ai-proposal` like one from the
  Git bridge (no modal); `.../history/components/change-list/origin.tsx`,
  `.../history/services/types/shared.ts`, `services/web/locales/en.json` and
  `services/web/frontend/extracted-translations.json` give History the label
  "AI proposal applied" for origin kind `lab-ai-proposal`.

## License and trademarks

Overleaf Community Edition is licensed under the GNU Affero General Public
License v3.0 (see [LICENSE](../LICENSE)); so is everything in this
repository.

Overleaf® is a registered trademark of its owner. LaTeXium is not affiliated
with, endorsed by or supported by Overleaf.
