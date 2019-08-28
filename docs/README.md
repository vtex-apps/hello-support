# Hello Support #

A quick setup for a support app in VTEX.

### Installation ###
```
$ git clone https://github.com/vtex/hello-support support-app
$ cd support-app
$ vtex link
```

Be sure to have [VTEX's toolbelt](https://github.com/vtex/toolbelt)
installed.

### FAQ ###

#### What is a support app? ####

A support app is one of the simplest examples of apps
that run in VTEX IO.

Its purpose is to declare groups of users in the VTEX
platform, and which roles they have access to.

If someone decides to install this app in a workspace,
they will be giving these groups of users the declared
accesses.

This enables app developers to support users having 
trouble with the app functionality.  
Say you're an app developer (which, by reading this, 
you probably are) and a customer is having trouble with 
some feature your apps have. By publishing a support app
with the adequate policies, you can ask your customer
to install it and help them hand-in-hand on their own
workspace!

#### How does it work? ####

By adding the `support` builder into the `builders`
object in `manifest.json`, the app declares that
it contains a `support.json`.

The `support.json` file must be like the example given:

```json
[
  {
    "role": "app-developer",
    "policies": [
      {
        "name": "read-write-workspace"
      },
      {
        "name": "read-workspace-info"
      },
      {
        "name": "link-apps",
        "attrs": {
          "appName": "vendor.appName"
        },
        "reason": "Insert reason here."
      },
      {
        "name": "read-workspace-apps"
      },
    ]
  },
  {
    "role": "support-agent",
    "policies": [
      {
        "name": "read-workspace-info"
      },
      {
        "name": "read-workspace-apps"
      }
    ]
  }
]
```

where `groupName` is the name of the group of people
that will have access to such policies,
and `policies` is an array of object of policies, which can
have
```ts
{
  name: string,
  reason: string,
  attrs: object,
}
```

This allows VTEX IO infrastructure to get this apps' support
policies and add to someone assuming a support role **with the
same vendor as the support app**. That is, having a support
app with vendor A linked to your workspace doesn't mean
a Support Agent from vendor B will have access to those policies.

