# Monitoring Fluentd

> Estimated Time: 4 minutes

One of the important aspects of any tool is the ability to be monitored. Fluentd provides special plugins for this purpose where it allows to provide debug information and general internal metrics.

## Step 1: Run Fluentd with Monitor Agent enabled

Get into the laboratory assets:

```
$ cd kelw/labs/2.5/
```

Check the example configuration file for Fluentd

```
$ cat config/test.conf
```

Run Fluentd with the test configuration file and then access the monitoring end-point

```
$ docker run -v $PWD:/kelw -p 24220:24220 kelw/fluentd:0.12 fluentd -c /kelw/config/test.conf
```

Now in a separate terminal window query the internal status using the _CURL_ command line program:

```bash
$ curl http://host:24220/api/plugins.json
{
  "plugins":[
    {
      "plugin_id":"object:3fec669d6ac4",
      "type":"forward",
      "output_plugin":false,
      "config":{
        "type":"forward"
      }
    },
    {
      "plugin_id":"object:3fec669dfa48",
      "type":"monitor_agent",
      "output_plugin":false,
      "config":{
        "type":"monitor_agent",
        "port":"24220"
      }
    },
    {
      "plugin_id":"object:3fec66aead48",
      "type":"forward",
      "output_plugin":true,
      "buffer_queue_length":0,
      "buffer_total_queued_size":0,
      "retry_count":0,
      "config":{
        "type":"forward",
        "host":"192.168.0.11"
      }
    }
  ]
}
```



