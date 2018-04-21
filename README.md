![Logo](logo.png)

# botbuilder-redis-storage [![npm version](https://badge.fury.io/js/botbuilder-redis-storage.svg)](https://badge.fury.io/js/botbuilder-redis-storage) [![CircleCI](https://circleci.com/gh/suttna/botbuilder-redis-storage.svg?style=svg)](https://circleci.com/gh/suttna/botbuilder-redis-storage)  [![codecov](https://codecov.io/gh/suttna/botbuilder-redis-storage/branch/master/graph/badge.svg)](https://codecov.io/gh/suttna/botbuilder-redis-storage) [![Gitter](https://badges.gitter.im/suttna/botbuilder-redis-storage.svg)](https://gitter.im/suttna/botbuilder-redis-storage?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Redis storage adapter for Microsoft BotBuilder. This class implements the `IBotStorage` interface.

## Install

```
yarn add botbuilder-redis-storage redis
```

## Usage

The storage depends on a redis client instance.

```javascript
var redis = require('redis')
var RedisStorage = require('botbuilder-redis-storage').RedisStorage
var builder = require('botbuilder')

// Initialize redis client
var redisClient = redis.createClient(process.env.REDIS_URL, { prefix: 'bot-storage:' });

// Create new storage with redis client
var storage = new RedisStorage(redisClient)

var connector = new builder.ChatConnector()
var bot = new builder.UniversalBot(connector)

// Configure bot to use the RedisStorage
bot.set('storage', storage)
```

### TTL for conversations

You can assign a life time for conversations. When enabling this feature, conversations that take longer
than the give TTL will be deleted automatically. Be aware that future interactions with the bot after
starting the conversation won't change the TTL of the conversation. Use this feature with caution.

```javascript
storage.setConversationTTLInSeconds(30 * 60) // 30 minutes
```

## Test

To run the tests:

```
yarn install
yarn test
```

## Contact

- Martín Ferández <martin@suttna.com>
- Santiago Doldán <santiago@suttna.com>
