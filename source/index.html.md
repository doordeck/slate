---
title: Doordeck API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='mailto:info@doordeck.com'>Contact Doordeck</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - authentication
  - account
  - site
  - tile
  - operations
  - platform
  - encoding
  - errors

search: true
---

# Introduction

Welcome to the Doordeck API! You can use our API to access Doordeck API endpoints, 
which can get information on the state of locks, manage access and perform operations.

This API documentation is generated using [Slate](https://github.com/lord/slate), 
if you spot any errors please submit a pull request directly on [Github](https://github.com/doordeck/docs/).

This API documentation includes details of both endpoints available to Doordeck users (i.e. users who have registered
on [Doordeck](https://app.doordeck.com) directly) and to third-party app developers, some endpoints are only available 
to one set of users, these are flagged as follows:

<aside class="warning">
This endpoint is only available to users with Doordeck issued auth tokens.
</aside>

## Environments

Doordeck operates production, staging and development environments at the following locations:

 - https://api.doordeck.com
 - https://api.staging.doordeck.com
 - https://api.dev.doordeck.com
 
 Newer endpoints may only exist in staging or development environments, these will be flagged as such. 
