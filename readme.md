The Pirate Bay node.js client
=============================
[![Build Status](https://travis-ci.org/t3chnoboy/thepiratebay.svg?branch=master)](https://travis-ci.org/t3chnoboy/thepiratebay)
[![NPM version](https://badge.fury.io/js/thepiratebay.svg)](http://badge.fury.io/js/thepiratebay)
[![Dependency Status](https://gemnasium.com/t3chnoboy/thepiratebay.svg)](https://gemnasium.com/t3chnoboy/thepiratebay)
[![npm](https://img.shields.io/npm/dm/thepiratebay.svg?maxAge=2592000)]()

<p align="center">
  <img src="https://i.imgur.com/xP3s8Xum.png"/>
</p>

## Installation

Install using npm:
```bash
npm install thepiratebay --save
```

## Usage

```javascript
  const PirateBay = require('thepiratebay')
```
All methods are asynchronous!
You can use promises, ES6 generators, or async/await

Using promises:
```javascript
  PirateBay.search('Game of Thrones', {
  	category: 205
  })
  .then(function(results) {
  	console.log(results)
  })
  .catch(function(err) {
  	console.log(err)
  })
```

Using ES7 async/await
```javascript
async search() {
  const searchResults = await PirateBay.search({
    category: 205,
    page: 3,
    orderBy: 'seeds',
    sortBy: 'desc',
  })
  console.log(searchResults)
}
```

## Methods

### search
```javascript
  // Takes a search query and options
  PirateBay.search('Game of Thrones', {
    category: 0,        // default - `/search/0/99/{category}`
    filter: {
      verified: true    // default - Filter all VIP or trusted torrents
    },
    page: 0,            // default - 0 - 99
    orderBy: 'leeches', // default - name, date, size, seeds, leeches
    sortBy: 'desc'      // default - desc, asc
  })

/* returns an array of search results:
[
  {
    name: 'Game of Thrones (2014)(dvd5) Season 4 DVD 1 SAM TBS',
    size: '4.17 GiB',
    link: 'http://thepiratebay.se/torrent/10013794/Game_of_Thron...'
    category: { id: '200', name: 'Video' },
    seeders: '125',
    leechers: '552',
    uploadDate: 'Today 00:57',
    magnetLink: 'magnet:?xt=urn:btih:4e6a2304fed5841c04b16d61a0ba...
    subcategory: { id: '202', name: 'Movies DVDR' }
  },
  ...
]
*/
```

### getTorrent
```javascript
  // takes an id or a link
  PirateBay
    .getTorrent('10676856')
    .then(function(results) {
      console.log(results)
    })
    .catch(function(error) {
      console.log(error)
    })

/*
output:
  {
    name: 'The Amazing Spider-Man 2 (2014) 1080p BrRip x264 - YIFY',
    filesCount: 2,
    size: '2.06 GiB (2209149731 Bytes)',
    seeders: '14142',
    leechers: '3140',
    uploadDate: '2014-08-02 08:15:25 GMT',
    magnetLink: 'magnet:?xt=urn:btih:025....
    link: 'http://thepiratebay.se/torrent/10676856/',
    id: '10676856',
    description: 'I've always known that Spider-Man...'
  }
*/
```

### topTorrents
```javascript
  // returns top 100 torrents
  PirateBay.topTorrents()

  // returns top 100 torrents for the category '400' aka Games
  PirateBay.topTorrents(400)
```

### recentTorrents
```javascript
  // returns the most recent torrents
  PirateBay.recentTorrents()
```

### userTorrents
```javascript
  // Gets a specific user's torrents
  PirateBay.userTorrents('YIFY', {
    page: 3,
    orderBy: 'name',
    sortBy: 'asc'
  })
```

### getCategories
```javascript
  // Gets all available categories on piratebay
  PirateBay.getCategories()

/*
[
  { name: 'Video',
    id: '200',
    subcategories:
     [ { id: '201', name: 'Movies' },
       { id: '202', name: 'Movies DVDR' },
       { id: '203', name: 'Music videos' },
       { id: '204', name: 'Movie clips' },
       { id: '205', name: 'TV shows' },
       { id: '206', name: 'Handheld' },
       { id: '207', name: 'HD - Movies' },
       { id: '208', name: 'HD - TV shows' },
       { id: '209', name: '3D' },
       { id: '299', name: 'Other' } ]
     }
  ...
]
*/
```
