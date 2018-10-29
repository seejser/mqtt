## Source: paho-mqtt.js
(Source: paho-mqtt.js)[http://www.eclipse.org/paho/files/jsdoc/index.html]
eg:
```
var port = 8084

var hostname ="xx.com";
//var hostname ="47.x.x.x";
//console.log(client)
var  settings = {
    userName: 'xx',
    password: 'xxx',
    useSSL:true,
    onSuccess:onConnect
};
// Create a client instance
const client = new Paho.MQTT.Client(hostname, port, "/ws","clientId");

//set callback handlers
client.onConnectionLost = onConnectionLost;
client.onMessageArrived = onMessageArrived;

//connect the client
client.connect(settings);


//called when the client connects
function onConnect() {
    // Once a connection has been made, make a subscription and send a message.
    console.log("onConnect");
//        client.subscribe("World");
//        message = new Paho.MQTT.Message("Hello");
    client.subscribe("LA_d000001/set/ac/temperature");
   const  message = new Paho.MQTT.Message("23");
    message.destinationName = "LA_d000001/set/ac/temperature";
    client.send(message);
}

// called when the client loses its connection
function onConnectionLost(responseObject) {
    if (responseObject.errorCode !== 0) {
        console.log("onConnectionLost:"+responseObject.errorMessage);
    }
}

// called when a message arrives
function onMessageArrived(message) {
    console.log("onMessageArrived:"+message.payloadString);
}

```
