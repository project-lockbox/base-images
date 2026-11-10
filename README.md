# base-images

Platform base images for the Lockbox example A.

| Image | Release repository | Pipeline |
|---|---|---|
| `images/alpine-3.24` | `ghcr.io/project-lockbox/alpine-3.24` | `.github/workflows/alpine-3.24.yml` |

Each pipeline calls the Lockbox build template from `project-lockbox/ci-templates` by full commit
SHA. It builds to the staging package `ghcr.io/project-lockbox/staging/<name>`, scans the digest
with Trivy and, only on a pass from the protected `main` branch, promotes it to the release
package tagged with the commit SHA, signs it keyless (GitHub OIDC) and attests provenance.
Lockbox triggers rebuilds of `main` through `workflow_dispatch`. `main` is protected: change it only
by pull request. Both packages are private; workloads get pull access to the release package only.
