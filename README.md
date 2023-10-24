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

### to set the value for key
```
SET key value
``` 

### to get the value for key
```
GET key value
``` 

### To delete a key use DEL command
```
DEL key1 key2
```

### How to check if keys exists or not
```
exists key1 key2
```