# Notifications

This folder contains examples of notification profile configuration. 

*From the admin guide, https://docs.fortinet.com/document/fortigate/7.6.3/administration-guide/427797/variables-in-actions*

## Variables in actions

A variable can be used to extract information from a trigger event, or the results of a previous action. When the variable is used within an action, the information can be inserted into the content of the new action.
For example, in an automation stitch where a trigger event is an event log and the action is an email notification, the email action can use the `%%log%%` variable to add the log into the email body. In an automation stitch which executes a webhook action followed by an email action, the email action can use the `%%results%%` variable to place the webhook results into the email body.

Both the `%%log%%` and `%%results%%` variables can use sub-variables to drill down on a portion of the source.

For instance, using the following trigger event log:

`date=2025-02-06 time=18:32:21 devid="FGVM04TM2400xxxx" devname="FGDocs" eventtime=1738895541338331122 tz="-0800" logid="0100032002" type="event" subtype="system" level="alert" vd="root" logdesc="Admin login failed" sn="0" user="abc" ui="https(192.168.2.204)" method="https" srcip=192.168.2.204 dstip=192.168.2.87 action="login" status="failed" reason="passwd_invalid" msg="Administrator abc login failed from https(192.168.2.204) because of invalid password"`

- `%%log.user%%` returns *abc*
- `%%log.status%%` returns *failed*
- `%%log.devname%%` returns *FGDocs*
- Sub-variables are determined by the log format and output.

Conversely, `%%results%%` requires an input from a previous action that returns a valid JSON payload. For example, this could be a JSON payload from a webhook action:

```json
{
    "x": "example content x",
    "y": "example content y",
    "results": {
        "port1": {
            "ip": "10.10.10.15",
            "allowaccess": "https"
        }
    },
    "speeds": [
        100,
        1000,
        10000
    ]
}
```

- `%%results.result.port1.ip%%` returns `10.10.10.15`
- `%%results.result.port1.allowaccess%%` returns `https`
- `%%results.x%%` returns example content `x`
- `%%results[set_ip].y%%` returns the value of property `y` from a previous action called `set_ip`
- `%%results.speeds.1%%` returns the item in the array index 1 from the array `speeds`


