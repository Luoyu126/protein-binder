# protein-binder

Shared workspace for two parallel lines of de novo binder-design work.

```
protein-binder/
├── complexa-post/     reward-based post-training of Proteina-Complexa
├── RFD4-Proteina/     RFdiffusion4 line
├── docs/              documentation shared by both
└── baselines/         third-party baselines (RFdiffusion and friends)
```

## What this repository tracks

**Only the layout.** The four directories above are each their own git
repository, nested inside this one and deliberately ignored here — so this
repo holds exactly this README and a `.gitignore`.

The reason is mechanical: git does not recurse into a nested repository. A
`git add -A` here would record each one as a bare gitlink — a submodule entry
with no `.gitmodules` — which GitHub renders as a grey row you cannot open and
a clone turns into three empty directories. Ignoring them keeps that from
happening by accident.

## Where each tree actually lives

| directory | its own remote | branch |
|---|---|---|
| `complexa-post/` | `lili-chen/complexa-post` | `develop-yunyi` |
| `RFD4-Proteina/` | `RosettaCommons/RFD4-Proteina` | `main` |
| `docs/` | local only, no remote yet | `master` |
| `baselines/` | not a git repository | — |

Large artifacts — rollouts, checkpoints, evaluation dumps — live on the cluster
under `/grogu/user/lilic/complexa-post/` and are mirrored nowhere.

## This repository is public

So research content is kept out of it by design: meeting records, experiment
results, pre-registrations and literature surveys stay in `docs/`, which has
its own git repository and no remote. `.gitignore` also excludes third-party
PDFs, model weights, generated designs and the symlinks that point into the
cluster's `/grogu` mount.

## `/home/lilic/yunyi/` keeps symlinks to the old paths

The three trees used to sit directly under `/home/lilic/yunyi/`. 164 job
scripts hardcode `REPO_DIR=/home/lilic/yunyi/complexa-post`, as do the
apptainer `--bind` lines and the Slurm `--output` paths, so moving them would
have broken every running and queued job. Symlinks keep the old paths working:

```
/home/lilic/yunyi/complexa-post  -> protein-binder/complexa-post
/home/lilic/yunyi/RFD4-Proteina  -> protein-binder/RFD4-Proteina
/home/lilic/yunyi/docs           -> protein-binder/docs
/home/lilic/yunyi/baselines      -> protein-binder/baselines
```

Removing a symlink breaks the jobs. Rewrite the paths in `job/` first if you
want them gone.

## `docs/` sits above both code trees

The two lines reference the same documents, so those documents cannot live
inside either repository. One consequence: a link from a document to code has
to name the repository.

```markdown
[script](../../complexa-post/build_diversity_weights.py)     ✅
[script](../../build_diversity_weights.py)                   ❌ resolves above the repos
```
