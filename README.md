# Dubzland: Redis
[![Gitlab pipeline status (self-hosted)](https://img.shields.io/gitlab/pipeline/jdubz/dubzland-redis?gitlab_url=https%3A%2F%2Fgit.dubzland.net)](https://git.dubzland.net/jdubz/dubzland-redis/pipelines)

Installs and configures Redis.

## Requirements

Ansible 2.2 or higher.

## Role Variables

Available variables are listed below, along with their default values (see
    `defaults/main.yml` for more info):

### dubzland_redis_supervised

```yaml
dubzland_redis_supervised: 'no'
```

Whether or not Redis is managed by Upstart/Systemd.

### dubzland_redis_loglevel/dubzland_redis_logfile

```yaml
dubzland_redis_loglevel: 'notice'
dubzland_redis_logfile: '/var/log/redis/redis-server.log'
```

Log level and file to use for output.

###
dubzland_redis_syslog_enabled/dubzland_redis_syslog_ident/dubzland_redis_syslog_facility

```yaml
dubzland_redis_syslog_enabled: 'no'
dubzland_redis_syslog_ident: 'redis'
dubzland_redis_syslog_facility: 'local0'
```

Controls for output to syslog/journald

### dubzland_redis_bind_ip/dubzland_redis_port

```yaml
dubzland_redis_bind_ip: '127.0.0.1'
dubzland_redis_port: 6379
```

IP address and port to listen for connections.

### dubzland_redis_tcp_backlog

```yaml
dubzland_redis_tcp_backlog: 511
```

Maximum connections possible in the completed connections queue.

### dubzland_redis_tcp_keepalive

```yaml
dubzland_redis_tcp_keepalive: 300
```

Time (in seconds) between ACKs for SO_KEEPALIVE

### dubzland_redis_unix_socket/dubzland_redis_unix_socket_perm

```yaml
dubzland_redis_unix_socket: ''
dubzland_redis_unix_socket_perm: 700
```

Local socket used for communication with clients, along with permissions to set
on the socket file.

### dubzland_redis_timeout

```yaml
dubzland_redis_timeout: 0
```

Number of seconds to wait before closing client connections with no activity
(`0` means never).

### dubzland_redis_databases

```yaml
dubzland_redis_databases: 16
```

Maximum number of databases to allow.

### dubzland_redis_save

```yaml
  - '900 1'
  - '300 10'
  - '60 10000'
```

Configures Redis snapshotting.  Each line specifies the number of seconds followed by the number of write operations that must have occurred before saving to disk.  For example, `300 10` means that every 300 seconds, if at least 10 write operations have occurred, save to disk.  Set to an empty list to disable saving to disk.

### dubzland_redis_stop_writes_on_bgsave_error

```yaml
dubzland_redis_stop_writes_on_bgsave_error: 'yes'
```

Signal failure to clients when Redis is unable to save the DB to disk.

### dubzland_redis_rdbcompression

```yaml
dubzland_redis_rdbcompression: 'yes'
```

Whether or not Redis should compress the database (using LZF) on save.

### dubzland_redis_rdbchecksum

```yaml
dubzland_redis_rdbchecksum: 'yes'
```

Whether or not Redis should append a CRC64 checksum of the database on save.

### dubzland_redis_dbfilename

```yaml
dubzland_redis_dbfilename: 'dump.rdb'
```

Filename used to store the Redis database on save.

### dubzland_redis_dbdir

```yaml
dubzland_redis_dbdir: '/var/lib/redis'
```

Directory where the database file will be stored.

### dubzland_redis_maxclients

```yaml
dubzland_redis_maxclients: 10000
```

Maximum number of concurrently connected clients.

### dubzland_redis_maxmemory

```yaml
dubzland_redis_maxmemory: 0
```

Upper memory limit for in-memory storage.

### dubzland_redis_maxmemory_policy

```yaml
dubzland_redis_maxmemory_policy: 'noeviction'
```

How Redis will react when the maximum memory limit has been reached (`noevicition` instructs Redis to return an error to the client).

### dubzland_redis_maxmemory_samples

```yaml
dubzland_redis_maxmemory_samples: 5
```

Number of samples to take when considering eviction.

### dubzland_redis_appendonly

```yaml
dubzland_redis_appendonly: 'no'
```

Instructs Redis to utilize an Append Only File for writes (appends writes instead of writing the entire db).  This is not mutually exclusive with RDB.

### dubzland_redis_appendfsync

```yaml
dubzland_redis_appendfsync: 'everysec'
```

Indicates how Redis should handle `fsync` on the AOF file.

### dubzland_redis_includes

```yaml
dubzland_redis_includes: []
```

List of additional files to include for overriding Redis behavior.

### dubzland_redis_disabled_commands

```yaml
dubzland_redis_disabled_commands: []
```

Redis commands to be disabled (for additional security).

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: dubzland-git
```

## License

MIT

## Author

* [Josh Williams](https://codingprime.com)
