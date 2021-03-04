# Setup Guide

## TL;DR

If you're developing your service in Python, read the first section below ([Service Contracts](#service-contracts)), then start your project with the [Python seed](https://github.com/cheese-drawer/seed-python-rabbitmq-docker).
If you're developing your service with another language, keep reading.

## Service Contracts

Each Service is expected to satisfy each of the following expectations:

1. Integration testing is required for each API endpoint on each service. These tests will be seen as a "contract" that the API itself guarantees to fulfill.
2. Each service must include internal unit tests, integrated into the service's own CI/CD. This should give better reliability expectations.
3. Every PR should be as limited in scope as possible to make reviewing simple.
4. Every PR must be reviewed by the non-author team member before merging.
5. Each service will be stored in their own repo in the [cheese-drawer](https://github.com/cheese-drawer) organization.
