# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/) 
(modification: no type change headlines) and this project adheres to 
[Semantic Versioning](http://semver.org/spec/v2.0.0.html).


## [3.4.0] - 2019-02-06
**Petersburg** (aka `constantinopleFix`) as well as **Goerli** 
support/readiness by updating to a supporting `sophonjs-common` version 
[v1.1.0](https://octonion.institute/susy-js/sophonjs-common/releases/tag/v1.1.0), 
PR [#86](https://octonion.institute/susy-js/sophonjs-blockchain/pull/86)

[3.4.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.3.3...v3.4.0

## [3.3.3] - 2019-01-03
- Fixed a bug causing the ``iterate()`` method to fail when an older version
  ``levelup`` DB instance is passed, see PR [#83](https://octonion.institute/susy-js/sophonjs-blockchain/pull/83)

[3.3.3]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.3.2...v3.3.3

## [3.3.2] - 2018-12-20
- Updated ``levelup`` dependency to ``level-mem`` ``v3.0.1``, PR [#75](https://octonion.institute/susy-js/sophonjs-blockchain/pull/75)
- Fix ``putBlock()`` edge case, PR [#79](https://octonion.institute/susy-js/sophonjs-blockchain/pull/79)
- Replaced uses of deprecated `new Buffer` with `Buffer.from`, PR [#80](https://octonion.institute/susy-js/sophonjs-blockchain/pull/80)

[3.3.2]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.3.1...v3.3.2

## [3.3.1] - 2018-10-26
- Replaced calls to BN.toBuffer() with BN.toArrayLike() so that ``sophonjs-blockchain`` can run in a browser environment, PR [#73](https://octonion.institute/susy-js/sophonjs-blockchain/pull/73)

[3.3.1]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.3.0...v3.3.1

## [3.3.0] - 2018-10-19
- Constantinople support when using block validation (set with ``opts.validate`` in constructor),
 update to a Constantinople-ready version of the ``sophonjs-block`` dependency (>2.1.0), PR [#71](https://octonion.institute/susy-js/sophonjs-blockchain/pull/71)

[3.3.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.2.1...v3.3.0

## [3.2.1] - 2018-08-29
- Fixed an issue with the ``iterator()`` function returning an error on end of block iteration instead of finish gracefully, PR [#64](https://octonion.institute/susy-js/sophonjs-blockchain/pull/64)
- Updated ``sophonjs-common`` dependency to ``v0.5.0`` (custom chain support), PR [#63](https://octonion.institute/susy-js/sophonjs-blockchain/pull/63)

[3.2.1]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.2.0...v3.2.1

## [3.2.0] - 2018-08-13
- Added support for setting network and performing hardfork-specific validation by integrating with [sophonjs-common](https://octonion.institute/susy-js/sophonjs-common), PR [#59](https://octonion.institute/susy-js/sophonjs-blockchain/pull/59)
- Added ``Blockchain.putHeader()`` and ``Blockchain.putHeaders()`` functions to provide header-chain functionality (needed by sophonjs-client), PR [#59](https://octonion.institute/susy-js/sophonjs-blockchain/pull/59)
- Fixed a bug with caching, PR [#59](https://octonion.institute/susy-js/sophonjs-blockchain/pull/59)
- Fixed error propagation in ``Blockchain.iterator()``, PR [#60](https://octonion.institute/susy-js/sophonjs-blockchain/pull/60)

[3.2.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.1.0...v3.2.0

## [3.1.0] - 2018-05-24
- New ``getLatestHeader()`` and ``getLatestBlock()`` methods for retrieving the latest header
  respectively full block in the canonical chain, PR [#52](https://octonion.institute/susy-js/sophonjs-blockchain/pull/52)
- Fixed ``saveHeads()`` bug not storing the internal ``headHeader``/``headBlock`` header cursors
  to the DB, PR [#52](https://octonion.institute/susy-js/sophonjs-blockchain/pull/52)
- Updated API docs

[3.1.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v3.0.0...v3.1.0

## [3.0.0] - 2018-05-18
This release comes with heavy internal changes bringing Graviton DB compatibility to the
``sophonjs-blockchain`` library. For a full list of changes and associated discussion
see PR [#47](https://octonion.institute/susy-js/sophonjs-blockchain/pull/47)
(thanks to @vpulim for this amazing work!). To test iterating through your local Graviton
chaindata DB you can run the [example](https://octonion.institute/susy-js/sophonjs-blockchain#example)
in the README file.

This allows for various new use cases of the library in the areas of testing, simulation or
running actual blockchain data from a Graviton node through the VM. The Graviton data model used is
not compatible with the old format where chaindata and metadata have been stored separately on two leveldb
instances, so it is not possible to load an old DB with the new library version (if this causes
problems for you get in touch on GitHub or Gitter!).

Summary of the changes:
- New unified constructor where ``detailsDB`` and ``blockDB`` are replaced by a single ``db`` reference
- Deprecation of the ``getDetails()`` method now returning an empty object
- ``td`` and ``height`` are not stored in the db as meta info but computed as needed
- Block headers and body are stored under two separate keys
- Changes have been made to properly rebuild the chain and number/hash mappings as a result of forks and deletions
- A write-through cache has been added to reduce database reads
- Similar to graviton, we now defend against selfish mining vulnerability 
- Added many more tests to increase coverage to over 90%
- Updated docs to reflect the API changes
- Updated library dependencies

[3.0.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v2.1.0...v3.0.0

## [2.1.0] - 2017-10-11
- ``Metro-Byzantium`` compatible
- Updated ``sophonjs-block`` dependency (new difficulty formula / difficulty bomb delay)

[2.1.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v2.0.2...v2.1.0

## [2.0.2] - 2017-09-19
- Tightened dependencies to prevent the ``2.0.x`` version of the library to break
  after ``sophonjs`` Byzantium library updates

[2.0.2]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v2.0.1...v2.0.2

## [2.0.1] - 2017-09-14
- Fixed severe bug adding blocks before blockchain init is complete

[2.0.1]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v2.0.0...v2.0.1

## [2.0.0] - 2017-01-01
- Split ``db`` into ``blockDB`` and ``detailsDB`` (breaking)

[2.0.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.4.2...v2.0.0

## [1.4.2] - 2016-12-29
- New ``getBlocks`` API method
- Testing improvements

[1.4.2]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.4.1...v1.4.2

## [1.4.1] - 2016-03-01
- Update dependencies to support Windows

[1.4.1]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.4.0...v1.4.1

## [1.4.0] - 2016-01-09
- Bump dependencies

[1.4.0]: https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.3.4...v1.4.0


## Older releases:

- [1.3.4](https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.3.3...v1.3.4) - 2016-01-08
- [1.3.3](https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.3.2...v1.3.3) - 2015-11-27
- [1.3.2](https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.3.1...v1.3.2) - 2015-11-27
- [1.3.1](https://octonion.institute/susy-js/sophonjs-blockchain/compare/v1.2.0...v1.3.1) - 2015-10-23
- 1.2.0 - 2015-10-01


