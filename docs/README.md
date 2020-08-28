# Quickstart 

Welcome to the SPOO Documentation Site. Here you'll find the docs for the SPOO framework as well as for the JS Client SDK and REST API.
The following quick examples show you how to spin up a platform and a client with just a few lines of code.

> For running a basic platform you will need ***Node.js***, ***Redis*** and ***MongoDB***

# Spin up a Platform

```shell
npm i spoojs
```

```javascript
// 1. import spoo
const SPOO = require('spoojs');

// 2. define some "object wrappers"
SPOO.OBJY.define({
  name: "user",
  pluralName: "users",
  authable: true
})

SPOO.OBJY.define({
  name: "object",
  pluralName: "objects"
})

// 3. run the platform via REST
SPOO.REST({
  port:80,
  metaMapper: new SPOO.metaMappers.mongoMapper().connect("mongodb://localhost") // The matamapper is for basic config
}).run()
```

# Set up a Client (SDK)

> Install via npm or script tag:

```html
<script src="spoo.js">
```
or
```shell
npm i spoo-client
```

```javascript
// 1. Initialize the client
const spoo = new SPOO_Client('mytenant');

// 2. Authenticate a user
spoo.io().auth("user", "pass", function(data, err){
  if(!err) console.log('you are in!');
})

// Add an object
spoo.io().object({
  name: "Mercedes",
  type: "car",
  properties: {
    owner : {
      type: "shortText",
      value: "Peter Griffin"
    }
  }
}).add(function(data, err)
{
  if(err) return console.error(err);
  console.log(data); // {...object...}
})

// Modify an object
spoo.io().object("objectid...").addProperty({
  color: {
    type: "shortText",
    value: "red"
  }
}).save(function(data, err)
{
  if(err) return console.error(err);
  console.log(data); // {...updated object...}
})
```


## Authors

* **Marco Boelling** - *Initial work* - [Twitter](https://twitter.com/marcoboelling)


## License

SPOO is open source and licensed under the AGPL license.

## Further reading

* For more information on SPOO, go to [spoo.io](https://spoo.io)

