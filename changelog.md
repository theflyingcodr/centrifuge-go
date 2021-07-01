v0.7.1
======

* Fix atomic align on 32-bit [#49](https://github.com/theflyingcodr/centrifuge-go/pull/49)

v0.7.0
======

* Updated `github.com/centrifugal/protocol` package dependency to catch up with the latest changes in it
* Introduced `Error` type which is used where we previously exposed `protocol.Error` – so there is no need to import `protocol` package in application code to investigate error code or message
* Methods `Client.SetName` and `Client.SetVersion` removed in favour of `Name` and `Version` fields of `Config`
* Add top-level methods `Client.History`, `Client.Presence`, `Client.PresenceStats` – so it's possible to call corresponding client API methods when using server-side subscriptions

```
$ gorelease -base v0.6.5 -version v0.7.0
github.com/theflyingcodr/centrifuge-go
------------------------------------
Incompatible changes:
- (*Client).SetName: removed
- (*Client).SetVersion: removed
Compatible changes:
- (*Client).History: added
- (*Client).Presence: added
- (*Client).PresenceStats: added
- Config.Name: added
- Config.Version: added
- DefaultName: added
- Error: added

v0.7.0 is a valid semantic version for this release.
```

v0.6.5
======

* One more fix for memory align on 32bit arch, see [#46](https://github.com/theflyingcodr/centrifuge-go/pull/46)

v0.6.4
======

* Add `Subscription.Close` method to close Subscription when it's not needed anymore. This method unsubscribes from a channel and removes Subscription from internal `Client` subscription registry – thus freeing resources. Subscription is not usable after `Close` called. This method can be helpful if you work with lots of short-living subscriptions to different channels to prevent unlimited internal Subscription registry growth.

v0.6.3
======

* Fix memory align on 32bit arch, see [#40](https://github.com/theflyingcodr/centrifuge-go/pull/40)

v0.6.2
======

* fix deadlock on a private channel resubscribe - see [#38](https://github.com/theflyingcodr/centrifuge-go/pull/38)

v0.6.1
======

* fix setting server-side unsubscribe handler, call server-side unsubscribe event on disconnect 

v0.6.0
======

* server-side subscriptions support
* get rid of Protobuf protocol struct `Publication` and `ClientInfo` aliases – use library scope structures instead
* change return values of `RPC`, `NamedRPC`, `History`, `Presence`, `PresenceStats`, `Publish` methods to be more meaningful and extensible
* much faster resubscribe to many subscriptions (previously we waited for each individual subscription response before moving further, now process is asynchronous)
* improved reconnect logic
* Client and Subscription status refactoring
* fix inconsistent join/subscribe event ordering – now both processed in order coming from server

v0.5.2
======

* `NamedRPC` method added - [#35](https://github.com/theflyingcodr/centrifuge-go/pull/35), thanks [@L11R](https://github.com/L11R)
