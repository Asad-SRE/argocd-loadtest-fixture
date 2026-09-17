# argocd-loadtest-fixture

Disposable, minimal Kubernetes manifest used as a synthetic source for load testing a GitOps controller (Argo CD). The Deployment runs at 0 replicas, so applying it never schedules real pods, only the reconcile/sync/health pipeline of the controller is exercised.

Safe to delete once the load test it supports is finished.
