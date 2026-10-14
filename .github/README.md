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

## License and trademarks

Overleaf Community Edition is licensed under the GNU Affero General Public
License v3.0 (see [LICENSE](../LICENSE)); so is everything in this
repository.

Overleaf® is a registered trademark of its owner. LaTeXium is not affiliated
with, endorsed by or supported by Overleaf.
