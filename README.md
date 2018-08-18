# o--o

[WIP] A lightweight elegant WebSocket in Node.js

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

### Patterns

#### pub / sub

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

#### req / rep

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
