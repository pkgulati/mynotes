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
A bound service is the server in a client-server interface. It allows components (such as activities) to bind to the service, send requests, receive responses, and perform interprocess communication (IPC). A bound service typically lives only while it serves another application component and does not run in the background indefinitely.

# Bundle
A mapping from String keys to various Parcelable values

# AlarmManager
This class provides access to the system alarm services. These allow you to schedule your application to be run at some point in the future. When an alarm goes off, the Intent that had been registered for it is broadcast by the system, automatically starting the target application if it is not already running.
In Android, the AlarmManager lets us schedule work to happen at a specific time. If your app has work to do and you’d like it to do that work even when the app isn’t running, then the AlarmManager might be a good solution.
But before we get started, a quick disclaimer. You should only use the AlarmManager when something needs to happen at a specific time. Anything else, and you should be using the JobScheduler. So unless you’re actually making an alarm or something like a clock that chimes every hour on the hour, then you should use the JobScheduler.

# Wake Lock
```
PowerManager powerManager = (PowerManager) getSystemService(POWER_SERVICE);
WakeLock wakeLock = powerManager.newWakeLock(PowerManager.PARTIAL_WAKE_LOCK,
        "MyWakelockTag");
wakeLock.acquire();
...
and later
wakeLock.release()
```

# Adapter
An Adapter object acts as a bridge between an AdapterView and the underlying data for that view. The Adapter provides access to the data items. The Adapter is also responsible for making a View for each item in the data set.

# ArrayAdapter
You can use this adapter to provide views for an AdapterView, Returns a view for each object in a collection of data objects you provide, and can be used with list-based user interface widgets such as ListView or Spinner.

# AdapterView
An AdapterView is a view whose children are determined by an Adapter.

# RecyclerView.ViewHolder
A ViewHolder describes an item view and metadata about its place within the RecyclerView.

# Links
* [Building a chat tutorial](https://blog.sendbird.com/android-chat-tutorial-building-a-messaging-ui)




