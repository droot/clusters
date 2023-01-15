# cluster

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cluster`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cluster`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cluster
kpt live apply cluster --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
