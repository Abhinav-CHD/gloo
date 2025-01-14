# End-to-End Tests

## Background

Gloo Edge is built to integrate with a user's environment. By enabling users to select their preferred tools for scheduling, persistence, and security, we must ensure that we have end-to-end tests to validate these scenarios.

We support the following types of end-to-end tests:
- [In Memory end-to-end](./e2e#in-memory-end-to-end-tests)
- [Kubernetes end-to-end](./kube2e#kubernetes-end-to-end-tests)
- [Consul/Vault end-to-end](./consulvaulte2e)

## CI
Each test suite may run on different infrastructure. Refer to the README of each test suite for more information.

## Performance tests

Our tests include some performance tests which variably guard against regressions in performance or validate decisions made to choose one algorithm over others.

These are located next to the code that they test and are denoted with the `Performance` label and are executed as part of our nightly tests rather than in CI.

To find the results of these, navigate to the "Actions" tab in the Github UI, click on the ["Nightly" workflow](https://github.com/solo-io/gloo/actions/workflows/nightly-tests.yaml), and select the latest run.
It may be useful to search for the name of the particular test you're investigating in order to quickly find the results.

Note that tests which use the go-utils benchmarking package only compile and run on Linux machines.
When developing performance tests it may be helpful to manually trigger runs of the Nightly job from the development branch.