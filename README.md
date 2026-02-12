# Progressive Canary Deployment Pipeline

This repository contains the Harness Git Experience configuration files for implementing a multi-stage progressive canary rollout strategy.

## References:
1. https://developer.harness.io/docs/continuous-delivery/deploy-srv-diff-platforms/kubernetes/kubernetes-executions/create-a-kubernetes-canary-deployment/#harness-canary-deployments
2. https://developer.harness.io/docs/continuous-delivery/x-platform-cd-features/sequential-and-parallel-deployments


## Components

* **`connector.yaml`**: Configures a GitHub connector (`harnessgitconnector`) to access the `harnesscd-example-apps` repository using a token reference (`harness_gitpat`).
* **`service.yaml`**: Defines the `harnessguestbookdep` service, which pulls a Helm chart from the `master` branch of the `harnesscd-example-apps` repository.
* **`pipeline.yaml`**: Orchestrates a three-stage deployment process (`dev`, `qa`, and `production`) featuring canary rollouts, shell script verifications, and manual approvals.

## Pipeline Stages

1.  **Deploy to Dev**: Executes a 25% canary deployment to the `dev` environment in both infrastructure definitions `dev_sk_ring0_infra` and `dev_sk_ring1_infra`.
2.  **Deploy to QA Ring0**: Performs a 25% canary rollout in the `qa` environment.
3.  **Deploy to Production Ring1**: Implements a 25% canary deployment in `production` with continuous verification and a 15-minute wait period before the final rolling update.

## Requirements

* **Harness Setup**: Requires a Harness account with the organization and project set to `default` and `default_project`.
* **Environments**: Environments must exist  dev, qa, prod.
* **Infrastructure**: Infrastructure definitions must exist for `dev_sk_ring0_infra`, `qa_sk_ring0_infra`, and `prod_sk_ring1_infra`.
* **Secrets**: A GitHub Personal Access Token must be stored as a Harness secret named `harness_gitpat`.

## External Resources

* **Application Repository**: [harnesscd-example-apps](https://github.com/srumonke/harnesscd-example-apps)

