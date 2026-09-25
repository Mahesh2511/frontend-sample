# frontend-sample

A demo **frontend** consumer of `devsecops-shared-github-actions`. XML configuration lives under `config/`.

The repository has no validation logic. Its workflow `.github/workflows/build.yml` declares:

```yaml
uses: Mahesh2511/devsecops-shared-github-actions/.github/workflows/build.yml@v1
with:
  artifact_type: frontend
  xml_path: config
```

On every pull request the shared framework checks that every `*.xml` under `config/` (recursively) is well-formed, before the build is allowed to run. The path is plain configuration, so another repo could pass `xml_path: src/main/resources`.

**Demo a failure:** open a PR that removes a closing tag in `config/settings.xml`. `PR Check` fails with an annotation on the file and `Build` is skipped. Revert the change and the check passes again.
