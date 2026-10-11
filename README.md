# openRepoKit-spec

The **spec leg** of the `openrepokit` project: requirements, decisions and
acceptance criteria. The implementation lives in
[`opensoft/openRepoKit-code`](https://github.com/opensoft/openRepoKit-code).

**Clone the assembly root, not this repository.** This leg is mounted as a
submodule at `spec/` inside
[`opensoft/openRepoKit`](https://github.com/opensoft/openRepoKit), which
is what pins the commit of this repository that the project currently is:

```sh
git clone --recurse-submodules /home/brett/Projects/.openRepoKit-remotes/openRepoKit.git
cd openRepoKit
make bootstrap
```

Working here directly is fine — it is an ordinary repository with an ordinary
branch. What advancing this leg does NOT do is advance the project: that is a
commit in the assembly root moving the gitlink, `contracts/spec-pin.yaml` and
any workflow `@<sha>` reference together.

Being the spec leg confers no authority over specifications. The split is
navigation; authority travels in grants, and a project that keeps spec and
code in one repository is reviewed identically.

Topic: `xf-project-openrepokit`.
