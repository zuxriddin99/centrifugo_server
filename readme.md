# Centrifugo - Real-time messaging (Websockets) server in Go
## For Running Server need to run `docker-compose up --build -d` after successfully build server will be available on http://localhost:8001 then can connect with client.html file in the project 

## Connection to centrifugo

For connection Centrifugo need to connect websocket with ws://localhost:8001/connection/websocket address
and subscribe main chanel with jwt token. bottom have JS example

`"token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIyIiwiZXhwIjoxNzA0MjgxNTc1LCJpYXQiOjE3MDM2NzY3NzV9.bDb4DcCm5D4_VPO6v3xsNLk_4BG74AiowYHO4dJaHxg"`
```javascript
<script src="https://unpkg.com/centrifuge@5.0.1/dist/centrifuge.js"></script>
<script type="text/javascript">
    const user_id = 8; // need to set self request user id
    const centrifuge = new Centrifuge("ws://188.34.179.79:8001/connection/websocket", {
    token: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzICPtFAGFg"
});

    centrifuge.on('connecting', function (ctx) {
    console.log(`connecting: ${ctx.code}, ${ctx.reason}`);
}).on('connected', function (ctx) {
    console.log(`connected over ${ctx.transport}`);
}).on('disconnected', function (ctx) {
    console.log(`disconnected: ${ctx.code}, ${ctx.reason}`);
}).connect();

    const sub = centrifuge.newSubscription(`main`);
    sub.on('publication', function (ctx) {
    console.log(ctx.data);
}).on('subscribing', function (ctx) {
    console.log(`subscribing: ${ctx.code}, ${ctx.reason}`);
}).on('subscribed', function (ctx) {
    console.log('subscribed', ctx);
}).on('unsubscribed', function (ctx) {
    console.log(`unsubscribed: ${ctx.code}, ${ctx.reason}`);
}).subscribe();
```

### Main doc https://centrifugal.dev/

### other libraries https://centrifugal.dev/docs/server/server_api#http-api-libraries

