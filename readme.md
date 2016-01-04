# koa-xml-body

A xml body parser for koa.

## Install

```bash
npm install --save koa-xml-body
```

## Usage

```js
var koa = require('koa');
var xmlParser = require('koa-xml-body');

var app = koa();
app.use(xmlParser());

app.use(function *() {
    // the parsed body will store in this.request.body
    // if nothing was parsed, body will be undefined
    this.body = this.request.body;
});
```

## Options

- **encoding**: requested encoding. Default is `utf8`. If not set, the lib will retrive it from `content-type`(such as `content-type:application/xml;charset=gb2312`).
- **limit**: limit of the body. If the body ends up being larger than this limit, a 413 error code is returned. Default is `1mb`.
- **length**: length of the body. When `content-length` is found, this will be overwritten by `content-length`.
- **onerror**: error handler. Default is a `noop` function. It means it will **eat** the error and do nothing. You can set it to customize the response.

```js
app.use(xmlParser({
    limit: 128,
    length: 200, // if not sure about the effect, just leave it unspecified
    encoding: 'utf8', // Again, it's better to leave it unspecified. and lib will detect it from `content-type` well
    onerror: (err, ctx) => {
        ctx.throw(err.status, err.message);
    }
}));
```


## Licences

[MIT](LICENSE)