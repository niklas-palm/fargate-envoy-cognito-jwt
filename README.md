# ECS Fargate with Envoy sidecar for JWT + Cognito

Sample ECS service with Fargate with an Envoy proxy running as a sidecar that validates incoming requests using the JWT Authorizer HTTP filter with Cognito as JWT Issuer.

## Prerequisites

- A Cognito Userpool. Enter the region and userpool id in the `envoy/parameters.sh` file
- 2 ECR repositories - one for the app image and one for the envoy image. Replace the environment variables in `.github/workflow/build_deploy.yaml` with your ECR repositories.
- Trust set up between Github and your AWS account. Replace the `OIDC_ROLE` with your own in `.github/workflow/build_deploy.yaml`
- Ensure VPC CIDR doesn't overlap with existing ranges

## Overview

- `/infra`
  The AWS infrastructure --> network, ECS service, task definition etc.

- `/app`
  The sample application container

- `/envoy`
  The sample Envoy sidecar container authenticating tokens against Cognito.

## Considerations

- Image build separation
  Currently there's a new Envoy and App image created and registered with ECR with every new commit. Optimally, the build of the images would be separate.
