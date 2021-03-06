---
title: InfluxDBOutNode (Kapacitor TICKscript node)
description: InfluxDBOutNode writes data to an InfluxDB database as it is received.
note: Auto generated by tickdoc

menu:
  kapacitor_1_4:
    name: InfluxDBOutNode
    weight: 150
    parent: TICKscript nodes
---
### Constructor

| Chaining Method | Description |
|:---------|:---------|
| **[influxDBOut](#descr)&nbsp;(&nbsp;)** | Create an influxdb output node that will store the incoming data into InfluxDB.  |

### Property Methods

| Setters | Description |
|:---|:---|
| **[buffer](#buffer)&nbsp;(&nbsp;`value`&nbsp;`int64`)** | Number of points to buffer when writing to InfluxDB. Default: 1000  |
| **[cluster](#cluster)&nbsp;(&nbsp;`value`&nbsp;`string`)** | The name of the InfluxDB instance to connect to. If empty the configured default will be used.  |
| **[create](#create)&nbsp;(&nbsp;)** | Create indicates that both the database and retention policy will be created, when the task is started. If the retention policy name is empty then no retention policy will be specified and the default retention policy name will be created.  |
| **[database](#database)&nbsp;(&nbsp;`value`&nbsp;`string`)** | The name of the database.  |
| **[flushInterval](#flushinterval)&nbsp;(&nbsp;`value`&nbsp;`time.Duration`)** | Write points to InfluxDB after interval even if buffer is not full. Default: 10s  |
| **[measurement](#measurement)&nbsp;(&nbsp;`value`&nbsp;`string`)** | The name of the measurement.  |
| **[precision](#precision)&nbsp;(&nbsp;`value`&nbsp;`string`)** | The precision to use when writing the data.  |
| **[retentionPolicy](#retentionpolicy)&nbsp;(&nbsp;`value`&nbsp;`string`)** | The name of the retention policy.  |
| **[tag](#tag)&nbsp;(&nbsp;`key`&nbsp;`string`,&nbsp;`value`&nbsp;`string`)** | Add a static tag to all data points. Tag can be called more then once.  |
| **[writeConsistency](#writeconsistency)&nbsp;(&nbsp;`value`&nbsp;`string`)** | The write consistency to use when writing the data.  |



### Chaining Methods
[Deadman](/kapacitor/v1.4/nodes/influx_d_b_out_node/#deadman), [Stats](/kapacitor/v1.4/nodes/influx_d_b_out_node/#stats)
<a id='descr'/><hr/><br/>
### Description

Writes the data to InfluxDB as it is received.

Example:


```javascript
    stream
        |from()
            .measurement('requests')
        |eval(lambda: "errors" / "total")
            .as('error_percent')
        // Write the transformed data to InfluxDB
        |influxDBOut()
            .database('mydb')
            .retentionPolicy('myrp')
            .measurement('errors')
            .tag('kapacitor', 'true')
            .tag('version', '0.2')
```

Available Statistics:

* points_written -- number of points written to InfluxDB
* write_errors -- number of errors attempting to write to InfluxDB



<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>

Properties
----------

Property methods modify state on the calling node.
They do not add another node to the pipeline, and always return a reference to the calling node.
Property methods are marked using the `.` operator.


### Buffer

Number of points to buffer when writing to InfluxDB.
Default: 1000


```javascript
influxDBOut.buffer(value int64)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### Cluster

The name of the InfluxDB instance to connect to.
If empty the configured default will be used.


```javascript
influxDBOut.cluster(value string)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### Create

Create indicates that both the database and retention policy
will be created, when the task is started.
If the retention policy name is empty then no
retention policy will be specified and
the default retention policy name will be created.

If the database already exists nothing happens.



```javascript
influxDBOut.create()
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### Database

The name of the database.


```javascript
influxDBOut.database(value string)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### FlushInterval

Write points to InfluxDB after interval even if buffer is not full.
Default: 10s


```javascript
influxDBOut.flushInterval(value time.Duration)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### Measurement

The name of the measurement.


```javascript
influxDBOut.measurement(value string)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### Precision

The precision to use when writing the data.


```javascript
influxDBOut.precision(value string)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### RetentionPolicy

The name of the retention policy.


```javascript
influxDBOut.retentionPolicy(value string)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### Tag

Add a static tag to all data points.
Tag can be called more then once.



```javascript
influxDBOut.tag(key string, value string)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


### WriteConsistency

The write consistency to use when writing the data.


```javascript
influxDBOut.writeConsistency(value string)
```

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>


Chaining Methods
----------------

Chaining methods create a new node in the pipeline as a child of the calling node.
They do not modify the calling node.
Chaining methods are marked using the `|` operator.


### Deadman

Helper function for creating an alert on low throughput, a.k.a. deadman's switch.

- Threshold -- trigger alert if throughput drops below threshold in points/interval.
- Interval -- how often to check the throughput.
- Expressions -- optional list of expressions to also evaluate. Useful for time of day alerting.

Example:


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    data
        |deadman(100.0, 10s)
    //Do normal processing of data
    data...
```

The above is equivalent to this
Example:


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    data
        |stats(10s)
            .align()
        |derivative('emitted')
            .unit(10s)
            .nonNegative()
        |alert()
            .id('node \'stream0\' in task \'{{ .TaskName }}\'')
            .message('{{ .ID }} is {{ if eq .Level "OK" }}alive{{ else }}dead{{ end }}: {{ index .Fields "emitted" | printf "%0.3f" }} points/10s.')
            .crit(lambda: "emitted" <= 100.0)
    //Do normal processing of data
    data...
```

The `id` and `message` alert properties can be configured globally via the 'deadman' configuration section.

Since the [AlertNode](/kapacitor/v1.4/nodes/alert_node/) is the last piece it can be further modified as usual.
Example:


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    data
        |deadman(100.0, 10s)
            .slack()
            .channel('#dead_tasks')
    //Do normal processing of data
    data...
```

You can specify additional lambda expressions to further constrain when the deadman's switch is triggered.
Example:


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    // Only trigger the alert if the time of day is between 8am-5pm.
    data
        |deadman(100.0, 10s, lambda: hour("time") >= 8 AND hour("time") <= 17)
    //Do normal processing of data
    data...
```



```javascript
influxDBOut|deadman(threshold float64, interval time.Duration, expr ...ast.LambdaNode)
```

Returns: [AlertNode](/kapacitor/v1.4/nodes/alert_node/)

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>

### Stats

Create a new stream of data that contains the internal statistics of the node.
The interval represents how often to emit the statistics based on real time.
This means the interval time is independent of the times of the data points the source node is receiving.


```javascript
influxDBOut|stats(interval time.Duration)
```

Returns: [StatsNode](/kapacitor/v1.4/nodes/stats_node/)

<a class="top" href="javascript:document.getElementsByClassName('article-heading')[0].scrollIntoView();" title="top"><span class="icon arrow-up"></span></a>
