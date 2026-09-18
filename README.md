# argocd-loadtest-fixture

Disposable Kubernetes manifest set used as a synthetic source for load testing a GitOps controller (Argo CD). Nested under `apps/<team>/<app>/base/` to mimic a realistic multi-layer repo path instead of a flat root.

Contents, 7 resources per app:
- ConfigMap, Secret, ServiceAccount, Service, NetworkPolicy: cheap, always resolve to a terminal state.
- Deployment at 0 replicas: exercises the reconcile/sync/health pipeline without ever scheduling a real pod.
- Job with `spec.suspend: true`: never runs, so it never reaches a terminal Complete/Failed condition. Argo CD's health check for it stays Progressing indefinitely, which forces the controller to keep re-evaluating this app's health on every reconcile loop instead of settling, a stand-in for real apps whose health never quite goes fully green.

Safe to delete once the load test it supports is finished.
