
# request v1.0.0 ![stable](https://img.shields.io/badge/stability-stable-4EBA0F.svg?style=flat)

```sh
npm install aleclarson/request#1.0.0
```

## Usage

```js
const request = require('request')

request(url, config).then(res => {
  console.log(res.status + ' ' + res.text)
})
```

The response object has these properties:
- `success: Boolean` <= Equals `true` if the `status` is `2xx`
- `status: Number`
- `headers: Object`
- `data: Buffer`
- `text: String` <= Derived from `data` on access
- `json: Object` <= Derived from `data` on access

## Configuration

The following options are defined using the `config` object:

### method

The HTTP method of the request. Must be a string.

Defaults to `POST` if `config.data` is defined, else `GET`.

### headers

An object containing the request headers.

The keys are not altered, so use `Content-Type` instead of `content-type` in case the server is picky.

### query

An object that is converted into a querystring and appended to the url.

A string is also allowed, but leave out the leading `?`.

### data

A string, object, or buffer that is sent with the request.

An object will be converted using `JSON.stringify`.

The data is sent all at once, not streamed.

### contentType

A string that overwrites `headers['Content-Type']` for convenience.

Possible values include:
- `json` => `application/json`
- `form` => `application/x-www-form-urlencoded; charset=utf-8`
- `text` => `text/plain; charset=utf-8`
- `binary` => `application/octet-stream`

You must define `headers['Content-Type']` if you're using another content type.

When set to `form`, the `data` object is converted into a string using the [`form-urlencoded`](https://github.com/aleclarson/form-urlencoded) package.

### stream

When `true`, the request promise will resolve into the raw response stream, instead of wrapping it with a response object.

The response stream is an `IncomingMessage` instance. [Learn more here.](https://nodejs.org/api/http.html#http_class_http_incomingmessage)

### socket

A string that defines the UNIX socket path.

When defined, the `url` string does not need the protocol or hostname, only the pathname.

### ssl

An object containing TLS options like:
- `ca`
- `cert`
- `ciphers`
- `key`
- `passphrase`
- `pfx`
- `rejectUnauthorized`
- `secureProtocol`
- `servername`

[Learn more here.](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback)
