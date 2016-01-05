# Screeps Perf

This is a drop in module for the game of [Screeps](https://www.screeps.com).  It helps to reduce CPU usage by monkey patching some of the built in prototypes to: make use of more efficient loops, cache expensive method calls, and clean up some redundant memory.

## Setup

You have two options for installing this script. You can either use npm and a compiler like webpack, or you can copy/paste the `screeps-perf.js` file and use the provided screeps require function.

## Usage

Just drop it into main.js, and call the exported function:

```javascript
require('screeps-perf')();
// ... other require statements

module.exports.loop = function() {
  // Game logic
};
```

It's best if this library is the first thing imported into your scripts.  This is because it adjusts some functions that your other scripts might use to be more performant.

## Options

You can disable any part of the performance module, by passing a config to the first use of the require statement.  All features are optional, but default to true.

```javascript
// Turn off any of the below features by passing false.
require('screeps-perf')({
  speedUpArrayFunctions: true,
  cleanUpCreepMemory: true,
  optimizePathFinding: true
});
```

## Accessing the original Room.prototype.findPath

It isn't always ideal to use cached paths, as they can be less than optimal depending on the layout of the room when they were generated.  For this reason, the performance module exports the original findPath function.  If you want to not use the cached path, you'll need to hook up the originalFindPath yourself.

```javascript
var perf = require('screeps-perf')();
var findPath = perf.originalFindPath;
```
