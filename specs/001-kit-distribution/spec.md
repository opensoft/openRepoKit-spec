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
   existing workBenches commands and support its generators through
   `WORKBENCHES_ROOT` or an explicit installation option.
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

## Acceptance

The composed integration suite installs offline into a temporary prefix,
checks exact versions and Project's routing, exercises Shape's real doctor,
proves a source drift refuses before prefix creation, rejects unmanaged
command collisions and verifies repeat installation and paths with spaces.
These checks establish Kit integration; they do not replace upstream suites.

## Updating components

Advance component gitlinks in a code feature branch and corresponding full
commits in a spec feature branch. Run integration against that selected pair.
Land both legs, then use openRepoShape's `bump-leg.py` to advance the assembly's
leg pins and gitlinks. Do not automatically advance Tools' nested Shape pin.
