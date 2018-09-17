[![ioredis](https://cdn.rawgit.com/luin/ioredis/57b5b89e3e9111ff25d8c62c0bc58ed42e5b8d1e/logo.svg)](https://github.com/luin/ioredis)

[![Build Status](https://travis-ci.org/luin/ioredis.svg?branch=master)](https://travis-ci.org/luin/ioredis)
[![Test Coverage](https://codeclimate.com/github/luin/ioredis/badges/coverage.svg)](https://codeclimate.com/github/luin/ioredis)
[![Code Climate](https://codeclimate.com/github/luin/ioredis/badges/gpa.svg)](https://codeclimate.com/github/luin/ioredis)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![Join the chat at https://gitter.im/luin/ioredis](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/luin/ioredis?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[Node.js를](https://nodejs.org/) 위한 강력하고 성능 중심의 완전한 기능을 갖춘 [Redis](http://redis.io/) 클라이언트 .

Redis> 2.6.12 및 (Node.js> = 6)을 지원합니다.

# Features
ioredis는 세계 최대의 온라인 상거래 회사 인 [Alibaba](http://www.alibaba.com/) 및 다른 많은 훌륭한 회사 에서 사용되는 강력하고 완벽한 기능을 갖춘 Redis 클라이언트입니다 .

1. 모든 기능을 갖춘. 그것은 지원 [클러스터](http://redis.io/topics/cluster-tutorial) , [센티넬](http://redis.io/topics/sentinel) , [파이프 라이닝](http://redis.io/topics/pipelining) 물론 [루아 스크립트](http://redis.io/commands/eval) & [펍 / 하위](http://redis.io/topics/pubsub) (바이너리 메시지의 지원을).
2. 고성능.
3. 유쾌한 API. 노드 콜백 및 기본 약속과 함께 작동합니다.
4. 명령 인수와 응답의 변환.
5. 투명한 키 접두사.
6. 루아 스크립팅을위한 추상화로 커스텀 커맨드를 정의 할 수 있습니다.
7. 바이너리 데이터 지원.
8. TLS 지원.
9. 오프라인 대기열 및 준비 확인 지원.
10. 같은 ES6 유형에 대한 지원 `Map`과 `Set`.
11. GEO 명령 지원 (Redis 3.2 Unstable).
12. 정교한 오류 처리 전략.

# Links
- [API 문서](https://github.com/luin/ioredis/blob/master/API.md)
- [변경 로그](https://github.com/luin/ioredis/blob/master/Changelog.md)
- [node_redis에서 마이그레이션](https://github.com/luin/ioredis/wiki/Migrating-from-node_redis)
- [오류 처리](https://github.com/luin/ioredis#error-handling)

## Become a Sponsor to Support ioredis's Development(ioredis의 개발을 지원하기위한 스폰서)
오픈 소스는 어렵고 시간이 많이 걸립니다. ioredis의 미래에 투자하고 싶다면 스폰서가되어이 도서관의 개선점과 새로운 기능에 더 많은 시간을 할애 할 수 있습니다.

<a href="https://opencollective.com/ioredis"><img src="https://opencollective.com/ioredis/tiers/sponsor.svg?avatarHeight=36"></a>

ioredis를 사용해 주셔서 감사합니다 :-)

<hr>
<a href="https://itunes.apple.com/app/medis-gui-for-redis/id1063631769"><img align="right" src="medis.png" alt="Download on the App Store"></a>


### Advertisement(광고)

OS X, Windows 및 Linux 용 Redis GUI 관리자를 찾으십니까? 여기 [메디스가 있습니다](https://itunes.apple.com/us/app/medis-gui-for-redis/id1063631769) !

Medis는 오픈 소스이며, 아름답고 사용하기 쉬운 Redis GUI 관리 응용 프로그램입니다.

Medis는 필요한 기본 기능부터 시작합니다.

- 키보기 / 편집
- 원격 서버와의 연결을위한 SSH 터널
- 사용자 지정 명령을 실행하기위한 터미널
- JSON / MessagePack 형식보기 / 편집 및 내장 된 강조 표시 / 유효성 검사기
- 그리고 다른 멋진 기능 ...

[Medis는 GitHub에서 오픈 소스입니다.](https://github.com/luin/medis)https://github.com/luin/ioredis#error-handling)

<hr>

# Quick Start

## Install
```shell
$ npm install ioredis
```

## Basic Usage

```javascript
var Redis = require('ioredis');
var redis = new Redis();

redis.set('foo', 'bar');
redis.get('foo', function (err, result) {
  console.log(result);
});

// 또는 마지막 인수가 함수가 아닌 경우 약속을 사용합니다.
redis.get('foo').then(function (result) {
  console.log(result);
});

// 명령에 대한 인수는 병합되므로 다음과 동일합니다:
redis.sadd('set', 1, 3, 5, 7);
redis.sadd('set', [1, 3, 5, 7]);

// 모든 인수는 redis 서버로 직접 전달됩니다:
redis.set('key', 100, 'EX', 10);
```

See the `examples/` folder for more examples.

## Connect to Redis
새 `Redis`인스턴스가 만들어 지면 Redis와의 연결이 동시에 생성됩니다. 연결할 Redis를 다음과 같이 지정할 수 있습니다.

```javascript
new Redis()       // Connect to 127.0.0.1:6379
new Redis(6380)   // 127.0.0.1:6380
new Redis(6379, '192.168.1.1')        // 192.168.1.1:6379
new Redis('/tmp/redis.sock')
new Redis({
  port: 6379,          // Redis port
  host: '127.0.0.1',   // Redis host
  family: 4,           // 4 (IPv4) or 6 (IPv6)
  password: 'auth',
  db: 0
})
```

연결 옵션을 [`redis://` URL](http://www.iana.org/assignments/uri-schemes/prov/redis) 로 지정할 수도 있습니다.:

```javascript
// 암호 "authpassword"를 사용하여 127.0.0.1:6380, db 4에 연결합니다. 
new Redis('redis://:authpassword@127.0.0.1:6380/4')
```

사용 가능한 모든 옵션에 대해서는 [API Documentation](API.md#new_Redis) 를 참조하십시오.

## Pub/Sub

다음은 게시 / 구독 용 API의 간단한 예입니다. 다음 프로그램은 두 개의 클라이언트 연결을 엽니 다. 하나의 연결로 채널을 구독하고 다른 채널로 해당 채널에 게시합니다:

```javascript
var Redis = require('ioredis');
var redis = new Redis();
var pub = new Redis();
redis.subscribe('news', 'music', function (err, count) {
  // 'news'와 'music'채널에 모두 가입했습니다 
  // 'count'는 현재 구독중인 채널의 수를 나타냅니다.

  pub.publish('news', 'Hello world!');
  pub.publish('music', 'Hello again!');
});

redis.on('message', function (channel, message) {
  // Receive message Hello world! from channel news
  // Receive message Hello again! from channel music
  console.log('Receive message %s from channel %s', message, channel);
});

// 또한 'messageBuffer'라는 이벤트가 있는데, 이는 'message'와 동일하지만 
// 문자열 대신 버퍼를 반환합니다. 
redis.on('messageBuffer', function (channel, message) {
// `channel`과`message` 둘 다 버퍼입니다. 
});
```

`PSUBSCRIBE` 유사한 방식으로 지원됩니다:

```javascript
redis.psubscribe('pat?ern', function (err, count) {});
redis.on('pmessage', function (pattern, channel, message) {});
redis.on('pmessageBuffer', function (pattern, channel, message) {});
```

클라이언트가 SUBSCRIBE 또는 PSUBSCRIBE를 발행하면 해당 연결은 "구독자"모드가됩니다. 이 시점에서 서브 스크립 션 세트를 수정하는 명령 만 유효합니다. 서브 스크립 션 세트가 비어 있으면 연결이 일반 모드로 되돌아갑니다.

가입자 모드에서 Redis에 정규 명령을 보내야하는 경우 다른 연결을여십시오.

## Handle Binary Data(이진 데이터 처리)
인수는 버퍼 일 수 있습니다:
```javascript
redis.set('foo', Buffer.from('bar'));
```

그리고 모든 명령에는 Buffer를 반환하는 메서드가 있습니다 (명령 이름에 "Buffer"접미사를 추가 함). utf8 문자열 대신 버퍼를 얻으려면:

```javascript
redis.getBuffer('foo', function (err, result) {
  // result is a buffer.
});
```

## Pipelining
일괄 명령 (예 :> 5)을 보내려는 경우 파이프 라이닝을 사용하여 명령을 메모리에 대기시킨 다음이를 즉시 Redis로 보냅니다. 이렇게하면 성능이 50 % ~ 300 % 향상됩니다
(See [benchmark section](#benchmark)).

`redis.pipeline()` Pipeline 인스턴스를 만듭니다. `Redis`인스턴스 와 마찬가지로 Redis 명령을 호출 할 수 있습니다. 
명령은 메모리에 대기하고 다음 `exec`메소드 를 호출하여 Redis로 플러시됩니다.

```javascript
var pipeline = redis.pipeline();
pipeline.set('foo', 'bar');
pipeline.del('cc');
pipeline.exec(function (err, results) {
   // 'err` 항상 널과`results`는 응답의 배열 인 
   // 대기 명령의 시퀀스에 대응. 
   // 각 응답의 포맷을'다음 [ERR, 결과] `.
});

// 명령을 연결할 수도 있습니다: 
redis.pipeline().set('foo', 'bar').del('cc').exec(function (err, results) {
});

// `exec` 또한 Promise를 반환합니다:
var promise = redis.pipeline().set('foo', 'bar').get('foo').exec();
promise.then(function (result) {
  // result === [[null, 'OK'], [null, 'bar']]
});
```

각 연결 명령에는 콜백이있을 수 있으며, 명령이 응답을 받으면 호출됩니다:

```javascript
redis.pipeline().set('foo', 'bar').get('foo', function (err, result) {
  // result === 'bar'
}).exec(function (err, result) {
  // result[1][1] === 'bar'
});
```

`pipeline` 큐에 명령을 개별적 으로 추가하는 것 외에도 명령 및 인수 배열을 생성자에 전달할 수도 있습니다:

```javascript
redis.pipeline([
  ['set', 'foo', 'bar'],
  ['get', 'foo']
]).exec(function () { /* ... */ });
```

`#length` 속성은 파이프 라인에서 몇 개의 명령을 보여줍니다:

```javascript
const length = redis.pipeline().set('foo', 'bar').get('foo').length;
// length === 2
```


## Transaction
대부분의 시간, 명령 트랜잭션 `multi`및이 `exec`파이프 라인과 함께 사용된다. 따라서 when `multi`이 호출되면 Pipeline기본적으로 인스턴스가 자동으로 만들어 지므로 다음 `multi`과 같이 사용할 수 있습니다 `pipeline`:

```javascript
redis.multi().set('foo', 'bar').get('foo').exec(function (err, results) {
  // results === [[null, 'OK'], [null, 'bar']]
});
```
트랜잭션의 명령 체인에 구문 오류 (예 : 잘못된 인수 수, 잘못된 명령 이름 등)가 있으면 아무 명령도 실행되지 않고 오류가 반환됩니다:

```javascript
redis.multi().set('foo').set('foo', 'new value').exec(function (err, results) {
  // err:
  //  { [ReplyError: EXECABORT Transaction discarded because of previous errors.]
  //    name: 'ReplyError',
  //    message: 'EXECABORT Transaction discarded because of previous errors.',
  //    command: { name: 'exec', args: [] },
  //    previousErrors:
  //     [ { [ReplyError: ERR wrong number of arguments for 'set' command]
  //         name: 'ReplyError',
  //         message: 'ERR wrong number of arguments for \'set\' command',
  //         command: [Object] } ] }
});
```

인터페이스의 관점에서 `multi`상이한 `pipeline`각 체인 커맨드에 대한 콜백을 지정하는 경우에는 큐 상태 대신에 명령의 결과의 콜백에 전달된다:

```javascript
redis.multi().set('foo', 'bar', function (err, result) {
  // result === 'QUEUED'
}).exec(/* ... */);
```

당신은 파이프 라인없이 트랜잭션을 사용하려면, 통과 `{ pipeline: false }`에 `multi`, 모든 명령은 즉시 기다리지 않고 레디 스로 전송됩니다 `exec`호출:

```javascript
redis.multi({ pipeline: false });
redis.set('foo', 'bar');
redis.get('foo');
redis.exec(function (err, result) {
  // result === [[null, 'OK'], [null, 'bar']]
});
```

`of`의 생성자는 `multi`일련의 명령을 받아들입니다:

```javascript
redis.multi([
  ['set', 'foo', 'bar'],
  ['get', 'foo']
]).exec(function () { /* ... */ });
```

인라인 트랜잭션은 파이프 라인에서 지원됩니다. 즉, 파이프 라인에있는 명령의 하위 집합을 트랜잭션으로 그룹화 할 수 있습니다:

```javascript
redis.pipeline().get('foo').multi().set('foo', 'bar').get('foo').exec().get('foo').exec();
```

## Lua Scripting
ioredis 같은 스크립트 명령을 모두 지원합니다 `EVAL`, `EVALSHA`하고 `SCRIPT`. 그러나 개발자가 스크립트 캐싱을 처리하고 언제 사용 `EVAL`하고 언제 사용할 것인지를 감지해야하기 때문에 실제 시나리오에서 사용하는 것은 지루 합니다 `EVALSHA`. ioredis `defineCommand`는 스크립팅을 훨씬 쉽게 사용할 수 있는 방법을 제공합니다.

```javascript
var redis = new Redis();

// This will define a command echo:
redis.defineCommand('echo', {
  numberOfKeys: 2,
  lua: 'return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}'
});

// 이제 다른 일반적인 명령처럼`echo`도 사용할 수 있습니다. 
// ioredis는 가능한 경우 성능 향상을 위해 내부적으로 EVALSHA를 사용하려고합니다. 
redis.echo('k1', 'k2', 'a1', 'a2', function (err, result) {
  // result === ['k1', 'k2', 'a1', 'a2']
});

// `echoBuffer`는 문자열 대신 버퍼를 반환하도록 자동으로 정의됩니다:
redis.echoBuffer('k1', 'k2', 'a1', 'a2', function (err, result) {
  // result[0] equals to Buffer.from('k1');
});

// 그리고 파이프 라인과 함께 작동합니다:
redis.pipeline().set('foo', 'bar').echo('k1', 'k2', 'a1', 'a2').exec();
```

명령을 정의 할 때 키 수를 결정할 수없는 경우 명령 `numberOfKeys`을 호출 할 때 속성을 생략 하고 첫 번째 인수로 키 수를 전달할 수 있습니다:

```javascript
redis.defineCommand('echoDynamicKeyNumber', {
  lua: 'return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}'
});

// 이제 매번 첫 번째 인자로 키의 수를 전달해야한다. 
// 당신은`echoDynamicKeyNumber` 명령을 호출한다 :
redis.echoDynamicKeyNumber(2, 'k1', 'k2', 'a1', 'a2', function (err, result) {
  // result === ['k1', 'k2', 'a1', 'a2']
});
```

## Transparent Key Prefixing(투명한 키 접두사)
이 기능을 사용하면 명령의 모든 키 앞에 자동으로 추가되는 문자열을 지정할 수 있으므로 키 네임 스페이스를보다 쉽게 ​​관리 할 수 ​​있습니다.

**Warning** 기능은 실제 키([#239](https://github.com/luin/ioredis/issues/239))가 아닌 패턴을 사용하는 [KEYS](http://redis.io/commands/KEYS) and [SCAN](http://redis.io/commands/scan) 
과 같은 명령에는 적용되지 않으며이 기능은 키 이름 ([#325](https://github.com/luin/ioredis/issues/325))
인 경우에도 명령 응답에 적용되지 않습니다.

```javascript
var fooRedis = new Redis({ keyPrefix: 'foo:' });
fooRedis.set('bar', 'baz');  // 실제로 SET foo를 보낸다 : bar baz

fooRedis.defineCommand('echo', {
  numberOfKeys: 2,
  lua: 'return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}'
});

// 파이프 라이닝 / 트랜잭션 
fooRedis.pipeline()
  // SORT foo를 보냅니다:list BY foo:weight_*->fieldname
  .sort('list', 'BY', 'weight_*->fieldname')
  // 사용자 정의 명령을 지원합니다. 
  // EVALSHA xxx foo를 보냅니다:k1 foo:k2 a1 a2
  .echo('k1', 'k2', 'a1', 'a2')
  .exec()
```

## Transforming Arguments & Replies(인수 및 응답 변환하기)
대부분의 Redis 명령은 하나 이상의 String을 인수로 사용하고 응답은 단일 String 또는 String of Array로 다시 전송됩니다. 그러나 때로는 뭔가 다른 것을 원할 수도 있습니다. 예를 들어, `HGETALL` 명령 `{ key: val1, key2: v2 }`이 키 값의 배열 (예 :) 대신 해시 (예 : hash )를 반환 하면보다 편리합니다 `[key1, val1, key2, val2]`.

ioredis는 인수와 응답을 변형하기위한 유연한 시스템을 갖추고 있습니다. 변압기에는 인수 변압기와 응답 변압기의 두 가지 유형이 있습니다:

```javascript
var Redis = require('ioredis');

// 여기에 내장 된 인수 변환하는 transformer converting
// hmset('key', { k1: 'v1', k2: 'v2' })
// or
// hmset('key', new Map([['k1', 'v1'], ['k2', 'v2']]))
// into
// hmset('key', 'k1', 'v1', 'k2', 'v2')
Redis.Command.setArgumentTransformer('hmset', function (args) {
  if (args.length === 2) {
    if (typeof Map !== 'undefined' && args[1] instanceof Map) {
      // utils is a internal module of ioredis
      return [args[0]].concat(utils.convertMapToArray(args[1]));
    }
    if ( typeof args[1] === 'object' && args[1] !== null) {
      return [args[0]].concat(utils.convertObjectToArray(args[1]));
    }
  }
  return args;
});

// 여기서 내장 HGETALL 응답 변환 응답 transformer converting
// ['k1', 'v1', 'k2', 'v2']
// into
// { k1: 'v1', 'k2': 'v2' }
Redis.Command.setReplyTransformer('hgetall', function (result) {
  if (Array.isArray(result)) {
    var obj = {};
    for (var i = 0; i < result.length; i += 2) {
      obj[result[i]] = result[i + 1];
    }
    return obj;
  }
  return result;
});
```

`hmset` &에 대한 두 개의 인수 변환기 및 `mset`응답 변환기가 내장 된 변환기가 세 개 있습니다 `hgetall`. 변압기 `hmset`와는 `hgetall`위에서 언급되었고, 용 변압기 `mset`에 대한 것과 유사합니다 `hmset`:

```javascript
redis.mset({ k1: 'v1', k2: 'v2' });
redis.get('k1', function (err, result) {
  // result === 'v1';
});

redis.mset(new Map([['k3', 'v3'], ['k4', 'v4']]));
redis.get('k3', function (err, result) {
  // result === 'v3';
});
```

reply 트랜스포머의 또 다른 유용한 예는 `hgetall`바이너리 해시 키를 처리 할 때 해시 키와 문자열의 원하지 않는 대화를 피하는 객체 대신 배열의 배열을 반환 하도록 변경 하는 것입니다:

```javascript
Redis.Command.setReplyTransformer('hgetall', function (result) {
  var arr = [];
  for (var i = 0; i < result.length; i += 2) {
    arr.push([result[i], result[i + 1]]);
  }
  return arr;
});
redis.hset('h1', Buffer.from([0x01]), Buffer.from([0x02]));
redis.hset('h1', Buffer.from([0x03]), Buffer.from([0x04]));
redis.hgetallBuffer('h1', function (err, result) {
  // result === [ [ <Buffer 01>, <Buffer 02> ], [ <Buffer 03>, <Buffer 04> ] ];
});
```

## Monitor(모니터링)

Redis는 다른 클라이언트 라이브러리 및 다른 컴퓨터를 포함한 모든 클라이언트 연결에서 Redis 서버가 수신 한 모든 명령을 볼 수있는 MONITOR 명령을 지원합니다.

`monitor`방법은 모니터 인스턴스를 반환합니다. MONITOR 명령을 보내면 해당 연결에서 다른 명령이 유효하지 않습니다. ioredis는 새로운 모니터 메시지가 나올 때마다 모니터 이벤트를 내 보냅니다. 모니터 이벤트에 대한 콜백은 Redis 서버의 타임 스탬프와 명령 인수 배열을 사용합니다.

다음은 간단한 예입니다:

```javascript
redis.monitor(function (err, monitor) {
  monitor.on('monitor', function (time, args, source, database) {
  });
});
```

## Streamify Scanning
Redis 2.8 `SCAN`에는 데이터베이스의 키를 점진적으로 반복 하는 명령이 추가되었습니다. 그것은 다른있어 `KEYS`그의 `SCAN`요소 만 적은 수의 각 호출을 반환, 그래서 그것은 오랜 시간 동안 서버를 차단의 단점없이 생산에 이용 될 수있다. 그러나 `SCAN`모든 키를 올바르게 반복하기 위해 명령이 호출 될 때마다 클라이언트 측에 커서를 기록해야 합니다. 비교적 일반적인 사용 사례이므로 ioredis는 `SCAN`명령을 훨씬 쉽게 해주는 스트리밍 인터페이스를 제공합니다. 읽을 수있는 스트림은 다음을 호출하여 만들 수 있습니다 `scanStream`.

```javascript
var redis = new Redis();
// Create a readable stream (object mode)
var stream = redis.scanStream();
stream.on('data', function (resultKeys) {
  // `resultKeys` 키 이름을 나타내는 문자열 배열입니다. 
  // resultKeys 0 키를 포함 할 수 있습니다, 그것은 때때로 것이다 
  // 레디 스에서 SCAN의 구현으로 인해 중복 포함.
  for (var i = 0; i < resultKeys.length; i++) {
    console.log(resultKeys[i]);
  }
});
stream.on('end', function () {
  console.log('all keys have been visited');
});
```

`scanStream` accepts an option, with which you can specify the `MATCH` pattern and the `COUNT` argument:

```javascript
var stream = redis.scanStream({
  // only returns keys following the pattern of `user:*`
  match: 'user:*',
  // 호출 당 약 100 요소를 반환 
  count: 100
});
```

다른 명령과 마찬가지로 버퍼 배열을 반환하는 `scanStream`바이너리 버전이 `scanBufferStream`있습니다. 키 이름이 utf8 문자열이 아닌 경우 유용합니다.

이 또한 `hscanStream`, `zscanStream`및 `sscanStream`해시, ZSET 및 세트의 요소를 반복 할 수 있습니다. 각각의 인터페이스는 `scanStream`첫 번째 인수가 키 이름 인 경우 를 제외하고 는 비슷합니다 .

```javascript
var stream = redis.hscanStream('myhash', {
  match: 'age:??'
});
```

[Redis documentation](http://redis.io/commands/scan)에서 자세한 내용을 확인할 수 있습니다.

**Useful Tips**
`data` 처리기 에서 비동기 작업을 수행하는 것이 일반적입니다 . 비동기 작업이 완료 될 때까지 검색 프로세스가 일시 중지되기를 바랍니다. `Stream#pause()`및 `Stream.resume()`트릭을 할. 예를 들어 Redis의 데이터를 MySQL로 마이그레이션하려는 경우:

```javascript
var stream = redis.scanStream();
stream.on('data', function (resultKeys) {
  // 우리는 현재 키 마이그레이션 할 때까지 이상의 키를 스캔에서 스트림을 일시 정지
  stream.pause();

  Promise.all(resultKeys.map(migrateKeyToMySQL)).then(() => {
    // 여기에서 다시 시작
    stream.resume();
  });
});

stream.on('end', function () {
  console.log('done migration');
});
```

## Auto-reconnect(자동 다시 연결)
기본적으로 ioredis는 레디 스에 대한 연결이 연결이 수동으로 폐쇄되는 경우를 제외하고는 손실 된 경우 다시 연결을 시도합니다 `redis.disconnect()`나 `redis.quit()`.

이 `retryStrategy`옵션을 사용하여 연결 해제 후 재 연결을 기다리는 시간을 제어하는 ​​것은 매우 유연합니다 .

```javascript
var redis = new Redis({
  // This is the default value of `retryStrategy`
  retryStrategy: function (times) {
    var delay = Math.min(times * 50, 2000);
    return delay;
  }
});
```

`retryStrategy`연결이 끊어졌을 때 호출 될 함수입니다. 인수 `times`는이 연결이 n 번째 재 연결이고 반환 값이 재 연결을 기다리는 시간 (ms)을 나타냄을 의미합니다. 반환 값이 숫자가 아닌 경우, ioredis는 재 연결 시도를 중지하고 사용자가 `redis.connect()`수동으로 호출하지 않으면 연결이 영구적으로 손실됩니다 .

다시 연결되면 클라이언트는 이전에 가입 한 채널을 자동으로 구독합니다. `autoResubscribe`옵션을 로 설정하면이 동작을 비활성화 할 수 있습니다 `false`.

그리고 이전 연결에 unfulfilled 명령이있을 경우 (예 : `brpop`and와 같은 차단 명령 일 가능성이 높음 `blpop`) 클라이언트는 다시 연결될 때 클라이언트를 다시 보냅니다. `autoResendUnfulfilledCommands`옵션을 로 설정하면이 동작을 비활성화 할 수 있습니다 `false`.

기본적으로 보류중인 모든 명령은 20 번의 재시도 시도마다 오류와 함께 삭제됩니다. 이렇게하면 연결이 끊어졌을 때 명령이 영원히 기다리지 않게됩니다. 다음과 같이 설정하여이 동작을 변경할 수 있습니다 `maxRetriesPerRequest`.

```javascript
var redis = new Redis({
  maxRetriesPerRequest: 1
});
```

`null`이 동작을 비활성화 하려면 maxRetriesPerRequest를 설정 하고 모든 명령은 연결이 다시 활성화 될 때까지 영원히 기다립니다 (ioredis v4 이전의 기본 동작).

### Reconnect on error(오류시 다시 연결)

연결이 닫힐 때 자동으로 다시 연결하는 것 외에도 ioredis는 `reconnectOnError`옵션 을 사용하여 지정된 오류에 대한 재 연결을 지원합니다 . 다음은 `READONLY`오류를 수신 할 때 다시 연결하는 예입니다:

```javascript
var redis = new Redis({
  reconnectOnError: function (err) {
    var targetError = 'READONLY';
    if (err.message.slice(0, targetError.length) === targetError) {
      // 오류가 "READONLY"로 시작될 때만 다시 연결하십시오.
      return true; // or `return 1;`
    }
  }
});
```

이 기능은 Amazon ElastiCache를 사용할 때 유용합니다. 일단 장애 조치가 발생하면 Amazon ElastiCache는 현재 연결된 마스터를 슬레이브로 전환하여 다음과 같은 쓰기가 오류로 인해 실패하게됩니다 `READONLY`. 를 사용 `reconnectOnError`하면 새로운 마스터에 연결하기 위해이 오류로 인해 연결이 다시 연결되도록 할 수 있습니다.

또한 `reconnectOnError`반환 된 경우 `2`, ioredis는 재 연결 후 실패한 명령을 다시 전송합니다.

## Connection Events(연결 이벤트)
Redis 인스턴스는 Redis 서버에 대한 연결 상태에 대한 일부 이벤트를 내 보냅니다.

| Event        | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| connect      | Redis 서버에 대한 연결이 설정되면 발생합니다.                |
| ready        | 경우 `enableReadyCheck`이며 `true`, 클라이언트가 방출됩니다 `ready`서버 (디스크에서 예를 마무리로드 데이터)가 명령을 수신 할 준비가되었음을보고 할 때. <br/>그렇지 않으면 이벤트 `ready`직후에 즉시 방출됩니다 `connect`. |
| error        | 연결하는 동안 오류가 발생하면 출력됩니다. <br/>그러나 ioredis `error`는 `error`이벤트를 청취하지 않을 경우 응용 프로그램이 충돌하지 않도록 모든 이벤트를 자동으로 내 보냅니다 (최소한 하나의 리스너가있을 때만 내 보냅니다 ) . |
| close        | 설정된 Redis 서버 연결이 닫힐 때 발생합니다.                 |
| reconnecting | 후 방출 `close`재 연결이 될 때. 이 이벤트의 인수는 다시 연결하기 전의 시간 (밀리 초)입니다. |
| end          | `close`더 이상의 재 연결이 이루어지지 않거나 연결이 설정되지 않을 때 방출 됩니다. |

`Redis#status`속성을 체크 아웃 하여 현재 연결 상태를 확인할 수도 있습니다.

위의 연결 이벤트 외에 몇 가지 다른 사용자 지정 이벤트가 있습니다:

| Event  | Description                                                  |
| :----- | :----------------------------------------------------------- |
| select | 데이터베이스가 변경 될 때 발생합니다. 인수는 새로운 db 번호입니다. |

## Offline Queue(오프라인 대기열)
명령이 Redis에 의해 처리 될 수없는 경우 ( `ready`이벤트 전에 전송 됨 ) 기본적으로 오프라인 대기열에 추가되고 처리 될 때 실행됩니다. `enableOfflineQueue` 옵션을 `false`다음과 같이 설정하여이 기능을 사용 중지 할 수 있습니다:

```javascript
var redis = new Redis({ enableOfflineQueue: false });
```

## TLS Options
Redis는 기본적으로 TLS를 지원하지 않지만 연결할 Redis 서버가 TLS 프록시 (예 : [stunnel](https://www.stunnel.org/) ) 뒤에 호스팅 되거나 TLS 연결을 지원하는 PaaS 서비스 (예 : [Redis Labs](https://redislabs.com/) )에서 제공되는 경우 `tls`옵션을 설정할 수 있습니다:

```javascript
var redis = new Redis({
  host: 'localhost',
  tls: {
    //의`tls.connect ()`섹션을 참조하십시오.
    // https://nodejs.org/api/tls.html
    // 지원되는 모든 옵션
    ca: fs.readFileSync('cert.pem')
  }
});
```

<hr>

## Sentinel(보초)
ioredis는 Sentinel을 즉시 사용할 수 있습니다. 단일 노드에 연결할 때 작동하는 모든 기능이 감시 그룹에 연결할 때도 작동하므로 투명하게 작동합니다. 이 기능을 사용하려면 Redis> 2.8.12를 실행해야합니다. Sentinels의 기본 포트는 26379입니다.

Sentinel을 사용하여 연결하려면 다음을 사용하십시오:

```javascript
var redis = new Redis({
  sentinels: [{ host: 'localhost', port: 26379 }, { host: 'localhost', port: 26380 }],
  name: 'mymaster'
});

redis.set('foo', 'bar');
```

생성자에 전달 된 인수는 단일 노드에 연결하는 데 사용하는 인수와 다릅니다. 여기서 인수는 다음과 같습니다.

- `name`마스터와 하나 이상의 슬레이브 ( `mymaster`이 예에서) 로 구성된 Redis 인스턴스 그룹을 식별합니다 .
- `sentinels`연결하려는 감시 명단입니다. 이 목록은 모든 센티널 인스턴스를 열거 할 필요는 없지만 클라이언트가 다운되면 클라이언트가 다음 인스턴스를 시도 할 수 있도록 몇 가지 인스턴스를 열거 할 필요는 없습니다.
- `role`(옵션) 값 `slave`을 지정하면 Sentinel 그룹에서 임의의 슬레이브를 반환합니다.
- `preferredSlaves`(선택 사항)은 우선 순위에 따라 특정 슬레이브 또는 슬레이브 세트를 선호하는 데 사용될 수 있습니다. 함수 나 배열을 받아들입니다.

ioredis 는 장애 조치 후에도 연결된 노드가 항상 마스터 임을 **보장** 합니다. 페일 오버가 발생하면 실패한 노드에 다시 연결하려고 시도하는 대신 (다시 사용할 수있을 때 슬레이브로 강등 됨) ioredis는 새 마스터 노드를 감지하고 그 노드에 연결합니다. 장애 조치 중에 전송 된 모든 명령은 대기열에 추가되고 새 연결이 설정되면 실행되어 명령이 손실되지 않습니다.

`role`값으로 옵션 을 지정하여 마스터가 아닌 슬레이브에 연결할 수 `slave`있으며 ioredis는 연결된 마스터 노드가 항상 슬레이브라는 보장하에 지정된 마스터의 임의의 슬레이브에 연결을 시도합니다. 현재 노드가 장애 조치로 인해 마스터로 승격 된 경우 ioredis는 연결을 끊고 다른 노드가 연결되도록 감시 장치에 요청합니다.

ioredis `preferredSlaves`와 함께 옵션을 지정하면 `role: 'slave'`사용 가능한 슬레이브 풀에서 슬레이브를 선택할 때이 값을 사용하려고합니다. 의 값 `preferredSlaves`은 사용 가능한 슬레이브의 배열을 받아들이고 하나의 결과를 반환하는 함수이거나, 슬레이브 값 우선 순위의 배열을 `prio`먼저 기본값 이 가장 작은 값으로 배열 해야합니다 `1`.

```javascript
// 사용 가능한 슬레이브 형식
var availableSlaves = [{ ip: '127.0.0.1', port: '31231', flags: 'slave' }];

// preferredSlaves 배열 형식 
var preferredSlaves = [
  { ip: '127.0.0.1', port: '31231', prio: 1 },
  { ip: '127.0.0.1', port: '31232', prio: 2 }
];

// preferredSlaves 함수 형식
preferredSlaves = function(availableSlaves) {
  for (var i = 0; i < availableSlaves.length; i++) {
    var slave = availableSlaves[i];
    if (slave.ip === '127.0.0.1') {
      if (slave.port === '31234') {
        return slave;
      }
    }
  }
  // 선호하는 슬레이브를 사용할 수없는 경우 임의의 하나가 사용됩니다
  return false;
};

var redis = new Redis({
  sentinels: [{ host: '127.0.0.1', port: 26379 }, { host: '127.0.0.1', port: 26380 }],
  name: 'mymaster',
  role: 'slave',
  preferredSlaves: preferredSlaves
});
```
이 `retryStrategy`옵션 외에도, `sentinelRetryStrategy`센티넬 모드에서는 모든 센티넬 노드가 연결 중에 도달 할 수 없을 때 호출됩니다. 경우 `sentinelRetryStrategy`유효한 지연 시간 반환 ioredis 처음부터 다시 연결을 시도합니다. 의 기본값 `sentinelRetryStrategy`은 다음과 같습니다:

```javascript
function (times) {
  var delay = Math.min(times * 10, 1000);
  return delay;
}
```

## Cluster
Redis Cluster는 Redis 설치를 실행하는 방법을 제공하며 데이터는 여러 Redis 노드에서 자동으로 분할됩니다. 다음과 같이 Redis Cluster에 연결할 수 있습니다:

```javascript
var Redis = require('ioredis');

var cluster = new Redis.Cluster([{
  port: 6380,
  host: '127.0.0.1'
}, {
  port: 6381,
  host: '127.0.0.1'
}]);

cluster.set('foo', 'bar');
cluster.get('foo', function (err, res) {
  // res === 'bar'
});
```

`Cluster` 생성자는 두 개의 인수를 받아들입니다.

1. 첫 번째 인수는 연결할 클러스터의 노드 목록입니다. Sentinel과 마찬가지로이 목록은 모든 클러스터 노드를 열거 할 필요는 없지만 하나가 도달 할 수없는 경우 클라이언트는 다음 노드를 시도하고 클라이언트는 하나 이상의 노드가 연결될 때 자동으로 다른 노드를 찾습니다.
2. 두 번째 인수는 옵션입니다.
   - `clusterRetryStrategy`: 시작 노드 중 아무도 연결할 수없는 `clusterRetryStrategy`경우 호출됩니다. 숫자가 반환되면 ioredis는 지정된 지연 (ms) 후에 처음부터 시작 노드에 다시 연결을 시도합니다. 그렇지 않으면 "시작 노드 없음"오류가 반환됩니다. 이 옵션의 기본값은 다음과 같습니다:

        ```javascript
        function (times) {
          var delay = Math.min(100 + times * 2, 2000);
          return delay;
        }
        ```

        `startupNodes`다른 노드 집합으로 전환하기 위해 속성 을 수정할 수 있습니다.

        ```javascript
        function (times) {
          this.startupNodes = [{ port: 6790, host: '127.0.0.1' }];
          return Math.min(100 + times * 2, 2000);
        }
        ```

- `enableOfflineQueue`: 클래스 의 `enableOfflineQueue`옵션과 비슷합니다 `Redis`.
- `enableReadyCheck`: 사용 가능한 경우, "준비"이벤트는 `CLUSTER INFO`클러스터를보고하는 명령이 명령을 처리 할 준비가 되었을 때만 발생 합니다. 그렇지 않으면 "연결"이 방출 된 직후에 방출됩니다.
- `scaleReads`: 읽기 쿼리를 보낼 위치를 구성합니다. 자세한 내용은 아래를 참조하십시오.
- `maxRedirections`: 클러스터와 관련된 오류 (예, 경우 `MOVED`, `ASK`및 `CLUSTERDOWN`기타)을 수신하고, 클라이언트가 다른 노드로 명령을 리디렉션한다. 이 옵션은 명령을 보낼 때 허용되는 최대 리디렉션을 제한합니다. 기본값은 `16`입니다.
- `retryDelayOnFailover`: 명령을 보낼 때 대상 노드의 연결이 끊어지면 ioredis는 지정된 지연 후에 재 시도합니다. 기본값은 `100`입니다. `retryDelayOnFailover * maxRedirections > cluster-node-timeout` 장애 조치 중에는 명령이 실패하지 않도록 해야합니다 .
- `retryDelayOnClusterDown`: 클러스터가 다운되면 모든 명령은의 오류와 함께 거부됩니다 `CLUSTERDOWN`. 이 옵션이 숫자 인 경우 (기본값 `100`), 클라이언트는 지정된 시간 (ms) 후에 명령을 다시 보냅니다.
- `retryDelayOnTryAgain`:이 옵션이 숫자 인 경우 (기본값 `100`), 클라이언트는 `TRYAGAIN`지정된 시간 (ms) 후에 오류로 거부 된 명령을 다시 보내 게됩니다 .
- `redisOptions`: `Redis`노드에 연결할 때 의 생성자에 전달되는 기본 옵션 .
- `slotsRefreshTimeout`: 클러스터에서 슬롯을 새로 고치는 동안 시간 초과가 발생하기 전의 밀리 초 (기본값 `1000`)
- `slotsRefreshInterval`: 모든 자동 슬롯 새로 고침 사이의 밀리 초 (기본값 `5000`)

### Read-write splitting(읽기 - 쓰기 분할)

일반적인 redis 클러스터에는 3 개 이상의 마스터와 각 마스터에 대한 여러 개의 슬레이브가 있습니다. `scaleReads`옵션 을 설정하여 읽기 쿼리를 슬레이브에 보내고 마스터에 쿼리를 쓰면 redis 클러스터를 수평 확장 할 수 있습니다.

`scaleReads`ioredis는 절대로 모든 쿼리를 슬레이브에 보내지 않는다는 것을 의미하는 "마스터"입니다. 다른 세 가지 옵션이 있습니다.

1. "all": 마스터에게 쓰기 쿼리를 보내고 마스터 또는 슬레이브에 임의로 쿼리를 읽습니다.
2. "slave": 마스터에 쓰기 쿼리를 보내고 쿼리를 슬레이브에 읽습니다.
3. 사용자 지정 `function(nodes, command): node`: 사용자 지정 함수를 선택하여 읽기 쿼리를 보낼 노드를 선택합니다 (쓰기 쿼리는 마스터로 계속 보내집니다). 첫 번째 노드 `nodes`는 항상 관련 슬롯을 제공하는 마스터입니다. 함수가 노드 배열을 반환하면 해당 목록의 임의 노드가 선택됩니다.

예:

```javascript
var cluster = new Redis.Cluster([/* nodes */], {
  scaleReads: 'slave'
});
cluster.set('foo', 'bar'); // 이 쿼리는 마스터 중 하나에게 전송됩니다.
cluster.get('foo', function (err, res) {
  // 이 쿼리는 슬레이브 중 하나로 보내집니다.
});
```

**NB** 위의 코드 `res`에서 master와 slave 사이의 복제 지연으로 인해 "bar"와 같지 않을 수 있습니다.

### Running commands to multiple nodes(여러 노드에 명령 실행)

모든 명령은 정확히 하나의 노드로 전송됩니다. 키를 포함하는 명령 (예를 들어 `GET`, `SET`및 `HGETALL`), ioredis 열쇠 서빙 노드로 송신하고, 다른 명령 키를 포함하는 (예를하지 않는 `INFO`, `KEYS`및 `FLUSHDB`) ioredis 임의 노드로 보낸다.

때로는 클러스터의 여러 노드 (마스터 또는 슬레이브)에 명령을 보내려는 경우 `Cluster#nodes()`메소드 를 통해 노드를 가져올 수 있습니다 .

`Cluster#nodes()`"master", "slave"및 "all"(기본값) 일 수있는 매개 변수 역할을 받아들이고 `Redis`인스턴스 배열을 반환 합니다. 예:

```javascript
// 모든 슬레이브에게`FLUSHDB` 커맨드를 보냅니다:
var slaves = cluster.nodes('slave');
Promise.all(slaves.map(function (node) {
  return node.flushdb();
}));

// 모든 마스터의 키를 가져옵니다:
var masters = cluster.nodes('master');
Promise.all(masters.map(function (node) {
  return node.keys();
})).then(function (keys) {
  // keys: [['key1', 'key2'], ['key3', 'key4']]
});
```

### Transaction and pipeline in Cluster mode(클러스터 모드의 트랜잭션 및 파이프 라인)
지원되는 거의 모든 기능 ( 예 : 사용자 정의 명령, 트랜잭션 및 파이프 라인) `Redis`도 지원됩니다 `Redis.Cluster`. 그러나 클러스터 모드에서 트랜잭션과 파이프 라인을 사용할 때 다음과 같은 몇 가지 차이점이 있습니다.

1. ioredis는 파이프 라인의 모든 명령을 동일한 노드로 전송하므로 파이프 라인의 모든 키는 동일한 슬롯에 속해야합니다.
2. `multi`파이프 라인 없이는 사용할 수 없습니다 (일명 `cluster.multi({ pipeline: false })`). 전화 `cluster.multi({ pipeline: false })`를 걸면 ioredis는 `multi`명령을 전송해야하는 노드를 알 수 없기 때문 입니다.
3. 파이프 라인에서 사용자 지정 명령 연결은 클러스터 모드에서 지원되지 않습니다.

파이프 라인의 명령이 a `MOVED`또는 `ASK`오류를 수신하면 ioredis는 다음 조건이 모두 충족 될 경우 iSeries가 지정된 노드로 전체 파이프 라인을 자동으로 다시 보냅니다.

1. 파이프 라인에서받은 모든 오류는 같습니다. 예를 들어, `MOVED`다른 노드를 가리키는 두 개의 오류 가있는 경우 파이프 라인을 다시 보내지 않습니다 .
2. 성공적으로 실행 된 모든 명령은 읽기 전용 명령입니다. 이렇게하면 파이프 라인을 다시 보내면 부작용이 발생하지 않습니다.

### Pub/Sub
클러스터 모드의 Pub / Sub는 독립형 모드에서와 똑같이 작동합니다. 내부적으로 클러스터의 노드가 메시지를 받으면 메시지를 다른 노드로 브로드 캐스트합니다. ioredis는 동시에 하나의 노드를 엄격하게 구독하여 각 메시지가 한 번만 수신되도록합니다.

```javascript
var nodes = [/* nodes */];
var pub = new Redis.Cluster(nodes);
var sub = new Redis.Cluster(nodes);
sub.on('message', function (channel, message) {
  console.log(channel, message);
});

sub.subscribe('news', function () {
  pub.publish('news', 'highlights');
});
```

### Events

Event    | Description
:------------- | :-------------
connect  | emits when a connection is established to the Redis server.
ready    | emits when `CLUSTER INFO` reporting the cluster is able to receive commands (if `enableReadyCheck` is `true`) or immediately after `connect` event (if `enableReadyCheck` is false).
error    | emits when an error occurs while connecting with a property of `lastNodeError` representing the last node error received. This event is emitted silently (only emitting if there's at least one listener).
close    | emits when an established Redis server connection has closed.
reconnecting | emits after `close` when a reconnection will be made. The argument of the event is the time (in ms) before reconnecting.
end     | emits after `close` when no more reconnections will be made.
+node   | emits when a new node is connected.
-node   | emits when a node is disconnected.
node error | emits when an error occurs when connecting to a node

### Password
password암호로 보호 된 클러스터에 액세스 하는 옵션 설정 :

```javascript
var Redis = require('ioredis');
var cluster = new Redis.Cluster(nodes, {
  redisOptions: {
    password: 'your-cluster-password'
  }
});
```

클러스터의 일부 노드가 다른 암호를 사용하는 경우 첫 번째 매개 변수에 지정해야합니다:

```javascript
var Redis = require('ioredis');
var cluster = new Redis.Cluster([
  // 사용 암호는 "암호-30001은"30001에 대한 
  { port: 30001, password: 'password-for-30001'},
  // 암호를 사용하지 마십시오 30002에 액세스 할 때 
  { port: 30002, password: null }
  // 다른 노드는 "fallback-password"를 사용할 것입니다.
], {
  redisOptions: {
    password: 'fallback-password'
  }
});
```

<hr>

# Error Handling(오류 처리)
Redis 서버가 반환하는 모든 오류는의 인스턴스이며 다음을 `ReplyError`통해 액세스 할 수 있습니다 `Redis`:

```javascript
var Redis = require('ioredis');
var redis = new Redis();
// 이 명령은 SET 명령에 두 개의 인수가 필요하므로 응답 오류가 발생합니다.
redis.set('foo', function (err) {
  err instanceof Redis.ReplyError
});
```

이것은 다음의 오류 스택입니다 `ReplyError`:

```
ReplyError: ERR wrong number of arguments for 'set' command
    at ReplyParser._parseResult (/app/node_modules/ioredis/lib/parsers/javascript.js:60:14)
    at ReplyParser.execute (/app/node_modules/ioredis/lib/parsers/javascript.js:178:20)
    at Socket.<anonymous> (/app/node_modules/ioredis/lib/redis/event_handler.js:99:22)
    at Socket.emit (events.js:97:17)
    at readableAddChunk (_stream_readable.js:143:16)
    at Socket.Readable.push (_stream_readable.js:106:10)
    at TCP.onread (net.js:509:20)
```

기본적으로 전체 스택은 코드가 아닌 ioredis 모듈 자체에서 발생하므로 오류 스택은 의미가 없습니다. 따라서 코드에서 오류가 발생한 부분을 찾는 것이 쉽지 않습니다. ioredis는 `showFriendlyErrorStack`문제를 해결할 수있는 옵션 을 제공합니다 . 활성화`showFriendlyErrorStack`하면 ioredis가 오류 스택을 최적화합니다:

```javascript
var Redis = require('ioredis');
var redis = new Redis({ showFriendlyErrorStack: true });
redis.set('foo');
```

출력은 다음과 같습니다:

```
ReplyError: ERR wrong number of arguments for 'set' command
    at Object.<anonymous> (/app/index.js:3:7)
    at Module._compile (module.js:446:26)
    at Object.Module._extensions..js (module.js:464:10)
    at Module.load (module.js:341:32)
    at Function.Module._load (module.js:296:12)
    at Function.Module.runMain (module.js:487:10)
    at startup (node.js:111:16)
    at node.js:799:3
```

이번에는 스택에서 코드의 세 번째 줄에 오류가 있음을 알립니다. 꽤 달콤한! 그러나 오류 스택을 최적화하기 위해 성능이 크게 저하됩니다. 따라서 기본적으로이 옵션은 사용할 수 없으며 디버깅 용도로만 사용할 수 있습니다. 당신은 안 프로덕션 환경에서이 기능을 사용합니다.

# Plugging in your own Promises Library(자신의 약속 라이브러리에 연결하기)
고급 사용자라면 [bluebird](https://www.npmjs.com/package/bluebird) 와 같은 자신 만의 약속 라이브러리를 플러그인 할 수 있습니다 . Redis.Promise를 좋아하는 ES6 스타일 약속 생성자로 설정하면 ioredis가이를 사용합니다.

```javascript
const Redis = require('ioredis')
Redis.Promise = require('bluebird')

const redis = new Redis()

// Use bluebird
assert.equal(redis.get().constructor, require('bluebird'))

// 언제든지 Promise 구현을 변경할 수 있습니다:
Redis.Promise = global.Promise
assert.equal(redis.get().constructor, global.Promise)
```


# Running tests(테스트 실행 중)

Start a Redis server on 127.0.0.1:6379, and then:

```shell
$ npm test
```

`FLUSH ALL` 각 테스트 후에 호출되므로 테스트를 실행하기 전에 중요한 데이터가 없는지 확인하십시오.

테스트 환경에서 Redis 서버를 [구동](https://github.com/stipsan/ioredis-mock) 할 수없는 경우 [ioredis-mock](https://github.com/stipsan/ioredis-mock) 은 테스트에서 사용할 수있는 드롭 인 대체 프로그램입니다. Redis 서버에 연결된 ioredis와 동일하게 작동하여 통합 테스트를 작성하고 품질을 향상시킵니다.

# Debug

`DEBUG`env를 설정하여 `ioredis:*`디버그 정보를 인쇄 할 수 있습니다:

```shell
$ DEBUG=ioredis:* node app.js
```

# Consolidation: It's time for celebration(강화 : 축하 할 시간이다)

지금은 주위에 두 개의 훌륭한 redis 클라이언트가 있으며 둘 다 서로 위에 몇 가지 장점이 있습니다. 우리는 [node_redis](https://github.com/NodeRedis/node_redis) 와 ioredis 에 대해 이야기 합니다. 그래서 서로 협력하여 우리가 함께 일할 수있는 방법에 대해 이야기 한 후에 (즉, [@BridgeAR](https://github.com/BridgeAR) 과 [@luin](https://github.com/luin) ) 장기적으로 단일 라이브러리를 향해 작업하기로 결정했습니다. 그러나 단계적으로.

우선 우리는 라이브러리의 작은 부분을 다른 부분으로 나누어 동일한 코드를 사용할 수있게하려고합니다. 이러한 라이브러리는 NodeRedis 조직하에 유지 관리됩니다. 이는 유지 보수 오버 헤드를 줄이고, 다른 사람들이 똑같은 코드를 사용할 수있게하고, 필요하다면 다른 사람들이 두 라이브러리에 기여하는 것이 더 쉽습니다.

우리는 가능한 한 최고의 redis 경험을 제공하기 위해 함께 일하는이 단계에 매우 만족합니다.

도움을 받아 도움을 청하기 원하면 언제든지 저희에게 연락하십시오.

# Join in!

버그 리포트, 픽스, 문서 개선 및 기타 개선 사항을 받게되어 기쁩니다.

그리고 저는 영어 원어민이 아니기 때문에, 문서에서 문법적인 실수를 발견하면 알려주십시오. :)

# Contributors

이 프로젝트는 기여한 모든 사람들에게 감사드립니다:

<a href="https://github.com/luin/ioredis/graphs/contributors"><img src="https://opencollective.com/ioredis/contributors.svg?width=890&showBtn=false" /></a>

# License

MIT
