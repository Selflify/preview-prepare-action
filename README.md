# Selflify Preview Prepare Action

Prepare a preview deployment matrix from `.github/preview-sites.json`, compute the preview path name, and resolve the related pull request number.

## What it does

- validates the preview site config file
- exposes the deploy matrix for later jobs
- computes a stable preview path such as `pr-42`, `stable`, or a normalized branch/tag name
- resolves the pull request number for comment publishing

## Usage

```yaml
- id: preview
  uses: Selflify/preview-prepare-action@v1
  with:
    config-path: .github/preview-sites.json
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Outputs

- `path_name`
- `pr_number`
- `matrix`
- `site_names`

## Expected config format

```json
{
  "include": [
    {
      "site": "marketing",
      "node_version": "20",
      "setup_cmd": "",
      "install_cmd": "yarn install --immutable",
      "build_cmd": "yarn build",
      "output": "dist"
    }
  ]
}
```

## Marketplace-style repository layout

- `action.yml` declares the composite action contract
- `README.md` is the public and Marketplace-facing documentation
- `LICENSE` keeps the repo ready for public reuse
- `v1` is the stable tag that caller workflows should use

## Publishing flow

1. push the repository changes
2. create or update the `v1` tag
3. optionally create a GitHub Release
4. publish the repo in GitHub Marketplace from the repository UI when you need a listing
