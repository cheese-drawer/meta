# Setup Guide

## TL;DR

If you're developing your service in Python, read the first section below ([Service contracts](#service-contracts)), then start your project with the [Python seed](https://github.com/cheese-drawer/seed-python-rabbitmq-docker).
If you're developing your service with another language, keep reading.

## Service contracts

Each Service is expected to satisfy each of the following expectations:

1. Integration testing is required for each API endpoint on each Service. These tests will be seen as a "contract" that the API itself guarantees to fulfill.
1. Each Service must include internal unit tests, integrated into the Service's own CI/CD. This should give better reliability expectations.
1. Every PR should be as limited in scope as possible to make reviewing simple.
1. Every PR must be reviewed by the non-author team member before merging.
1. Each Service will be stored in their own repo in the [cheese-drawer](https://github.com/cheese-drawer) organization.
1. Each Service will communicate with the Gateway API over AMQP with an RPC pattern.
1. Each Service will communicate with other Services over AMQP with a Work Queue pattern, when such communication is necessary.
1. Each Service will be deployed as a Docker image to the [cheese-drawer](https://github.com/cheese-drawer) container registry (see [GitHub Container Registry Docs](https://docs.github.com/en/packages/guides/about-github-container-registry)).

## Best practices

When designing a new Service keep the following ideas in mind:

### Limited Service to Service communication

Communication between Services should be as limited as possible. 
While it's not practical to limit all communications between Services, an 'ideal' Service is self-contained with no communication to any entities other than the Gateway API.

When a Service does need to communicate something to another Service, the amount of knowledge needed about that other Service should be as minimal as possible. 
The reason for limiting this knowledge is to encourage loose coupling, allowing for easier development about a Service in as independant of a manner as possible. 

For this reason, the [Service contracts](#service-contracts) define inter-Service communication to use a Work Queue pattern over AMQP.
The Work Queue pattern is one-way--a sender simply pushes a message to a queue, expecting no response.
This means that a sender doesn't care about what is done with the message, simply that it was sent.
Additionally, a receiver not having to worry about sending a response to a sender means the only thing they have to know about the other Service is how to integrate the data from the message into their existing structure.

## Example

To see an example of a Service that follows the guidelines above, see the [Python seed project repo](https://github.com/cheese-drawer/seed-python-rabbitmq-docker).
The [Development usage section](https://github.com/cheese-drawer/seed-python-rabbitmq-docker/tree/async#development-usage) of the seed project's README outlines the basics of how a Python Service may work in a simplified example.
