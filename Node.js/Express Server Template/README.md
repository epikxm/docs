https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html

# 타입스크립트 기반 클래스 형식으로 Express 서버 만들기 (SSL 적용)

```javascript
index.ts
---
import https from "https";
import express from "express";
import fs from "fs";

class Server {
    #ssl_options = {
        ca: fs.readFileSync('./ssl/DigiCertCA.pem'),
        key: fs.readFileSync('./ssl/newkey.pem'),
        cert: fs.readFileSync('./ssl/cert.pem')
    };

    #SSL_PORT = 443;
    #port: number = this.#SSL_PORT;
    #app = express();

    #thisobj: https.Server;

    Port(number: number = this.#SSL_PORT): this {
        this.#port = number;
        return this;
    }

    get httpsObj(): https.Server {
        return this.#thisobj;
    }

    constructor () {
        this.#app.disable("x-powered-by");
        this.#thisobj = https.createServer(this.#ssl_options, this.#app);
    }
}

let server = new Server().Port();
server.httpsObj
server.listen(443);
// console.log(server.httpsObj);
---
```
