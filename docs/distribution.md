# Distribution implementation

Run from assembly: `python3 code/openRepoKit verify` and
`python3 -m unittest discover -s code/tests -v`.

The `code/components/` mounts are unmodified upstream sources. Exact commits
live in `spec/contracts/components.json`. Tools' nested Shape remains its own
dependency, distinct from Kit's runtime Shape. Python 3.10+, Git, Bash and
PyYAML are prerequisites. Installation does not install prerequisites.

The implementation entry point `code/openRepoKit` is an executable Python
command. `code/launcher.py` dispatches installed commands. These files and
their integration tests are implementation; component contracts and prose
documentation belong to this spec leg.

## Checkout discovery

Both openBenches and workBenches checkouts use the existing
`WORKBENCHES_ROOT` launcher export and the release manifest's `workbenches`
field. Selection precedence is explicit Project `--workbenches`, then inherited
`WORKBENCHES_ROOT`, then the path saved by Kit's `--workbenches` installation
option in the release manifest, then Project's existing `.workbenches-path`
marker, and finally automatic new-first discovery. Thus an explicit Project
option overrides a conflicting inherited environment value, and an inherited
environment value overrides conflicting saved and marker paths. Those names and
installed launcher artifacts remain unchanged during the compatibility window.

Without any of those selections, the launcher selects the first candidate
containing `config/bench-config.json` in this order:

1. `~/projects/openBenches`
2. `~/Projects/openBenches`
3. `~/projects/workBenches`
4. `~/Projects/workBenches`

When `PROJECTS_DIR` is set, convention discovery uses only that directory and
tries `openBenches` before `workBenches`. Invalid automatic candidates are
skipped; explicit and saved values retain their existing downstream validation
and are never silently replaced by a discovered checkout. Existing checkouts
are not moved or merged.
