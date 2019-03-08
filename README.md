# single-user-cache

[![Build Status](https://travis-ci.com/mcollina/single-user-cache.svg?branch=master)](https://travis-ci.com/mcollina/single-user-cache)

A simple cache system for a single user request, built on the same concepts of [data loader](https://github.com/facebook/dataloader).

## Install

```js
npm i single-user-cache
```

## Usage

```js
const { Factory } = require('.')
const factory = new Factory()

factory.add('fetchSomething', async (queries) => {
  console.log(queries)
  // [ 42, 24 ]

  return queries.map((k) => {
    return { k }
  })
})

async function run () {
  const cache = factory.create()

  const p1 = cache.fetchSomething(42)
  const p2 = cache.fetchSomething(24)

  const res = await Promise.all([p1, p2])

  console.log(res)
  // [
  //   { k: 42 },
  //   { k: 24 }
  // ]
}

run().catch(console.log)
```

## License

MIT