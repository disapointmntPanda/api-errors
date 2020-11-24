# api-errors

A zero dependency tiny module to handle HTTP errors which extends nodejs error.

## Install

This is a [Node.js](https://nodejs.org/en/) module available through the
[npm registry](https://www.npmjs.com/). Installation is done using the
[`npm install` command](https://docs.npmjs.com/getting-started/installing-npm-packages-locally):

## Example

```js
const { AccessDeniedError } createError = require('api-errors')
var express = require('express')
var app = express()

app.use(function (req, res, next) {
  if (!req.user) return next(new AccessDeniedError('Please login to view this page.')) // message is optional
  next()
})

app.use(function(err, req, res, next) {
  // catch all else api errors
  if (error instanceof APIError) {
    return res
      .status(error.status)
      .send({
        status: false,
        message: error.message,
      });
  }
})

```

## API

This is the current API, currently extracted from Koa and subject to change.

#### List of all constructors

| Status Code | Constructor Name          |
| ----------- | ------------------------- |
| 400         | BadRequestError           |
| 401         | UnauthorizedError         |
| 403         | ForbiddenError            |
| 404         | NotFoundError             |
| 405         | MethodNotAllowedError     |
| 409         | ConflictError             |
| 412         | PreconditionFailedError   |
| 415         | UnsupportedMediaTypeError |
| 422         | UnprocessableEntityError  |
| 500         | InternalServerError       |

## License

[MIT](LICENSE)
