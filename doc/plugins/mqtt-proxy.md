# Summary
- [**Name**](#name)
- [**Attributes**](#attributes)
- [**How To Enable**](#how-to-enable)
- [**Test Plugin**](#test-plugin)
- [**Disable Plugin**](#disable-plugin)


## Name

The plugin `mqtt-proxy` only works in stream model, it help you to dynamic load
balance by `client_id` of MQTT.

And this plugin both support MQTT [3.1.*](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html) and [5.0](https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html).

## Attributes

|name          |option  |description|
|---------     |--------|-----------|
|protocol_name |require |Name of protocol, shoulds be `MQTT` in normal.|
|protocol_level|require |Level of protocol, it should be `4` for MQTT `3.1.*`. it should be `5` for MQTT `5.0`.|
|upstream.ip   |require |IP address of upstream, will forward current request to.|
|upstream.port |require |Port of upstream, will forward current request to.|


## How To Enable

Creates a stream route, and enable plugin `mqtt-proxy`.

```shell
curl http://127.0.0.1:9080/apisix/admin/stream_routes/1 -X PUT -d '
{
    "remote_addr": "127.0.0.1",
    "plugins": {
        "mqtt-proxy": {
            "protocol_name": "MQTT",
            "protocol_level": 4,
            "upstream": {
                "ip": "127.0.0.1",
                "port": 1980
            }
        }
    }
}'
```

## Delete Plugin

```shell
$ curl http://127.0.0.1:2379/v2/keys/apisix/stream_routes/1 -X DELETE
```

The `mqtt-proxy` plugin has been deleted now.
