# GitHub Actions Branches Reproduction

Reproduction for https://github.com/renovatebot/renovate/issues/40172

## Problem

The workflow in `.github/workflows/test.yml` uses GitHub Actions that reference **branches** instead of tags:

```yaml
- uses: christopherhx/gitea-upload-artifact@v4
- uses: christopherhx/gitea-download-artifact@v4
```

Here, `v4` is a **branch**, not a tag. The GitHub Actions runner supports this, but Renovate's `github-tags` datasource only queries `refs/tags/`, so:

1. Renovate cannot find version information for these actions
2. Renovate cannot pin digests for these actions

## Expected Behavior

Renovate should be able to pin digests for branch-based actions using a new `github-branches` datasource.

