# DCAS API

Browser and node module for making API requests against [DCAS API]().

**Please note: This module uses [Popsicle](https://github.com/blakeembrey/popsicle) to make API requests. Promises must be supported or polyfilled on all target environments.**

## Installation

```
npm install dcas-api --save
bower install dcas-api --save
```

## Usage

### Node

```javascript
var DcasApi = require('dcas-api');

var client = new DcasApi();
```

### Browsers

```html
<script src="dcas-api/index.js"></script>

<script>
  var client = new DcasApi();
</script>
```

### Options

You can set options when you initialize a client or at any time with the `options` property. You may also override options for a single request by passing an object as the second argument of any request method. For example:

```javascript
var client = new DcasApi({ ... });

client.options = { ... };

client.resource('/').get(null, {
  baseUri: 'http://example.com',
  headers: {
    'Content-Type': 'application/json'
  }
});
```

#### Base URI

You can override the base URI by setting the `baseUri` property, or initializing a client with a base URI. For example:

```javascript
new DcasApi({
  baseUri: 'https://example.com'
});
```

#### Base URI Parameters

If the base URI has parameters inline, you can set them by updating the `baseUriParameters` property. For example:

```javascript
client.options.baseUriParameters.version = 'v1';
```

### Resources

All methods return a HTTP request instance of [Popsicle](https://github.com/blakeembrey/popsicle), which allows the use of promises (and streaming in node).

#### resources.user

```js
var resource = client.resources.user;
```

##### GET

```js
resource.get().then(function (res) { ... });
```

##### POST

```js
resource.post().then(function (res) { ... });
```

##### Body

**application/json**

```
{  "$schema": "http://json-schema.org/draft-03/schema",
   "type": "object",
   "description": "A single User",
   "properties": {
     "id":  { "type": "string", "required": true },
     "name":  { "type": "string", "required": true },
     "age":  { "type": "integer" }
   }
}

```

##### DELETE

```js
resource.delete().then(function (res) { ... });
```

#### resources.user.userId(userId)

* **userId** _string_

```js
var resource = client.resources.user.userId(userId);
```

##### GET

```js
resource.get().then(function (res) { ... });
```

##### PUT

```js
resource.put().then(function (res) { ... });
```

##### Body

**application/json**

```
{  "$schema": "http://json-schema.org/draft-03/schema",
   "type": "object",
   "description": "A single User",
   "properties": {
     "id":  { "type": "string", "required": true },
     "name":  { "type": "string", "required": true },
     "age":  { "type": "integer" }
   }
}

```

##### DELETE

```js
resource.delete().then(function (res) { ... });
```



### Custom Resources

You can make requests to a custom path in the API using the `#resource(path)` method.

```javascript
client.resource('/example/path').get();
```

## License

Apache 2.0
