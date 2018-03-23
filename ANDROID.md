# Service
A Service is an application component representing either an application's desire to perform a longer-running operation while not interacting with the user or to supply functionality for other applications to use.
* A Service is not a separate process by default (Although it is possible to achieve it)

# IntentService
To handle aynchronous requests (as intents), to use it extend IntentService and implement onHandleIntent

# Job Scheduler
This is an API for scheduling various types of jobs against the framework that will be executed in your application's own process.

# JobIntentService
Helper for processing work that has been enqueued for a job/service

# Bound Service
### A bound service is the server in a client-server interface. It allows components (such as activities) to bind to the service, send requests, receive responses, and perform interprocess communication (IPC). A bound service typically lives only while it serves another application component and does not run in the background indefinitely.

