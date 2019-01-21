# SSL-
Quickly generate HTTPS certificate for local development 

1. Clone this repository and `cd` into it:
2. Run the script to create a root certificate:
sh createRootCA.sh
3. Run the script to create a domain certificate for `localhost`: 
sh createSelfSigned.sh
4. Move `server.key` and `server.crt` to an accessible location on your server and include them when starting it. In an Express app running on Node.js, you'd do something like this:

```js
var path = require('path')
var fs = require('fs')
var express = require('express')
var https = require('https')

var certOptions = {
  key: fs.readFileSync(path.resolve('build/cert/server.key')),
  cert: fs.readFileSync(path.resolve('build/cert/server.crt'))
}

var app = express()

var server = https.createServer(certOptions, app).listen(443)

