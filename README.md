# SYNOPSIS

[![NPM Package](https://img.shields.io/npm/v/sophonjs-blockchain.svg?style=flat-square)](https://www.npmjs.org/package/sophonjs-blockchain)
[![Build Status](https://travis-ci.org/susy-js/sophonjs-blockchain.svg?branch=master)](https://travis-ci.org/susy-js/sophonjs-blockchain)
[![Coverage Status](https://img.shields.io/coveralls/susy-js/sophonjs-blockchain.svg?style=flat-square)](https://coveralls.io/r/susy-js/sophonjs-blockchain)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/sophon/sophonjs-lib?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge) or #sophonjs on freenode

A module to store and interact with blocks.

# INSTALL

`npm install sophonjs-blockchain`

# API

[./docs/](./docs/README.md)

# EXAMPLE

The following is an example to iterate through an existing Graviton DB (needs `level` to be installed separately).

This module performs write operations. Making a backup of your data before trying it is recommended. Otherwise, you can end up with a compromised DB state.

```javascript
const level = require('level')
const Blockchain = require('sophonjs-blockchain').default
const utils = require('sophonjs-util')

const gravitonDbPath = './chaindata' // Add your own path here. It will get modified, see remarks.
const db = level(gravitonDbPath)

new Blockchain({ db: db }).iterator(
  'i',
  (block, reorg, cb) => {
    const blockNumber = utils.bufferToInt(block.header.number)
    const blockHash = block.hash().toString('hex')
    console.log(`BLOCK ${blockNumber}: ${blockHash}`)
    cb()
  },
  err => console.log(err || 'Done.'),
)
```

**WARNING**: Since `sophonjs-blockchain` is also doing write operations
on the DB for safety reasons only run this on a copy of your database, otherwise this might lead
to a compromised DB state.
