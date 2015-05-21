---
layout: doc
sublayout: guide
title: Repository Notifications
---
Quay.io supports adding _notifications_ to a repository for various events that occur in the repository's lifecycle. To add notifications, click the "Notifications" tab in the [Repository Admin Panel](/glossary/repo-admin.html).

Note: adding notifications requires **repository admin permission**.

### Repository Events

#### <i class="fa fa-lg fa-upload event-icon"></i>Repository Push
<a name="#repo_push"></a>

A successful push of one or more images was made to the repository

<a name="#webhook_repo_push"></a>

```json
{
  "repository": "mynamespace/repository",
  "namespace": "mynamespace",
  "name": "repository",
  "docker_url": "quay.io/mynamespace/repository",
  "homepage": "https://quay.io/repository/mynamespace/repository",
  "visibility": "public",

  "updated_tags": {
    "latest": "b750fe79269d2ec9a3c593ef05b4332b1d1a02a62b4accb2c21d589ff2f5f2dc"
  },
  "pushed_image_count": 10,
  "pruned_image_count": 3
}
```

#### <i class="fa fa-lg fa-tasks event-icon"></i>Dockerfile Build Queued
<a name="#build_queued"></a>

A Dockerfile build has been queued into the build system

<a name="#webhook_build_queued"></a>

```json
{
  "repository": "mynamespace/repository",
  "namespace": "mynamespace",
  "name": "repository",
  "docker_url": "quay.io/mynamespace/repository",
  "homepage": "https://quay.io/repository/mynamespace/repository/build?current=some-fake-build",
  "visibility": "public",

  "is_manual": false,
  "build_id": "build_uuid",
  "build_name": "some-fake-build",
  "docker_tags": ["latest", "foo", "bar"],
  "trigger_kind": "github"
}
```

#### <i class="fa fa-lg fa-circle-o-notch event-icon"></i>Dockerfile Build Started
<a name="#build_started"></a>

A Dockerfile build has been started by the build system

<a name="#webhook_build_started"></a>

```json
{
  "repository": "mynamespace/repository",
  "namespace": "mynamespace",
  "name": "repository",
  "docker_url": "quay.io/mynamespace/repository",
  "homepage": "https://quay.io/repository/mynamespace/repository/build?current=some-fake-build",
  "visibility": "public",

  "build_id": "build_uuid",
  "build_name": "some-fake-build",
  "docker_tags": ["latest", "foo", "bar"],
  "trigger_kind": "github"
}
```

#### <i class="fa fa-lg fa-check-circle-o event-icon"></i>Dockerfile Build Successfully Completed
<a name="#build_success"></a>

A Dockerfile build has been successfully completed by the build system

Note: This event will occur **simultaneously** with a <i class="fa fa-lg fa-upload"></i> _Repository Push_ event for the built image(s)

<a name="#webhook_build_success"></a>

```json
{
  "repository": "mynamespace/repository",
  "namespace": "mynamespace",
  "name": "repository",
  "docker_url": "quay.io/mynamespace/repository",
  "homepage": "https://quay.io/repository/mynamespace/repository/build?current=some-fake-build",
  "visibility": "public",

  "build_id": "build_uuid",
  "build_name": "some-fake-build",
  "docker_tags": ["latest", "foo", "bar"],
  "trigger_kind": "github"
}
```

#### <i class="fa fa-lg fa-times-circle-o event-icon"></i>Dockerfile Build Failed
<a name="#build_failure"></a>

A Dockerfile build has failed

<a name="#webhook_build_failure"></a>

```json
{
  "repository": "mynamespace/repository",
  "namespace": "mynamespace",
  "name": "repository",
  "docker_url": "quay.io/mynamespace/repository",
  "homepage": "https://quay.io/repository/mynamespace/repository/build?current=some-fake-build",
  "visibility": "public",

  "build_id": "build_uuid",
  "build_name": "some-fake-build",
  "docker_tags": ["latest", "foo", "bar"],
  "trigger_kind": "github",

  "error_message": "This is the reason the build failed"
}
```

### Notification Actions

#### <img class="method-icon" src="https://quay.io/static/img/favicon.ico" style="width: 22px; height: 22px;">Quay.io Notification
<a name="quay_notification"></a>

A notification will be added to the Quay.io notification area. The notification area can be found by clicking on the bell icon in the top right of any Quay.io page.

Quay.io Notifications can be setup to be sent to a <i class="fa fa-user entity-icon"></i>_User_, <i class="fa fa-group entity-icon"></i>[_Team_](/glossary/teams.html), or the _organization_ as a whole.

#### <i class="fa fa-lg method-icon fa-envelope"></i>E-mail
<a name="email"></a>

An e-mail will be sent to the specified address describing the event that occurred.

Note: All e-mail addresses will have to be verified on a **per-repository** basis

#### <i class="fa fa-lg method-icon fa-link"></i>Webhook POST
<a name="webhook"></a>

An HTTP POST call will be made to the specified URL with the event's data (see above for each event's data format).

#### <i class="fa fa-lg method-icon hipchat-icon"></i>Hipchat Notification
<a name="hipchat"></a>

Posts a message to HipChat.

#### <i class="fa fa-lg method-icon slack-icon"></i>Slack Notification
<a name="slack"></a>

Posts a message to Slack.

#### <i class="fa fa-lg method-icon flowdock-icon"></i>Flowdock Notification
<a name="flowdock"></a>

Posts a message to Flowdock.
