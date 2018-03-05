---
layout: post

title: Provisioning history
tip-number: 2
tip-username: bachirooov
tip-username-profile: https://www.twitter.com/bachirooov
tip-tldr: C3 Server provisioning history.

categories:
    - en
    - platform
---

The following command give you information about the provisioning history on your cluster. For instance:
- When the last time someone provisioned was
- What branch of the repo the provisioning was done from!

```javascript
c3Grid(TagProvisionLog.fetch({order: 'descending(meta.created)'}))
```