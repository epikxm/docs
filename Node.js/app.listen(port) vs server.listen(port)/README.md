# express 서버 기본

## app.listen(80) vs. server.listen(80) 무엇이 다른가?

-   결론은 <b>다르지 않다.</b>

```javascript
> index1.js

const express = require('express');
const app = express();

const port = process.env.PORT || 3000;

app.listen(port);
```

---

```javascript
> index2.js

const http = require('http');
const express = require('express');
const app = express();

const port = process.env.PORT || 3000;

const server = http.createServer(app);
server.listen(port);
```

---

위 두 개 소스는 같은 동작을 한다.

socket.io를 사용하여 소켓 통신을 하는 경우 소켓서버 모듈이 http 위에서 동작하므로 다음과 같이 사용해야 한다.

```javascript
> index3.js

const http = require('http');
const express = require('express');
const socketIO = require('socket.io');
const app = express(); // express instance

const port = process.env.PORT || 3000;

const server = http.createServer(app); // http instance
const io = socketIO(server);

io.on('connection', (socket) => {
    console.log('Socket Connected!');
});

server.listen(port);
```

OR

```javascript
> index4.js

const express = require('express');
const socketIO = require('socket.io');
const app = express(); // express instance

const port = process.env.PORT || 3000;

const server = app.listen(port, () => console.log('SERVER RUN!'));
const io = socketIO(server);

io.on('connection', (socket) => {
    console.log('Socket Connected!');
});
```
