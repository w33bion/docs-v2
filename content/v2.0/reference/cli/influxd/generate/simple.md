---
title: influxd generate simple
description: >
  The `influxd generate simple` command generates and writes a simple data set using
  reasonable defaults and CLI flags.
v2.0/tags: [sample-data]
menu:
  v2_0_ref:
    parent: influxd generate
weight: 301
---

The `influxd generate simple` command generates and writes a simple data set using
reasonable defaults and command line interface (CLI) [flags](#flags).

{{% note %}}
#### Important notes
- `influxd generate simple` cannot run while the `influxd` server is running.
  It modifies the index and Time-Structured Merge Tree (TSM) data.
- This tool is intended for development and testing purposes only and
  **should not** be run on a production server.
{{% /note %}}

## Usage
```sh
influxd generate simple [flags]
```

## Flags
| Flag           | Description                                                               | Input Type |
|:----           |:-----------                                                               |:----------:|
| `--print`      | Print data spec and exit                                                  |            |
| `--org`        | Name of organization                                                      | string     |
| `--bucket`     | Name of bucket                                                            | string     |
| `--start-time` | Start time (`YYYY-MM-DDT00:00:00Z`) (default is 00:00:00 of one week ago) | string     |
| `--end-time`   | End time (`YYYY-MM-DDT00:00:00Z`) (default is 00:00:00 of current day)    | string     |
| `--clean`      | Clean time series data files (`none`, `tsm` or `all`) (default `none`)    | string     |
| `--cpuprofile` | Collect a CPU profile                                                     | string     |
| `--memprofile` | Collect a memory profile                                                  | string     |
| `-h`, `--help` | Help for `generate simple`                                                |            |