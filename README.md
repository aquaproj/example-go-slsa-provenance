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
  --source-tag v0.1.2
```

:thumbsup: Passed.

```
Verified signature against tlog entry index 9476343 at URL: https://rekor.sigstore.dev/api/v1/log/entries/24296fb24b8ad77a92eb2665ca9575614bc6b0833267eca755ca5d2e8d5a563c2b70c310dad3c0f6
Verified build using builder https://github.com/slsa-framework/slsa-github-generator/.github/workflows/generator_generic_slsa3.yml@refs/tags/v1.4.0 at commit 4581df55e03c5155801ad10b88b19e42f99d8861
PASSED: Verified SLSA provenance
```

Let's verify [example-go-slsa-provenance v0.1.1](https://github.com/aquaproj/example-go-slsa-provenance/releases/tag/v0.1.1).
Assets of this version were tamperred intentionally for demonstrating SLSA Verification.

```sh
slsa-verifier verify-artifact example-go-slsa-provenance_darwin_arm64.tar.gz \
  --provenance-path multiple.intoto.jsonl \
  --source-uri github.com/aquaproj/example-go-slsa-provenance \
  --source-tag v0.1.1
```

:thumbsup: The verification failed expectedly.

```
Verified signature against tlog entry index 9476343 at URL: https://rekor.sigstore.dev/api/v1/log/entries/24296fb24b8ad77a92eb2665ca9575614bc6b0833267eca755ca5d2e8d5a563c2b70c310dad3c0f6
FAILED: SLSA verification failed: expected tag 'refs/tags/v0.1.1', got 'refs/tags/v0.1.2': tag used to generate the binary does not match provenance
Usage:
  slsa-verifier verify-artifact [flags]

Flags:
      --build-workflow-input map[]    [optional] a workflow input provided by a user at trigger time in the format 'key=value'. (Only for 'workflow_dispatch' events on GitHub Actions). (default map[])
      --builder-id string             the unique builder ID who created the provenance
  -h, --help                          help for verify-artifact
      --print-provenance              print the verified provenance to stdout
      --provenance-path string        path to a provenance file
      --source-branch string          [optional] expected branch the binary was compiled from
      --source-tag string             [optional] expected tag the binary was compiled from
      --source-uri string             expected source repository that should have produced the binary, e.g. github.com/some/repo
      --source-versioned-tag string   [optional] expected version the binary was compiled from. Uses semantic version to match the tag

expected tag 'refs/tags/v0.1.1', got 'refs/tags/v0.1.2': tag used to generate the binary does not match provenance
```

## LICENSE

[MIT](LICENSE)
