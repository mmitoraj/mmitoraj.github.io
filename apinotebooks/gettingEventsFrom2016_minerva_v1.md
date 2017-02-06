---
id: gettingEventsFrom2016_minerva_v1
interactive: true
type: Tutorial
title: 'Getting conference events for 2016'
service: 'Minerva'
---


Minerva service exposes its API contract using RAML specification. Thanks to it, you can generate a JavaScript client that you will later use in your code.
This is what is done in this tutorial, first you create a REST client and then you make proper API calls using it

```javascript
API.createClient('minervaService',
'http://derberg.github.io/services/minerva/v1/api.raml');
```

To get from the server only conference events from 2016 you need to request data with a proper query parameter.
The `type` attribute defines if it is a conference that will take place in 2016.

```javascript
confEvents = minervaService.events.get(null, {
  query: {
    'q': 'type:"Conference 2016"'
  }
})
```

Now once you have the list, grab it with some code

```javascript
confEvents = confEvents.body;
```


Now extract only conferences that will occure in Poland.

```javascript
confsInPoland = [];

confEvents.forEach(function(conf){

  if(conf.address.indexOf('Poland') !== -1) {

    confsInPoland.push(conf);
  }
})

confsInPoland;
```