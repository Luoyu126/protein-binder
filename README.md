# protein-binder

Shared workspace for two parallel lines of de novo binder-design work.

```
protein-binder/
├── complexa-post/     reward-based post-training of Proteina-Complexa
├── RFD4-Proteina/     RFdiffusion4 line
└── docs/              documentation shared by both
```

## Status

**This is the skeleton.** It exists to establish the layout and the git
association; the working trees are not mirrored here yet.

The repository is **public**, so research content is kept local by design —
meeting records, experiment results, pre-registrations and literature surveys
stay on the cluster. See each directory's README for where its content lives.

## Where the real trees are

| directory | upstream / local source |
|---|---|
| `complexa-post/` | `lili-chen/complexa-post`, branch `develop-yunyi` |
| `RFD4-Proteina/` | `RosettaCommons/RFD4-Proteina`, branch `main` |
| `docs/` | `/home/lilic/yunyi/docs`, its own git repository |

Large artifacts (rollouts, checkpoints, evaluation dumps) live on the cluster
under `/grogu/user/lilic/complexa-post/` and are not mirrored anywhere.

## Why `docs/` sits above both code trees

The two lines are developed in parallel and reference the same documents, so
those documents cannot live inside either repository. One consequence: a link
from a document to code has to name the repository.

```markdown
[script](../../complexa-post/build_diversity_weights.py)     ✅
[script](../../build_diversity_weights.py)                   ❌ resolves above the repos
```
