## Classes

<dl>
<dt><a href="#Redis">Redis</a> ⇐ <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code></dt>
<dd></dd>
<dt><a href="#Cluster">Cluster</a> ⇐ <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code></dt>
<dd></dd>
<dt><a href="#Commander">Commander</a></dt>
<dd></dd>
</dl>

<a name="Redis"></a>

## Redis ⇐ <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code>
**Kind**: global class  
**Extends**: <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code>, [<code>Commander</code>](#Commander)  

* [Redis](#Redis) ⇐ <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code>
    * [new Redis([port], [host], [options])](#new_Redis_new)
    * _instance_
        * [.connect([callback])](#Redis+connect) ⇒ <code>Promise.&lt;void&gt;</code>
        * [.disconnect()](#Redis+disconnect)
        * ~~[.end()](#Redis+end)~~
        * [.duplicate()](#Redis+duplicate)
        * [.monitor([callback])](#Redis+monitor)
        * [.getBuiltinCommands()](#Commander+getBuiltinCommands) ⇒ <code>Array.&lt;string&gt;</code>
        * [.createBuiltinCommand(commandName)](#Commander+createBuiltinCommand) ⇒ <code>object</code>
        * [.defineCommand(name, definition)](#Commander+defineCommand)
    * _static_
        * ~~[.createClient()](#Redis.createClient)~~

<a name="new_Redis_new"></a>

### new Redis([port], [host], [options])
Creates a Redis instance


| Param                                   | Type                           | Default       | Description                                                  |
| --------------------------------------- | ------------------------------ | ------------- | ------------------------------------------------------------ |
| [port]                                  | `number` | `string` | `Object` | `6379`        | Redis 서버의 포트 또는 URL 문자열 (아래 예제 참조) 또는 `options`객체 (세 번째 인수 참조). |
| [host]                                  | `string` | `Object`            | `"localhost"` | Redis 서버의 호스트는 첫 번째 인수가 URL 문자열 일 때이 인수는 객체를 나타내는 옵션입니다. |
| [options]                               | `Object`                       |               | 다른 옵션.                                                   |
| [options.port]                          | `number`                       | `6379`        | Redis 서버의 포트입니다.                                     |
| [options.host]                          | `string`                       | `"localhost"` | Redis 서버의 호스트.                                         |
| [options.family]                        | `string`                       | `4`           | IP 스택의 버전. 기본값은 4입니다.                            |
| [options.path]                          | `string`                       | `null`        | 로컬 도메인 소켓 경로. 설정하면 및`port`, 무시됩니다.`host``family` |
| [options.keepAlive]                     | `number`                       | `0`           | 시작하기 전에 지연 시간이 Xms 인 소켓의 TCP KeepAlive. keepAlive를 사용하지 않으려면 숫자가 아닌 값으로 설정하십시오. |
| [options.noDelay]                       | `boolean`                      | `true`        | Nagle의 알고리즘을 비활성화할지 여부. 기본적으로 지연 시간을 줄이려면이 기능을 비활성화하십시오. |
| [options.connectionName]                | `string`                       | `null`        | 연결 이름.                                                   |
| [options.db]                            | `number`                       | `0`           | 사용할 데이터베이스 인덱스입니다.                            |
| [options.password]                      | `string`                       | `null`        | 설정된 경우 클라이언트는이 옵션 값과 함께 AUTH 명령을 전송합니다. |
| [options.dropBufferSupport]             | `boolean`                      | `false`       | 더 나은 성능을 위해 버퍼 지원을 중단하십시오. 이 옵션은 큰 배열 응답을 처리 할 때 사용 가능하게 설정하는 것이 좋으며 버퍼 지원이 필요하지 않습니다. |
| [options.enableReadyCheck]              | `boolean`                      | `true`        | Redis 서버에 대한 연결이 설정되면 서버가 여전히 디스크에서 데이터베이스를로드 중일 수 있습니다. 로드하는 동안 서버는 명령에 응답하지 않습니다. 이 문제를 해결하기 위해이 옵션을 사용 `true`하면 ioredis가 Redis 서버의 상태를 확인하고 Redis 서버가 명령을 처리 할 수있을 때 `ready`이벤트가 방출됩니다. |
| [options.enableOfflineQueue]            | `boolean`                      | `true`        | 레디스 서버에 활성 연결이 없을 경우 기본적으로 명령은 큐에 추가하고 연결이 "준비"일단 실행 (`enableReadyCheck`이다 `true`, "준비"는 레디 스 서버가 디스크에서 데이터베이스를로드 다른 수단을 의미 Redis 서버에 대한 연결이 설정되었습니다). 이 옵션이 false이면 연결 준비가되지 않았을 때 명령을 실행할 때 오류가 반환됩니다. |
| [options.connectTimeout]                | `number`                       | `10000`       | Redis 서버에 처음 연결하는 동안 시간 초과가 발생하기 전의 밀리 초입니다. |
| [options.autoResubscribe]               | `boolean`                      | `true`        | 다시 연결 한 후 이전 연결이 구독자 모드 인 경우 클라이언트는이 채널을 자동으로 다시 구독합니다. |
| [options.autoResendUnfulfilledCommands] | `boolean`                      | `true`        | 참이면 클라이언트는 재 연결될 때 이전 연결에서 완료되지 않은 명령 (예 : 블록 명령)을 다시 보냅니다. |
| [options.lazyConnect]                   | `boolean`                      | `false`       | 기본적으로 새 `Redis`인스턴스가 생성되면 자동으로 Redis 서버에 연결됩니다. 명령이 호출 될 때까지 인스턴스 연결을 끊기를 원하면 `lazyConnect`생성자에 옵션을 전달할 수 있습니다.`javascript var redis = new Redis({ lazyConnect: true }); // No attempting to connect to the Redis server here. // Now let's connect to the Redis server redis.get('foo', function () { });` |
| [options.tls]                           | `Object`                       |               | TLS connection support. See <https://github.com/luin/ioredis#tls-options> |
| [options.keyPrefix]                     | `string`                       | `"''"`        | 명령의 모든 키 앞에 추가 할 접두사입니다.                    |
| [options.retryStrategy]                 | `function`                     |               | See "Quick Start" section                                    |
| [options.maxRetriesPerRequest]          | `number`                       |               | See "Quick Start" section                                    |
| [options.reconnectOnError]              | `function`                     |               | See "Quick Start" section                                    |
| [options.readOnly]                      | `boolean`                      | `false`       | 연결에 READONLY 모드를 사용 가능하게하십시오. 클러스터 모드에서만 사용 가능합니다. |
| [options.stringNumbers]                 | `boolean`                      | `false`       | 강제 번호는 항상 JavaScript 문자열로 반환됩니다. 이 옵션은 큰 숫자를 처리 할 때 필요합니다 ([-2^53,+2^53] 범위 초과). |

**Example**  
```js
var Redis = require('ioredis');

var redis = new Redis();

var redisOnPort6380 = new Redis(6380);
var anotherRedis = new Redis(6380, '192.168.100.1');
var unixSocketRedis = new Redis({ path: '/tmp/echo.sock' });
var unixSocketRedis2 = new Redis('/tmp/echo.sock');
var urlRedis = new Redis('redis://user:password@redis-service.com:6379/');
var urlRedis2 = new Redis('//localhost:6379');
var authedRedis = new Redis(6380, '192.168.100.1', { password: 'password' });
```
<a name="Redis+connect"></a>

### redis.connect([callback]) ⇒ <code>Promise.&lt;void&gt;</code>
Redis 연결을 만듭니다. 이 메서드 `lazyConnect: true`는 전달 되지 않는 한 새 Redis 인스턴스를 만들 때 자동으로 호출됩니다 .

이 메서드를 수동으로 호출하면 Promise가 반환되고 연결 상태가 준비되면 해결됩니다.

**Kind**: instance method of [<code>Redis</code>](#Redis)  
**Access**: public  

| Param | Type |
| --- | --- |
| [callback] | <code>function</code> | 

<a name="Redis+disconnect"></a>

### redis.disconnect()
Redis에서 연결을 끊습니다.

이 메서드는 즉시 연결을 닫고 클라이언트에 기록하지 않은 보류중인 응답을 잃을 수 있습니다. 보류중인 응답을 기다리고 싶다면 Redis #를 대신 사용하십시오.

**Kind**: instance method of [<code>Redis</code>](#Redis)  
**Access**: public  
<a name="Redis+end"></a>

### ~~redis.end()~~
***Deprecated***

Redis에서 연결을 끊습니다.

**Kind**: instance method of [<code>Redis</code>](#Redis)  
<a name="Redis+duplicate"></a>

### redis.duplicate()
현재 인스턴스와 동일한 옵션으로 새 인스턴스를 만듭니다.

**Kind**: instance method of [<code>Redis</code>](#Redis)  
**Access**: public  
**Example**  
```js
var redis = new Redis(6380);
var anotherRedis = redis.duplicate();
```
<a name="Redis+monitor"></a>

### redis.monitor([callback])
실시간으로 서버가 수신 한 모든 요청을 들어보십시오.

이 명령은 현재 연결에 방해가되지 않도록 Redis에 대한 새 연결을 만들고 새 연결을 통해 MONITOR 명령을 보냅니다.

**Kind**: instance method of [<code>Redis</code>](#Redis)  
**Access**: public  

| Param | Type | Description |
| --- | --- | --- |
| [callback] | <code>function</code> | 콜백 함수. 생략하면 약속이 반환됩니다. |

**Example**  
```js
var redis = new Redis();
redis.monitor(function (err, monitor) {
  // 모니터링 모드를 입력.
  monitor.on('monitor', function (time, args, source, database) {
    console.log(time + ": " + util.inspect(args));
  });
});

// 약속을 지원하고 다른 명령어
redis.monitor().then(function (monitor) {
  monitor.on('monitor', function (time, args, source, database) {
    console.log(time + ": " + util.inspect(args));
  });
});
```
<a name="Commander+getBuiltinCommands"></a>

### redis.getBuiltinCommands() ⇒ <code>Array.&lt;string&gt;</code>
지원되는 내장 명령 반환

**Kind**: instance method of [<code>Redis</code>](#Redis)  
**Returns**: <code>Array.&lt;string&gt;</code> - command list  
**Access**: public  
<a name="Commander+createBuiltinCommand"></a>

### redis.createBuiltinCommand(commandName) ⇒ <code>object</code>
내장 명령 만들기

**Kind**: instance method of [<code>Redis</code>](#Redis)  
**Returns**: <code>object</code> - functions  
**Access**: public  

| Param | Type | Description |
| --- | --- | --- |
| commandName | <code>string</code> | command name |

<a name="Commander+defineCommand"></a>

### redis.defineCommand(name, definition)
lua 스크립트를 사용하여 커스텀 커맨드 정의하기

**Kind**: instance method of [<code>Redis</code>](#Redis)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| name | <code>string</code> |  | 명령 이름 |
| definition | <code>object</code> |  |  |
| definition.lua | <code>string</code> |  | 루아 코드 |
| [definition.numberOfKeys] | <code>number</code> | <code></code> | 키의 수 생략하면 명령을 호출 할 때마다 첫 번째 인수로 키 개수를 전달해야합니다 |

<a name="Redis.createClient"></a>

### ~~Redis.createClient()~~
***Deprecated***

Redis 인스턴스 만들기

**Kind**: static method of [<code>Redis</code>](#Redis)  
<a name="Cluster"></a>

## Cluster ⇐ <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code>
**Kind**: global class  
**Extends**: <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code>, [<code>Commander</code>](#Commander)  

* [Cluster](#Cluster) ⇐ <code>[EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)</code>
    * [new Cluster(startupNodes, options)](#new_Cluster_new)
    * [.connect()](#Cluster+connect) ⇒ <code>Promise</code>
    * [.disconnect([reconnect])](#Cluster+disconnect)
    * [.quit([callback])](#Cluster+quit) ⇒ <code>Promise</code>
    * [.nodes([role])](#Cluster+nodes) ⇒ [<code>Array.&lt;Redis&gt;</code>](#Redis)
    * [.getBuiltinCommands()](#Commander+getBuiltinCommands) ⇒ <code>Array.&lt;string&gt;</code>
    * [.createBuiltinCommand(commandName)](#Commander+createBuiltinCommand) ⇒ <code>object</code>
    * [.defineCommand(name, definition)](#Commander+defineCommand)
    * *[.sendCommand()](#Commander+sendCommand)*

<a name="new_Cluster_new"></a>

### new Cluster(startupNodes, options)
Creates a Redis Cluster instance


| Param                             | Type                              | Default                         | Description                                                  |
| --------------------------------- | --------------------------------- | ------------------------------- | ------------------------------------------------------------ |
| startupNodes                      | <code>Array.&lt;Object&gt;</code> |                                 | 클러스터의 노드 배열, [{port : number, host : string}]       |
| options                           | <code>Object</code>               |                                 |                                                              |
| [options.clusterRetryStrategy]    | <code>function</code>             |                                 | "빠른 시작"섹션을 참조하십시오.                              |
| [options.enableOfflineQueue]      | <code>boolean</code>              | <code>true</code>               | Redis 클래스보기                                             |
| [options.enableReadyCheck]        | <code>boolean</code>              | <code>true</code>               | 활성화 된 경우, ioredis `CLUSTER INFO`는 클러스터를보고하는 명령이 명령을 처리 할 준비가 되면 "준비"이벤트 만 방출 합니다. |
| [options.scaleReads]              | <code>string</code>               | <code>&quot;master&quot;</code> | 지정된 역할이있는 노드로 읽습니다. 사용할 수있는 값은 "master", "slave"및 "all"입니다. |
| [options.maxRedirections]         | <code>number</code>               | <code>16</code>                 | MOVED 또는 ASK 오류가 수신되면 클라이언트는 명령을 다른 노드로 재 지정합니다. 이 옵션은 명령을 보낼 수있는 최대 리디렉션을 제한합니다. |
| [options.retryDelayOnFailover]    | <code>number</code>               | <code>100</code>                | 명령을 보낼 때 오류가 수신되면 (예 : 대상 Redis 노드가 작동 중지되면 "Connection is closed."), |
| [options.retryDelayOnClusterDown] | <code>number</code>               | <code>100</code>                | CLUSTERDOWN 오류가 수신되면, 클라이언트`retryDelayOnClusterDown`는 유효한 지연 시간 인 경우 재 시도합니다 . |
| [options.retryDelayOnTryAgain]    | <code>number</code>               | <code>100</code>                | TRYAGAIN 오류가 수신되면 클라이언트`retryDelayOnTryAgain`는 유효한 지연 시간 인 경우 재 시도합니다 . |
| [options.slotsRefreshTimeout]     | <code>number</code>               | <code>1000</code>               | 클러스터에서 슬롯을 새로 고치는 동안 시간 초과가 발생하기 전의 밀리 초입니다. |
| [options.slotsRefreshInterval]    | <code>number</code>               | <code>5000</code>               | 모든 자동 슬롯 새로 고침 사이의 밀리 초입니다.               |
| [options.redisOptions]            | <code>Object</code>               |                                 | 생성자에 전달되었습니다 `Redis`.                             |

<a name="Cluster+connect"></a>

### cluster.connect() ⇒ <code>Promise</code>
클러스터에 연결

**Kind**: instance method of [<code>Cluster</code>](#Cluster)  
**Access**: public  
<a name="Cluster+disconnect"></a>

### cluster.disconnect([reconnect])
클러스터의 모든 노드와의 연결을 끊습니다.

**Kind**: instance method of [<code>Cluster</code>](#Cluster)  
**Access**: public  

| Param | Type |
| --- | --- |
| [reconnect] | <code>boolean</code> | 

<a name="Cluster+quit"></a>

### cluster.quit([callback]) ⇒ <code>Promise</code>
클러스터를 정상적으로 종료하십시오.

**Kind**: instance method of [<code>Cluster</code>](#Cluster)  
**Returns**: <code>Promise</code> - return 'OK' if successfully  
**Access**: public  

| Param | Type |
| --- | --- |
| [callback] | <code>function</code> | 

<a name="Cluster+nodes"></a>

### cluster.nodes([role]) ⇒ [<code>Array.&lt;Redis&gt;</code>](#Redis)
지정된 역할을 가진 노드를 가져옵니다.

**Kind**: instance method of [<code>Cluster</code>](#Cluster)  
**Returns**: [<code>Array.&lt;Redis&gt;</code>](#Redis) - array of nodes  
**Access**: public  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [role] | <code>string</code> | <code>&quot;all&quot;</code> | role, "master", "slave" or "all" |

<a name="Commander+getBuiltinCommands"></a>

### cluster.getBuiltinCommands() ⇒ <code>Array.&lt;string&gt;</code>
지원되는 내장 명령 반환

**Kind**: instance method of [<code>Cluster</code>](#Cluster)  
**Returns**: <code>Array.&lt;string&gt;</code> - command list  
**Access**: public  
<a name="Commander+createBuiltinCommand"></a>

### cluster.createBuiltinCommand(commandName) ⇒ <code>object</code>
내장 명령 만들기

**Kind**: instance method of [<code>Cluster</code>](#Cluster)  
**Returns**: <code>object</code> - functions  
**Access**: public  

| Param | Type | Description |
| --- | --- | --- |
| commandName | <code>string</code> | command name |

<a name="Commander+defineCommand"></a>

### cluster.defineCommand(name, definition)
lua 스크립트를 사용하여 커스텀 커맨드 정의하기

**Kind**: instance method of [<code>Cluster</code>](#Cluster)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| name | <code>string</code> |  | 명령 이름 |
| definition | <code>object</code> |  |  |
| definition.lua | <code>string</code> |  | 루아 코드 |
| [definition.numberOfKeys] | <code>number</code> | <code></code> | 키의 수 생략하면 명령을 호출 할 때마다 첫 번째 인수로 키 개수를 전달해야합니다 |

<a name="Commander+sendCommand"></a>

### *cluster.sendCommand()*
명령 보내기

**Kind**: instance abstract method of [<code>Cluster</code>](#Cluster)  
**Overrides**: [<code>sendCommand</code>](#Commander+sendCommand)  
**Access**: public  
<a name="Commander"></a>

## Commander
**Kind**: global class  

* [Commander](#Commander)
    * [new Commander()](#new_Commander_new)
    * [.getBuiltinCommands()](#Commander+getBuiltinCommands) ⇒ <code>Array.&lt;string&gt;</code>
    * [.createBuiltinCommand(commandName)](#Commander+createBuiltinCommand) ⇒ <code>object</code>
    * [.defineCommand(name, definition)](#Commander+defineCommand)
    * *[.sendCommand()](#Commander+sendCommand)*

<a name="new_Commander_new"></a>

### new Commander()
Commander

이것은 Redis, Redis.Cluster 및 Pipeline의 기본 클래스입니다.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [options.showFriendlyErrorStack] | <code>boolean</code> | <code>false</code> | 친숙한 오류 스택을 표시할지 여부. 성능이 크게 저하됩니다. |

<a name="Commander+getBuiltinCommands"></a>

### commander.getBuiltinCommands() ⇒ <code>Array.&lt;string&gt;</code>
지원되는 내장 명령 반환

**Kind**: instance method of [<code>Commander</code>](#Commander)  
**Returns**: <code>Array.&lt;string&gt;</code> - command list  
**Access**: public  
<a name="Commander+createBuiltinCommand"></a>

### commander.createBuiltinCommand(commandName) ⇒ <code>object</code>
내장 명령 만들기

**Kind**: instance method of [<code>Commander</code>](#Commander)  
**Returns**: <code>object</code> - functions  
**Access**: public  

| Param | Type | Description |
| --- | --- | --- |
| commandName | <code>string</code> | 명령 이름 |

<a name="Commander+defineCommand"></a>

### commander.defineCommand(name, definition)
lua 스크립트를 사용하여 커스텀 커맨드 정의하기

**Kind**: instance method of [<code>Commander</code>](#Commander)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| name | <code>string</code> |  | 명령 이름 |
| definition | <code>object</code> |  |  |
| definition.lua | <code>string</code> |  | 루아 코드 |
| [definition.numberOfKeys] | <code>number</code> | <code></code> | 키의 수 생략하면 명령을 호출 할 때마다 첫 번째 인수로 키 개수를 전달해야합니다 |

<a name="Commander+sendCommand"></a>

### *commander.sendCommand()*
명령 보내기

**Kind**: instance abstract method of [<code>Commander</code>](#Commander)  
**Access**: public  
