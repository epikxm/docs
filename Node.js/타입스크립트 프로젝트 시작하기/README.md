# 타입스크립트 프로젝트 시작하기

Node.js 프로젝트에 Typescript를 사용하는 경우에 대한 설명이다.

## 프로젝트 시작

**폴더 구조**

```javascript
[project: /]
    > dist
    > node_modules
    > src
        app.ts
    package.json
    tsconfig.json
```

## Typescript & 관련 모듈 설치

Typescript 미설치시 글로벌로 설치한다.

```javascript
> npm i -g typescript
```

다음 모듈을 추가한다.

```javascript
> yarn add @types/node
> yarn add -D ts-node tsc-watch [typescript]
```

**@types/node** Node.js에서 type 정의를 포함하고 있는 패키지  
**ts-node** Typescript를 실행시키는 엔진 (개발환경에서만 사용하려면 -D 옵션을 주고 설치한다.)  
**tsc-watch** .ts 코드가 변경되면 자동으로 컴파일한 뒤 js로 실행

## Typescript 환경 설정(tsconfig.json 생성)

```javascript
> tsc --init --rootDir src --outDir ./dist --esModuleInterop --lib ES2020 --module commonjs --noImplicitAny true
```

## tsconfig.json 수정

```javascript
{
  "compilerOptions": {
    ...
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

## package.json 수정

```javascript
  "scripts": {
    "start": "tsc-watch --onSuccess \"ts-node dist/app.js\" "
  }
```

## 실행

```javascript
> yarn start
```

> .ts 소스가 수정되면 즉시 컴파일되어 ts-node ./dist/app.js 를 수행한다.
