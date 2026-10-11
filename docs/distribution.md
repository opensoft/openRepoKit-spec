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
