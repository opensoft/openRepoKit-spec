# openRepoKit distribution

The user elected a Triad on 2026-10-11: openRepoKit is the assembly root,
openRepoKit-spec owns requirements and contracts, and openRepoKit-code owns
installation, integration tests and three upstream component submodules.
The existing components retain their repositories and source identities.

## Requirements

1. Pin each component by full commit in its code-leg gitlink and this leg's
   `contracts/components.json`. Verify both, including recursive dependencies,
   before installation. Missing, modified or mismatched trees must refuse.
2. Preserve Shape's independence and Tools' own tested Shape dependency.
   The nested Shape commit may differ from the Kit runtime Shape commit.
3. Install into a separate prefix with a versioned source snapshot. Preserve
   existing workBenches commands and support both openBenches and workBenches
   generators through `WORKBENCHES_ROOT` or the explicit `--workbenches`
   installation option.
4. Route Project to the bundled Shape, and override inherited component source
   and revision variables with the selected immutable revisions. Shape uses
   the bundled setup script rather than fetching `main`.
5. Delegate Tools artifact installation to its upstream installer. Keep Claude
   configuration inside the prefix by default; activating user Claude skills
   and hooks is an explicit `--with-claude-integration` option.
6. Never create projects, initialize a personal workspace, authenticate,
   install prerequisites or change component source repositories during Kit
   installation or verification.
7. Preserve upstream refusals and exit statuses. Component self-installation
   through Kit launchers must refuse rather than replace managed launchers.
8. Preserve explicit Project `--workbenches` and `WORKBENCHES_ROOT` selection,
   then the saved release-manifest `workbenches` path and existing
   `.workbenches-path` marker behavior. Without those selections, discover only
   checkouts containing `config/bench-config.json`, trying `openBenches` before
   `workBenches` in each projects convention. With no `PROJECTS_DIR`, the order
   is `~/projects/openBenches`, `~/Projects/openBenches`,
   `~/projects/workBenches`, then `~/Projects/workBenches`; with `PROJECTS_DIR`,
   use only that directory with the same new-first basename order. Do not
   rename the environment export, marker, manifest field, versioned launchers,
   or installed artifacts, and do not move or merge existing checkouts.

## Acceptance

The composed integration suite installs offline into a temporary prefix,
checks exact versions and Project's routing, exercises Shape's real doctor,
proves a source drift refuses before prefix creation, rejects unmanaged
command collisions and verifies repeat installation and paths with spaces.
Focused launcher fixtures cover old-only, new-only, both-present, invalid
automatic candidates, explicit override, saved release metadata, marker
precedence, and downstream `WORKBENCHES_ROOT` export and argument forwarding.
Old-only selects the legacy checkout, new-only selects the new checkout, and
both-present deterministically selects openBenches without renaming the
legacy ABI. These checks establish Kit integration; they do not replace
upstream suites.

## Updating components

Advance component gitlinks in a code feature branch and corresponding full
commits in a spec feature branch. Run integration against that selected pair.
Land both legs, then use openRepoShape's `bump-leg.py` to advance the assembly's
leg pins and gitlinks. Do not automatically advance Tools' nested Shape pin.
