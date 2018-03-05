---
layout: post

title: Cluster information
tip-number: 1
tip-username: bachirooov
tip-username-profile: https://www.twitter.com/bachirooov
tip-tldr: C3 cluster information and state.

categories:
    - en
    - platform
---

The following command give you a lot of information about your cluster. For instance:
- The state of all nodes (wether running or not, for how long they have been up, etc.) 
- What version of `c3-server` and environment is on.
- and more.
```javascript
c3Grid(Cluster.hosts())
```
This can be useful to look at when you have unexplained provisioning errors.