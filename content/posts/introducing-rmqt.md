---
title: "Introducing rmqt - A Tool for RabbitMQ Maintenance Tasks"
date: 2018-09-11T15:04:55-04:00
draft: true
---

**rmqt** is a command line tool aimed at making maintenance and debugging of RabbitMQ services easier. It's available for windows/macOS/linux and requires your RabbitMQ server/cluster to have the Management Plugin enabled.
## Overview

At a high level, **rmqt** provides tools to help you:

- Query the state of your RabbitMQ services
- Create and restore backups of RabbitMQ topology
- Inspect and reroute messages in realtime
- Clean up stale messages

### Creating and Restoring Backups

The `import`, `export`, and `diff` commands work together to help you maintain backups of your RabbitMQ topologies. You can also use these commands to promote topology changes up through your environments, or even between servers during an upgrade.

First, begin by exporting a current snapshot of your topology using the `export` command:
```bash
$ rmqt export --file=snapshot.json
```

You can filter which exchanges/queues/bindings are including by using the `-e|--exchanges`, `-q|--queues`, and `-b|--bindings` flags. These flags accept regular expressions.

```bash
$ rmqt export --file=snapshot.json --exchanges=^prefix.*
```




### Querying RabbitMQ State

The `query` command gives you the ability to view/filter/format the exchanges, queues, and bindings on your RabbitMQ hosts using Go template syntax.

Example: 
```bash
$ rmqt query "{{table .Exchanges}}"
```