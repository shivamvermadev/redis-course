# Redis Course

- To start redis use `redis-server` command
- To connect to redis server or create a redis client via terminal use `redis-cli` command
- `INFO` command is used to get the information about the redis server.
- To disconnect client from redis server use QUIT command or ctrl + d keys
- refer https://redis.io/commands/ for all commands that can be ran on redis.
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

---
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

### Key Spaces
- Key spaces in redis is simmilar to databases namespace schemas(Like different Databases in MySQL)
- This allows you to have same key name in multiple key space
- Key values are override in same key space location
- You can manage keys per each key spaces
- Key space index start with 0
- To use a key space use below command, index starts with 0, which is default key space 
```
SELECT index
```

- FLUSHDB is the command to delete all the keys in a key space
```
FLUSHDB
```
- You cannot link keys with on key space to another key space like SQL can

### Keys naming convention
- Redis keys are binary safe - you can use any binary sequence as a key
- Empty string is also a valid key

### Keys pattern matching
```
KEYS pattern
```
- Consider KEYS as a command that should be used in production environment with extreme care. It may ruin the performance when it is executed against large databases.
- Consider using `SCAN`
- h`?`llo matches hello, hallo, hxllo
- h`*`llo matches hllo, heeeeello
- h`[ae]`llo matches hello or hallo, but not hillo, either a or e
- h`[^e]`llo matches hallo, hbllo... but not hello
- h`[a-c]`llo matches hallo, hbllo, hcllo, from a to c

### Saving keys information on server
- To save keys on the disk we can use the below command
```
SHUTDOWN save
```
- To not save the keys on the disk for current redis session
```
SHUTDOWN nosave
```

### Rename a key
- Renames key to newkey. It returns an error when key does not exist. If newkey already exists it is overwritten, when this happens RENAME executes an implicit DEL operation, so if the deleted key contains a very big value it may cause high latency even if RENAME itself is usually a constant-time operation.

- In Cluster mode, both key and newkey must be in the same hash slot, meaning that in practice only keys that have the same hash tag can be reliably renamed in cluster.
```
RENAME key newkey
```

### Rename a key with caution
- Renames key to newkey if newkey does not yet exist. It returns an error when key does not exist.
- Return : Integer :
    - 1 if key was renamed to newkey.
    - 0 if newkey already exists.

### Deleting keys Asynchronously via UNLINK
- When we do ` DEL k1 k2 ` system first deletes k1, waits for it to get deleted and then start deleting k2 and then gives control back on the terminal, which means DEL operation deletes the keys synchronously
- To delete keys asynchronously use `UNLINK` command, it will do the things in background.

### How to find the data type of value hold by a key
```
TYPE key
```
---

## Redis Data Types

### String

### Counting Numbers using INCR and DECR
- To increment number by 1 use INCR command, provided value of key should be integer parsable
```
INCR key
```
- To decrement number by 1 use DECR command, provided value of key should be integer parsable
```
DECR key
```

- To increase the number by `X` use INCRBY command, provided value of key should be integer parsable
```
INCRBY key X
```

- To decrease the number by `X` use DECRBY command, provided value of key should be integer parsable
```
DECRBY key X
```

### Increment and decrement float numbers
- To increment and decrement float numbers, use INCRBYFLOAT command, provided the value of key should be integer or float parsable, also to decrement the value by X we have use -X.

#### For Incrementing 
```
INCRBYFLOAT key X 
```

#### For Decrementing
```
INCRBYFLOAT key -X 
```

### To append string at the end of another existing string
- To append string at the end of another existing string, use APPEND command. If the key exists then the string is appended and if the key does not exist then new key is created with the value to be append.

```
APPEND key "stringVal"
```

### To get the len of string
- Use STRLEN to get the length of string
```
STRLEN key
```

### To set multiple keys and values
- Use MSET command to set multiple keys and values, if there already exists a key, then MSET will override the value for that key.

```
MSET k1 v1 k2 v2 k3 v3
```

### To get multiple keys and values
- Use MGET command to get multiple keys and values, if there is key that does not exist then MGET will return nil for that key.

```
MGET k1 k2 k3
```

### To set multiple keys and values, for the keys that does not exist
- Use MSETNX command to set values for the keys that does not exist. MSETNX will not perform any operation at all even if just a single key already exists.

```
MSETNX k1 v1 k2 v2
```

### To get substring of a string
- To get the substring of a string use GETRANGE command.

```
GETRANGE key startIndex endIndex
```
- startIndex <= endIndex
- To get the whole string pass startIndex = 0 and endIndex = -1


### To set the key with expiration
- Setting the key with expiration in seconds
```
SETEX key number_of_seconds value
```

- Setting the key with expiration in milliseconds
```
PSETEX key number_of_milliseconds value
```

### Redis string encoding Types
- `int` : For strings representing 64 bit signed integers.
- `embstr` : For strings whose length is less or equal to 44 bytes this type of encoding is more efficient in memory usage and performance.
- `raw` : For strings whose length is greater than 44 bytes.

- To get the encoding type of a key, use below command
```
OBJECT ENCODING key
```