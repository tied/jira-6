<p align="center">
  <a href="https://jira.ulivz.com/" target="_blank">
    <img width="500" src="https://raw.githubusercontent.com/ulivz/jira/master/static/assets/images/jira.jpg" alt="logo">
  </a>
</p>

* [Introduction](#introduction)
* [Features](#features)
* [Architecture](#architecture)
* [API](#api)
* [Test Account](#test-account)
* [Build Setup](#build-setup)
  + [FE only mode](#fe-only-mode)
  + [Full Mode](#full-mode)
  + [Test](#test)
  + [Release](#release)
* [Policy](#policy)

## Introduction

[JIRA](https://www.atlassian.com/software/jira) Software is the project management tool for agile teams.

JIRA itself provides a lot of valuable functions，e.g. **Scrum boards**, **Kanban boards**, **Agile reporting** etc. Surely, this project wasn't a duplicated wheel, It implements a small function that JIRA hasn't implemented at present, which I called `State Report`。

`State Report` stems from the needs of international team cooperation. Suppose there are the following scenes: you are the lead of a multinational technical team. You and your technician are in City A, and your demand side (usually a PM or PD) is in City B, which is 8 time zones away from City A. then you will face a problem —— **How to tell the distant colleagues about the latest ticket's state change every day?**. If you use JIRA, you will find that JIRA does not have a page and records a state of ticket at different time points. And then, it's time for the project to come out.

## Features

- Daily ticket's state report based on sprint
- Responsive UI
- Support multiple teams
- Login Integration
- Built-in filters and sorters 
- Extensible filters
- Extensible sorters

## Architecture

This project follow the standard **separation-of-front-and-backup-end** structure, and uses `Node.js` as the middle layer(BFF).

- FE: `Vue.js`, `vuex`, `iview`
- BFF: `Express`
- API Cache：`LRU-Cache`
- CI: `pm2`

## API

This project depends on following JIRA's API, which are configured in [config.json](https://github.com/ulivz/jira/blob/master/api/config/config.json).

API Name | API URL
---|---
login | `auth/1/session`
issue | `api/2/issue/{id}`
issueWithChangelog | `api/2/issue/{id}?expand=changelog`
user | `api/2/user?username={name}`
backlogUrl | `greenhopper/1.0/xboard/plan/backlog/data.json`
sprintList | `greenhopper/1.0/sprintquery/{teamId}`
sprintIssues | `greenhopper/1.0/rapid/charts/scopechangeburndownchart.json`
sprintReport | `greenhopper/1.0/rapid/charts/sprintreport?rapidViewId={teamId}&sprintId={sprintId}`

## Test Account

Test accounts are configured in [accounts.json](https://github.com/ulivz/jira/blob/master/api/mock/accounts.json).

Uername | Password
---|---
vue | 123456
username | 123456

## Build Setup

It's recommended to use [yarn](https://github.com/yarnpkg/yarn) to manage this project.

### Install Dependencies

```bash
yarn
```

### FE only mode

> This mode is specially opened for the convenience of the demo.

```bash
# serve with hot reload at http://localhost:8081
yarn feonly:dev

# build for production with minification
yarn feonly:build
```

### Full Mode

```bash
# api server at http://localhost:3000
# serve FE with hot reload at http://localhost:8081
yarn dev # equivalent to "yarn dev:fe" & "yarn dev:api"

# build for production with minification
yarn build

# build for production and view the bundle analyzer report
yarn build --report
```

### Test

```bash
# run unit tests
yarn unit

# run e2e tests
yarn e2e

# run all tests
yarn test
```

### Release

> FYI, this is the most primitive CI way, it's recommended to use k8s/docker for continuous integration.

```bash
yarn release  # Release first time
yarn ci       # Follow-up release
```

## Policy

The demo data of this project are all from the real production environment, but all data has been confused in order not to violate the policy.

- All avatars are crawled from the latest [Github Trending](https://github.com/trending).
- All tickets are crawled from [mongodb's JIRA](https://jira.mongodb.org/secure/Dashboard.jspa).
- All names are randomized.

