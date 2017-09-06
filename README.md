# Discord RPC Client

#### Official RPC extension for [Discord.js](https://discord.js.org), and all types used in this library are from Discord.js

```js
const { Client } = require('discord-rpc');

const clientID = '187406016902594560';
const scopes = ['rpc', 'rpc.api', 'messages.read'];

// This demonstrates discord's implicit oauth2 flow
// http://discordapi.com/topics/oauth2#implicit-grant

const params = new URLSearchParams(document.location.hash.slice(1));

if (!params.has('access_token')) {
  // Redirect to discord to get an access token
  document.location.href =
    `https://discordapp.com/oauth2/authorize?response_type=token&client_id=${clientID}&scope=${scopes.join('%20')}`;
}

const client = new Client({ transport: 'websocket' });

client.on('ready', () => {
  console.log('Logged in as', client.application.name);
  console.log('Authed for user', client.user.tag);
});

// Log in to RPC with client id and access token
client.login(clientID, { accessToken: params.get('access_token') });
```
