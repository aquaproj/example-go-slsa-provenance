# example-go-slsa-provenance

Example Go Application with [SLSA Provenance](https://slsa.dev/provenance/v0.2).

SLSA Provenance `multiple.intoto.jsonl` is released in [GitHub Releases](https://github.com/aquaproj/example-go-slsa-provenance/releases).

## GitHub Actions Workflow

[release.yaml](.github/workflows/release.yaml)

## How to verify

1. [Install slsa-verifier v2](https://github.com/slsa-framework/slsa-verifier#installation).
1. [Download asset and multiple.intoto.jsonl from GitHub Releases](https://github.com/aquaproj/example-go-slsa-provenance/releases)
1. Execute slsa-verifier

```sh
slsa-verifier verify-artifact example-go-slsa-provenance_darwin_arm64.tar.gz \
  --provenance-path multiple.intoto.jsonl \
  --source-uri github.com/aquaproj/example-go-slsa-provenance \
  --source-tag v0.1.1
```

:thumbsup: Passed.

```
Verified signature against tlog entry index 9475705 at URL: https://rekor.sigstore.dev/api/v1/log/entries/24296fb24b8ad77a9964977a0a9c3fd73825187368ef5dd3878947ad56d72f6a97a71324571dc55f
Verified build using builder https://github.com/slsa-framework/slsa-github-generator/.github/workflows/generator_generic_slsa3.yml@refs/tags/v1.4.0 at commit 9e9632ad9bfaaaa7d2d082e612cd3418ba23b335
PASSED: Verified SLSA provenance
```

## LICENSE

[MIT](LICENSE)
