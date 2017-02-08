# MBTiles Offline

[![Build Status](https://travis-ci.org/DenisCarriere/mbtiles-offline.svg?branch=master)](https://travis-ci.org/DenisCarriere/mbtiles-offline)
[![Coverage Status](https://coveralls.io/repos/github/DenisCarriere/mbtiles-offline/badge.svg?branch=master)](https://coveralls.io/github/DenisCarriere/mbtiles-offline?branch=master)
[![npm version](https://badge.fury.io/js/mbtiles-offline.svg)](https://badge.fury.io/js/mbtiles-offline)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/DenisCarriere/mbtiles-offline/master/LICENSE)

<!-- Line Break -->
[![Standard - JavaScript Style Guide](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

> This library is intented to be used in an offline environment with no dependencies which require the use of downloading a package from the internet.

## NodeJS Support

Windows, MacOSX, Linux & Electron

-   ~~4.X~~
-   ~~5.X~~
-   6.X
-   7.X

## Install

```bash
$ npm install --save mbtiles-offline
```

## Usage

```javascript
const MBTiles = require('mbtiles-offline')
const db = new MBTiles('example.mbtiles')
db.metadata()
    .then(metadata => console.log(metadata))
```

## Features

| Name                  | Description                         |
| --------------------- | :---------------------------------- |
| [metadata](#metadata) | Retrieve Metadata from MBTiles      |
| [update](#update)     | Update Metadata                     |
| [save](#save)         | Save buffer data to individual Tile |
| [delete](#delete)     | Delete individual Tile              |
| [count](#count)       | Count total tiles                   |
| [findOne](#findone)   | Finds one Tile and returns buffer   |
| [findAll](#findall)   | Finds all Tiles                     |
| [tables](#tables)     | Build SQL Tables                    |
| [index](#index)       | Build SQL Index                     |

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### index

MBTiles

#### constructor

MBTiles

**Parameters**

-   `uri` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Path to MBTiles

**Examples**

```javascript
const mbtiles = new MBTiles('example.mbtiles')
//=mbtiles
```

Returns **MBTiles** MBTiles

#### save

Save buffer data to individual Tile

**Parameters**

-   `tile` **Tile** Tile [x, y, z]
-   `image` **[Buffer](https://nodejs.org/api/buffer.html)** Tile image

**Examples**

```javascript
mbtiles.save([x, y, z], buffer)
  .then(status => console.log(status))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)>** 

#### metadata

Retrieves Metadata from MBTiles

**Examples**

```javascript
mbtiles.metadata()
  .then(metadata => console.log(metadata))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;Metadata>** Metadata as an Object

#### delete

Delete individual Tile

**Parameters**

-   `tiles` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Tile>?** Only find given tiles
-   `tile` **Tile** Tile [x, y, z]

**Examples**

```javascript
mbtiles.delete([x, y, z])
  .then(status => console.log(status))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)>** 

#### count

Count the amount of Tiles

**Parameters**

-   `tiles`  

**Examples**

```javascript
mbtiles.count()
  .then(count => console.log(count))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)>** 

#### update

Update Metadata

**Parameters**

-   `metadata` **Metadata?** Metadata according to MBTiles spec 1.1.0 (optional, default `{}`)
    -   `metadata.attribution` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Attribution
    -   `metadata.bounds` **BBox** Bounds [west, south, east, north]
    -   `metadata.center` **Center** Center [lng, lat] or [lng, lat, height]
    -   `metadata.description` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Description
    -   `metadata.format` **Formats** Format 'png' | 'jpg' | 'webp' | 'pbf'
    -   `metadata.minzoom` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** Minimum zoom level
    -   `metadata.maxzoom` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** Maximum zoom level
    -   `metadata.name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Name
    -   `metadata.url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** URL source or tile scheme
    -   `metadata.type` **Types?** Type 'baselayer' | 'overlay' (optional, default `'baselayer'`)
    -   `metadata.version` **Versions?** Version '1.0.0' | '1.1.0' | '1.2.0' (optional, default `'1.1.0'`)

**Examples**

```javascript
const options = {
  name: 'Foo',
  description: 'Bar',
  minzoom: 1,
  maxzoom: 3,
  format: 'png',
  bounds: [-110, -40, 95, 50]
}
mbtiles.update(options)
  .then(metadata => console.log(metadata))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;Metadata>** Metadata

#### findAll

Finds all Tile unique hashes

**Parameters**

-   `tiles` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Tile>?** Only find given tiles

**Examples**

```javascript
const tile1 = [33, 40, 6]
const tile2 = [20, 50, 7]
mbtiles.findAll([tile1, tile2])
  .then(tiles => console.log(tiles))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Tile>>** An array of Tiles [x, y, z]

#### findOne

Finds one Tile and returns Buffer

**Parameters**

-   `tile` **Tile** Tile [x, y, z]

**Examples**

```javascript
mbtiles.findOne([x, y, z])
  .then(image => console.log(image))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[Buffer](https://nodejs.org/api/buffer.html)>** Tile Data

#### tables

Build SQL tables

**Examples**

```javascript
mbtiles.tables()
  .then(status => console.log(status))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)>** 

#### index

Build SQL index

**Examples**

```javascript
mbtiles.index()
  .then(status => console.log(status))
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)>** 

#### hash

Creates hash from a single Tile

**Parameters**

-   `tile` **Tile** 

**Examples**

```javascript
const hash = mbtiles.hash([5, 25, 30])
//=hash
```

Returns **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** hash

#### hashes

Creates a hash table for all tiles

**Parameters**

-   `tiles` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Tile>?** Only find given tiles

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)>** hashes
