# o--o

[WIP] A lightweight elegant WebSocket in Node.js

## Features

- Support `Pub / Sub` pattern
- Support `Push / Pull` pattern
- Support `Request / Reply` pattern
- Promise based

## Events

- `error` (err) when an un-handled socket error occurs
- `close` when server or connection is closed
- `pub` (...args) when a message publishes
- `sub` (...args) when a message subscription occurs
- `req` (...args) when a message requests
- `rep` (...args) when a message reply occurs

## Usages

**Server.js**

```js
import { Server } from 'o--o';

(async function () {
  try {
    const server = await Server.create(9994);
    server.sub('greeting', (msg) => {
      console.log('received', msg);
    });
  } catch (err) {
    console.errer(err);
  }
}());
```

**Client.js**

```js
import { Client } from 'o--o';

(async function () {
  try {
    const client = await Client.connect(`ws://127.0.0.1:9994`);
    await client.pub('greeting', 'hello');
  } catch (err) {
    console.errer(err);
  }
}());
```

### Pattern: pub / sub

**Server.js**

```js
server.sub('greeting', (msg) => {
  console.log('received', msg);
});
```

**Client.js**

```js
const client = await Client.connect(`ws://127.0.0.1:9994`);
await client.pub('greeting', 'hello');
```

### Pattern: req / rep

**Server.js**

```js
await server.rep('greeting', async (msg) => {
  return msg === 'hello' ? 'world' : 'hi';
});
```

**Client.js**

```js
const client = await Client.connect(`ws://127.0.0.1:9994`);
await client.req('greeting', 'hello');
```

## License

MIT © Cap32
