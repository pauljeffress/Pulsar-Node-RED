# Pulsar-Node-RED
Config of my Node-RED environment for the Pulsar Project.
It receives a Mobile Originated (a.k.a. MO) messages from my boat via Iridium Short Burst Data service and a webhook from the Rock7 service.
Once the message arrives I do the following in my main slow;
1. With a "buffer - parser" Node I separate the fields I have coded in a binary buffer into stand alone fields in msg.MOparams.xxx.
2. With a "function" Node I then extract the text formatted msg.payload.transmit_time into an epoch based number format as its unusable in its string/text format.
3. With a "change" Node I then convert all of the remaining Iridium parameters like payload.iridium_longitude from strings to number fields and also place them in fields like msg.MOparams.iridium_longitude.  In this "change" Node, if you look at the last bit of its config, I also then substitute all of my msg.MOparams fields directly into msg.payload.xxx 
4. With a "influxdb out" Node I then pass everything that is in msg.payload.xxx up to my InfluxDB Cloud environment for storage.


I have added the following Nodes to my Node Palette for this flow.
https://flows.nodered.org/node/node-red-contrib-buffer-parser
https://flows.nodered.org/node/node-red-contrib-influxdb
