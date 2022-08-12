https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html

# 타입스크립트 기반 클래스 형식으로 Express 서버 만들기 (SSL 적용)

```javascript
index.ts
---
import https from "https";
import express, { Application, Request, Response, NextFunction } from "express";
import fs from "fs";
import { hrtime } from "process";

class Server {
    #ssl_options = {
        ca: fs.readFileSync('./ssl/DigiCertCA.pem'),
        key: fs.readFileSync('./ssl/newkey.pem'),
        cert: fs.readFileSync('./ssl/cert.pem')
    };

    #SSL_PORT = 443;
    #port: number = this.#SSL_PORT;
    app: Application = express();


    Port(number: number = this.#SSL_PORT): this {
        this.#port = number;
        return this;
    }

    constructor () {
        this.app = express();
        this.#config();
    }

    #config = (): void => {
        this.app.disable("x-powered-by");
        this.app.use((req: Request, res: Response, next: NextFunction) => {
            res.header('Access-Control-Allow-Origin', '*');
        });
    }
}

let server = new Server().Port();
---
```
