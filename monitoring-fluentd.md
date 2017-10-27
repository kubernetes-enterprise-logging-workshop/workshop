# Monitoring Fluentd

> Estimated Time: 4 minutes

One of the important aspects of any tool is the ability to be monitored. Fluentd provides special plugins for this purpose where it allows to provide debug information and general internal metrics.

## Step 1: Run Fluentd with Monitor Agent enabled

Run Fluentd against and use the configuration file ABC.conf which will tail and print the data out to JSON files:

```
$ docker run -v vol/vol kelw/fluentd:v0.12 /fluentd/bin/fluentd -c /vol/file.conf
```

> COMMENT: use the following config snippet
>
> &lt;source&gt;  
>     @type monitor\_agent  
>     bind 0.0.0.0  
>     port 24220  
> &lt;/source&gt;

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



