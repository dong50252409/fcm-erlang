# fcm-erlang

This software provides an Erlang client for [`Firebase Cloud Messaging`](https://firebase.google.com/docs/cloud-messaging) to enable notifications to

* Browser
* Android
* iOS notifications

### How to use with rebar3:

You can use fcm_app as a dependency in your rebar.config:

```
{deps , [
    {fcm, {git, "https://github.com/dong50252409/fcm-erlang", {branch, "master"}}}
]}.
```
### Start FCM Service

Two connection types are supported.

1. `start_pool_with_api_key` supports legacy api
2. `start_pool_with_json_service_file` supports http v1 api

```

3> fcm:start_pool_with_api_key(foo, "google_console_server_key").
{ok,<0.60.0>}
4> fcm:start_pool_with_json_service_file(bar, "google_service_file_path.json").
{ok,<0.65.0>}
```

### Stop Service

```
6> fcm:stop(foo).
6> fcm:stop(bar).
```

### How to send a FCM message using from a specific FCM application:

At any time you can send a FCM message to one or more mobile devices by calling:

```
7> fcm:push(RegisteredName, RegIds, Message, Retry).
```

Where

``` 
* `RegistereName` is the atom used during registration
* `RegId` is Registration Id specified as Erlang binary (e.g., `<<"APA91bHun4MxP5egoKMwt2KZFBaFUH-1RYqx...">>`)
* `RegIds` is a list (max 1000 elements) of `RegId`	
* `Message` is an Erlang Map.
* `Retry` is only valid for legacy api.
```

In order to understand `Message` payload see [Message Syntax](https://firebase.google.com/docs/cloud-messaging/http-server-ref#send-downstream).
or [Refer to HTTP v1](https://firebase.google.com/docs/cloud-messaging/send-message#rest)

## Credits

The project was inspired from [pdincau/gcm-erlang](https://github.com/pdincau/gcm-erlang). I would like to thank Paolo for the same.