# Design

The application architecture is intended to be implemented as follows: 

![Design diagram](https://raw.githubusercontent.com/cheese-drawer/meta/main/MVP_design.svg?token=ACWMUE43OE6G43Y6OQAI2BDAIDPSY)

A user Client implements views (User login, Balance, Transactions, etc.) which communicate with a singular gateway API. 
The Gateway API is responsible for knowing how to contact each of the different services, and for knowing which API route's requests get handled by which services. 
Finally, each service (User Authentication, bank accounts, transactions, etc.) communicates primarily with the Gateway API to receive Client requests, then send responses to the API, who forwards them to the appropriate Client. 

Each service may need to also alert other services of changes in their information; when this happens, they send a one-way message to the appropriate service, without expecting any response.
A service that receives such a message simply needs to take action as it deems necessary.

All communications between the Client & the Gateway API happen over HTTP via a RESTful API.
All communications between the Gateway API and any Service happen over AMQP via RPC.
All communications between any one Service and another Service happen over AMQP via Work Queues.

Finally, each Service may have data storage needs. 
While they can choose to implement their own isolated database server if needed, there will be a singular PostgreSQL database server available to all Services.
Any Service that uses the central PostgreSQL server must create & separately maintain their own database on the server.
Any Service that uses the central PostgreSQL server must not ever interact with a database that belongs to another Service.
