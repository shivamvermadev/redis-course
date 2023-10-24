# Redis Course

- To start redis use `redis-server` command
- To connect to redis server or create a redis client via terminal use `redis-cli` command
- `INFO` command is used to get the information about the redis server.
- To disconnect client from redis server use QUIT command or ctrl + d keys
- refer https://redis.io/commands/  for all commands that can be ran on redis.
- Redis is a key based data structure.
- Redis is in the family of databases called 'Key-Value stores'.
- Key = Value 
- Value can be:
    - String
    - List
    - Hash
    - Sets
    - And more
- IMPORTANT: The data can only be retrieved if we know the exact key used to store it
- a key means is a way to store and retrieve values.

### To set the value for key
```
SET key value
``` 

### To get the value for key
```
GET key value
``` 

### To delete a key use DEL command
```
DEL key1 key2
```

### How to check if keys exists or not
```
EXISTS key1 key2
```

### Adding keys with expiration
- EX will set the expiration time in seconds
```
SET key value EX number_of_seconds
```
- PX will set the expiration time in milliseconds
```
SET key value PX number_of_seconds
```

### Get the time left for key to expire
- This will return the time left in seconds for key to expire, if the returned value is negative then the key doesn't exists.
```
TTL key
```

- This will return the time left in milli seconds for key to expire, if the returned value is negative then the key doesn't exists.
```
PTTL key
```

### To expire key 
- To expire key in some seconds, even though their prev TTL was greater, we can expire them
```
EXPIRE key num_of_seconds
```

- To expire key in some milli seconds, even though their prev TTL was greater, we can expire them
```
PEXPIRE key num_of_milliseconds
```

### How to remove expiration from a key
```
PERSIST key
```

### How redis handle key expiration
- Normal keys are created without any expiration
- Keys with expiry, Key expiration information is stored in Unix timestamp (in milliseconds)

### Keys are expired in two ways
- Passive Way : A key is passively expired simply when some client tries to access it, and the key is found to be timed out.
- Active Way :
    - Redis does 10 times per second
        - Test 20 random keys from the set of keys with an associated expire.
        - Delete all the keys found expired.
        - If more than 25% of keys were expired, start again from step 1.

