# SSL 인증서를 이용한 https 서버 만들기

```javascript
app.js
---
'use strict';

const https = require('https');
const app = require('express')();
const timeout = require('connect-timeout');
const bodyParser = require('body-parser');
const methodOverride = require('method-override');
const compression = require('compression');
const async = require('async');
const morgan = require('morgan');
const log = require('./modules/debug');
const fs = require('fs');
const path = require('path');
const ENV_FILE = path.join(__dirname, '.env');
require('dotenv').config({path: ENV_FILE});

:

const parallel = (middlewares) => {
    return function (req, res, next) {
        async.each(
            middlewares,
            function (mw, cb) {
                mw(req, res, cb);
            },
            next
        );
    };
};

const port = 443;
app.set('port', port);

function onError(error) {
    if (error.syscall !== 'listen') {
        throw error;
    }

    var bind = typeof port === 'string'
        ? 'Pipe ' + port
        : 'Port ' + port;

    // handle specific listen errors with friendly messages
    switch (error.code) {
        case 'EACCES':
            console.error(bind + ' requires elevated privileges');
            process.exit(1);
            break;
        case 'EADDRINUSE':
            console.error(bind + ' is already in use');
            process.exit(1);
            break;
        default:
            throw error;
    }
}

function onListening() {
    var addr = server.address();
    var bind = typeof addr === 'string'
        ? 'pipe ' + addr
        : 'port ' + addr.port;
    log('Listening on ' + bind);
}

app.disable('x-powered-by');
app.use(
    parallel([
        bodyParser.urlencoded({
            extended: true,
            limit: '3mb',
            parameterLimit: 1000000
        }),
        morgan('combined'),
        compression(),
        timeout(10 * 60 * 1000),
        bodyParser.json({
            limit: '3mb'
        }),
        methodOverride(),
        function (req, res, next) {
            var heades = 'X-Requested-With, X-HTTP-Method-Override, Content-Type, Accept';
            res.header('Access-Control-Allow-Origin', '*');
            res.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE,OPTIONS');
            res.header('Access-Control-Allow-Headers', heades);
            next();
        }
    ])
);

const options = {
    ca: fs.readFileSync('./ssl/DigiCertCA.pem'),
    key: fs.readFileSync('./ssl/newkey.pem'),
    cert: fs.readFileSync('./ssl/cert.pem')
};

const server = https.createServer(options, app);

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);

process.on('uncaughtException', error => {
    console.log('uncaughtException:', error);
});


---
```
