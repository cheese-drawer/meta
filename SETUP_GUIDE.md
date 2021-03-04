# Setup Guide

## TL;DR

If you're developing your service in Python, read the first section below ([Service Contracts](#service-contracts)), then start your project with the [Python seed](https://github.com/cheese-drawer/seed-python-rabbitmq-docker).
If you're developing your service with another language, keep reading.

## Service Contracts

Each Service is expected to satisfy each of the following expectations:

1. Integration testing is required for each API endpoint on each Service. These tests will be seen as a "contract" that the API itself guarantees to fulfill.
1. Each Service must include internal unit tests, integrated into the Service's own CI/CD. This should give better reliability expectations.
1. Every PR should be as limited in scope as possible to make reviewing simple.
1. Every PR must be reviewed by the non-author team member before merging.
1. Each Service will be stored in their own repo in the [cheese-drawer](https://github.com/cheese-drawer) organization.
1. Each Service will communicate with the Gateway API over AMQP with an RPC pattern.
1. Each Service will communicate with other Services over AMQP with a Work Queue pattern, when such communication is necessary.
1. Each Service will be deployed as a Docker image to the [cheese-drawer](https://github.com/cheese-drawer) container registry (see [GitHub Container Registry Docs](https://docs.github.com/en/packages/guides/about-github-container-registry)).
