## ci-workflow libraries

Gflows package with some shared functionalities 

### Usage

1) Reference this project as [GFlows package](https://github.com/jbrunton/gflows/wiki/GFlows-Packages) in `config.yml` file in your [project](https://github.com/CoverGo/scan-code-net/blob/27fadbfe4910ae87ec747411eab5abf76ac66915/.gflows/config.yml). 

```yaml
# Config file for GFlows.
# See https://github.com/jbrunton/gflows/wiki/Configuration for options.
githubDir: github-sample
templates:
  engine: ytt
  defaults:
    libs:
      - workflow-configuration/scan-code-net
    dependencies:
      - https://raw.githubusercontent.com/CoverGo/ci-workflow-libraries/v1.1/.gflows
```
2) Import functions required in your templates and use it in your template file, like [scan-code.template.yml](https://github.com/CoverGo/scan-code-net/blob/27fadbfe4910ae87ec747411eab5abf76ac66915/.gflows/workflows/scan-code-net/scan-code-net.template.yml)
```yaml

#@ load("@ytt:data", "data")
#@ load("@ytt:overlay", "overlay")
#@ load("workflows.lib.yml", "pull_request_defaults")

name: Scan code
"on": #@ pull_request_defaults(data.values.scan_code_net)
jobs:
  build:
    name: Analyse
```

### Functions for producing
- [tags for docker registries](https://github.com/CoverGo/ci-workflow-libraries/blob/master/.gflows/libs/workflows.lib.yml#L39)
- [job names](https://github.com/CoverGo/ci-workflow-libraries/blob/master/.gflows/libs/workflows.lib.yml#L52)
- [docker login step](https://github.com/CoverGo/ci-workflow-libraries/blob/f8a0a9a2ecba53281412c3586d7feea3c5be33a6/.gflows/libs/workflows.lib.yml#L57)
- [diagnostic password generation](https://github.com/CoverGo/ci-workflow-libraries/blob/f8a0a9a2ecba53281412c3586d7feea3c5be33a6/.gflows/libs/workflows.lib.yml#L197)
### Steps for:
- [checkout of private CoverGo actions](https://github.com/CoverGo/ci-workflow-libraries/blob/f8a0a9a2ecba53281412c3586d7feea3c5be33a6/.gflows/libs/workflows.lib.yml#L81)
- [docker image build and publish](https://github.com/CoverGo/ci-workflow-libraries/blob/f8a0a9a2ecba53281412c3586d7feea3c5be33a6/.gflows/libs/workflows.lib.yml#L110) with cache and main registry
- [the legacy integration tests](https://github.com/CoverGo/ci-workflow-libraries/blob/f8a0a9a2ecba53281412c3586d7feea3c5be33a6/.gflows/libs/integration-tests-legacy-steps.lib.yml)
### Full job for:
- [build and publish docker image](https://github.com/CoverGo/ci-workflow-libraries/blob/master/.gflows/libs/workflows.lib.yml#L139)
 
