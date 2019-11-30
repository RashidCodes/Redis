# Introduction to Redis
Visit https://redis.io/commands for a list of all commands.


### Get redis using docker
```bash
docker pull redis
```

**Start with persistent storage**
```bash
docker run --name some-redis --network some-network -d redis redis-server --appendonly yes
```

**Connect to the redis-cli**

This container will be removed immediately after I'm done using it.
```bash
docker run -it --network some-network --rm redis redis-cli -h some-redis
```

### Commands
Format: **command (->returns) output**

```bash
ping -> pong
echo "Hello World"  -> "Hello world"
```

SET-VALUE
```bash
SET key value

eg.
SET foo 100 -> OK
```

GET-VALUE
```bash
GET foo -> "100"
```

INCREMENT A VALUE
```bash
INCR foo -> (integer) 101
```

DECREMENT A VALUE
```bash
DECR foo -> (integer) 100
```

CHECK IF SOMETHING EXITS
```bash
EXISTS foo -> (integer) 1
EXISTS food -> (integer) 0
```

DELETE KEY:VALUE PAIR
```bash
DEL foo -> (integer) 1
```

CLEAR EVERYTHING OUT ENTIRELY
```bash
FLUSHALL -> OK
```

KEY SPACES
```bash
SET server:name someserver -> OK
GET server:name -> "someserver"
```

SET VALUES THAT WILL EXPIRE AFTER SOME TIME
```bash
SET greeting "Hello world" 
EXPIRE greeting 50 -> (integer) 1
TTL greeting -> 50
TTL greeting -> 49
...
TTL greeting -> 0
GET greeting -> (nil)


OR 

SETEX greeting 30 "Hello world" -> OK
```

PERSISTING A KEY WITH A TTL
While the TTL is reducing, run the following command to persist greeting.

```bash
PERSIST greeting
```

SETTING MULTIPLE KEY:VALUE PAIRS
```bash
MSET key1 "hello" key2 "world" -> OK
```

RENAME KEYS
```bash
RENAME key1 greeting -> OK
```


### DATA TYPES

**Lists**
Appending values to the head of a list called "people"
```bash
LPUSH people "Rashid" -> (integer) 1
LPUSH people "Jennifer" -> (integer) 1
LPUSH people "Saeed" -> (integer) 1
```

Output the list
```bash
LRANGE people 0 -1
```

