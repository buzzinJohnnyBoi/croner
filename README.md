# Croner

[![Build status](https://travis-ci.org/Hexagon/croner.svg)](https://travis-ci.org/Hexagon/croner) [![npm version](https://badge.fury.io/js/croner.svg)](https://badge.fury.io/js/croner) [![Codacy Badge](https://app.codacy.com/project/badge/Grade/4978bdbf495941c087ecb32b120f28ff)](https://www.codacy.com/gh/Hexagon/croner/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Hexagon/croner&amp;utm_campaign=Badge_Grade)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](https://img.shields.io/badge/license-MIT-blue.svg)

Pure JavaScript minimal isomorphic cron parser and scheduler. Or simply speaking - setInterval on steroids. 

Supports Node.js, requirejs, es-module and stand alone usage. 

Documented with JSDoc for intellisense, and complete TypeScript typings for type checking.

```html
<script src="//cdn.56k.guru/js/croner/latest/croner.min.js"></script>
```

```javascript
// Run a function each second
Cron('* * * * * *', function () {
	console.log('This will run every second');
});
```


# Installation

## Node.js

```npm install croner```


## CDN

Copy and paste one of the following script tags.

**Minified normal module (umd)**

```html
<script src="//cdn.56k.guru/js/croner/latest/croner.min.js"></script>
```

**Minified ESM-module**

See usage-section for more examples, including ESM usage.


## Manual (server/client)

 * Download latest [zipball](http://github.com/Hexagon/croner/zipball/master/)
 * Unpack
 * Grab croner.min.js or croner.min.mjs from the [dist/](/dist) folder



# Usage

## Node.js/CommonJS

```javascript
var Cron = require('croner');

Cron('* * * * * *', function () {
	console.log('This will run every second');
});
```

## Browser ESM

Import croner.min.mjs from cdn or manually, see installation section above.

```html
<script type="module">
import Cron from 'https://cdn.jsdelivr.net/npm/croner@1.1.27/dist/croner.min.mjs';

Cron('* * * * * *', () => {
	console.log('This will run every second');
});
</script>
```

## Browser ESM with import-maps

Import croner.min.mjs from cdn or manually, see installation section above.

```html
<script type="importmap">
{
  "imports": {
    "croner": "https://cdn.jsdelivr.net/npm/croner@1.1.27/dist/croner.min.mjs"
  }
}
</script>
<script type="module">
import Cron from 'croner';

Cron('* * * * * *', () => {
	console.log('This will run every second');
});
</script>
```

## Browser, stand-alone

Include croner.min.js fron cdn or manually, see installation section above. Croner registers itself globally as 'Cron'.

```javascript
// Run a function each second
Cron('* * * * * *', function () {
	console.log('This will run every second');
});
```

## Browser, require.js

Include croner.min.js in your preferred way, it will register itself as a require.js module.

```javascript
define(["croner"], function(Cron) {

	Cron('* * * * * *', function () {
		console.log('This will run every second');
	});

});
```


# Examples 

## Minimalist scheduling
```javascript
// Run a function each second
Cron('* * * * * *', function () {
	console.log('This will run every second');
});
```

## Minimalist scheduling with stepping
```javascript
// Run a function every fifth second
Cron('*/5 * * * * *', function () {
	console.log('This will run every fifth second');
});
```

## Minimalist scheduling with range
```javascript
// Run a function the first five seconds of a minute
Cron('0-4 * * * * *', function () {
	console.log('This will run the first five seconds every minute');
});
```

## Minimalist scheduling with options
```javascript
// Run a function each second, limit to five runs
Cron('* * * * * *', { maxRuns: 5 }, function () {
	console.log('This will run each second, but only five times.');
});
```

## Minimalist scheduling with controls
```javascript
// Run a function each second, get reference to job
var job = Cron('* * * * * *', function () {
	console.log('This will run each second.');
});

// Pause job
job.pause();

// Resume job
job.resume();

// Stop job
job.stop();

```

## Basic scheduling
```javascript

// Run every minute
var scheduler = Cron('0 * * * * *');

scheduler.schedule(function() {
	console.log('This will run every minute');
});
```

## Scheduling with options
```javascript

// Run every minute
var scheduler = Cron('0 * * * * *');

// Schedule with options (all options are optional)
scheduler.schedule({ maxRuns: 5 }, function() {
	console.log('This will run every minute.');
});
```
## Scheduling with controls
```javascript

// Run every minute
var scheduler = Cron('0 * * * * *');

// Schedule with options (all options are optional)
var job = scheduler.schedule({ maxRuns: 5 }, function() {
	console.log('This will run every minute.');
});

// Pause job
job.pause();

// Resume job
job.resume();

// Stop job
job.stop();
```

# Full API
```javascript

var o = Cron( <string pattern> [, <object options>] [, <function callback> ] );

// If Cron is initialized without a scheduled function, cron itself is returned
// and the following member functions is available.
o.next( [ <date previous> ] );
o.msToNext();

// If Cron is initialized _with_ a scheduled function, the job is retured instead.
// Otherwise you get a reference to the job when scheduling a new job.
var job = o.schedule( [ { startAt: <date>, stopAt: <date>, maxRuns: <integer> } ,] callback);

// These self-explanatory functions is available to control the job
job.pause();
job.resume();
job.stop();

```


# Pattern

```
┌──────────────── second (0 - 59)
│ ┌────────────── minute (0 - 59)
│ │ ┌──────────── hour (0 - 23)
│ │ │ ┌────────── day of month (1 - 31)
│ │ │ │ ┌──────── month (1 - 12)
│ │ │ │ │ ┌────── day of week (0 - 6) 
│ │ │ │ │ │       (0 to 6 are Sunday to Saturday; 7 is Sunday, the same as 0)
│ │ │ │ │ │
* * * * * *
```



# License

MIT
