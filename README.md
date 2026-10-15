# strfry-images

Builds **stock upstream** [strfry](https://github.com/hoytech/strfry) release tags
and publishes them to `ghcr.io/nosfabrica/strfry:<tag>`.

Upstream only publishes `ghcr.io/hoytech/strfry:latest`, which any branch push
overwrites, so there is no image for a release. This repo fills that gap.

- Source: `hoytech/strfry` at the given git tag, upstream `Dockerfile`, **no patches**.
- Tags: `:<X.Y.Z>` and `:<X.Y.Z>-sha-<short>`. There is no `:latest`.
- Arches: linux/amd64 + linux/arm64.
- Release tags are immutable. Rebuilding an existing tag fails unless `force=true`.

This is **not** neofry. The patched relay lives on the `neofry` branch of
[nosfabrica/strfry](https://github.com/nosfabrica/strfry) and publishes
`ghcr.io/nosfabrica/neofry`. Don't push upstream tags into that fork: its build
derives `:latest-<ver>` from the highest X.Y.Z tag there.

## Build a release

```bash
gh workflow run build.yml -R nosfabrica/strfry-images -f strfry_tag=1.1.3
gh run watch -R nosfabrica/strfry-images
```
