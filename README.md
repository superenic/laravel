# Queue server provide

A server has 1 Millon of requests, those should be resolved as soon as possible, one
example is the email, it should be mailed now. A server sends 1 million of request
in one second is not possible, it consumes a lot of resources or can crash itself.

Provide a service do not mean you should use a single server, you can use more of
one to consume a list of jobs/tasks.

Laravel provides a functionality call Queue, this methodology work in the follow way:

- Create a list of tasks should be resolved one by one.
- Create a microserver (how many you want) all of the execute (PHP artisan queue:work).
  > queue:work create consumer jobs, resolve pendings.

Adding this methodology you can use Events to resolve these issues in the way you want.
For this repository take decisions from 2 ideas.

Scenario: The server provider is down.

  Server consumers try to get resources from the server providers, but it has issues.

Given server throw 500 or higher error
When server consumer tries to connect to the server
then Server should send an email to support technique
  and move all task to next day to avoid errors on our side

Scenario: server consumer receive a bad request

Given Server throw 400 to 499 
When server consumer tries to connect to the server
then server consumer send an email to developer to get a solution for this issue
