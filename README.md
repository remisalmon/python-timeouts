# Python Timeouts

An unresponsive service can be worse than a down one. It can tie up your entire system if not handled properly. **All network requests should have a timeout.**

Here’s how to add timeouts for popular Python packages. **[All have been tested](tests)**. The default is no timeout, unless otherwise specified. Enjoy!

[![Build Status](https://github.com/ankane/python-timeouts/workflows/build/badge.svg?branch=master)](https://github.com/ankane/python-timeouts/actions)

## Packages

Standard library

- [ftplib](#ftplib)
- [http](#http)
- [imaplib](#imaplib)
- [nntplib](#nntplib)
- [poplib](#poplib)
- [smtplib](#smtplib)
- [socket](#socket)
- [subprocess](#subprocess)
- [telnetlib](#telnetlib)

PyPI

- [aiohttp](#aiohttp)
- [asyncpg](#asyncpg)
- [boto3](#boto3)
- [cassandra-driver](#cassandra-driver)
- [elasticsearch](#elasticsearch)
- [httpx](#httpx)
- [mongoengine](#mongoengine)
- [mysqlclient](#mysqlclient)
- [opensearch-py](#opensearch-py)
- [psycopg](#psycopg)
- [psycopg2](#psycopg2)
- [pymemcache](#pymemcache)
- [pymongo](#pymongo)
- [redis](#redis)
- [requests](#requests)
- [SQLAlchemy](#SQLAlchemy)
- [trino](#trino)
- [typesense](#typesense)

## Standard Library

### ftplib

```python
FTP(host, timeout=1)
```

Raises `socket.timeout`

### http

```python
HTTPConnection(host, port, timeout=1)
```

Raises `socket.timeout`

### imaplib

```python
IMAP4(host, timeout=1)
```

Raises `socket.timeout`

### nntplib

```python
NNTP(host, timeout=1)
```

Raises `socket.timeout`

### poplib

```python
POP3(host, timeout=1)
```

Raises `socket.timeout`

### smtplib

```python
SMTP(host, timeout=1)
```

Raises

- `socket.timeout` on connect timeout
- `smtplib.SMTPServerDisconnected` on read timeout

### socket

```python
sock.settimeout(1)
```

Raises `socket.timeout`

### subprocess

```python
subprocess.run(cmd, timeout=1)
```

Raises `subprocess.TimeoutExpired`

### telnetlib

```python
Telnet(host, timeout=1)
```

Raises `socket.timeout`

## PyPI

### aiohttp

```python
timeout = aiohttp.ClientTimeout(total=1)
async with aiohttp.ClientSession(timeout=timeout) as session:
    # ...
```

Raises `asyncio.exceptions.TimeoutError`

### asyncpg

```python
asyncpg.connect(timeout=1)
```

Default: 60s

Raises `asyncio.exceptions.TimeoutError`

### boto3

```python
boto3.client('s3', config=Config(connect_timeout=1, read_timeout=1))
```

Raises

- `botocore.exceptions.ConnectTimeoutError` on connect timeout
- `botocore.exceptions.ReadTimeoutError` on read timeout

### cassandra-driver

```python
Cluster([host], connect_timeout=1)
```

Raises `cassandra.cluster.NoHostAvailable` on connect timeout

### elasticsearch

```python
Elasticsearch(timeout=1)
```

Raises `elasticsearch.exceptions.ConnectionError`

### httpx

```python
httpx.get(url, timeout=1)
# or
httpx.Client(timeout=1)
```

Raises

- `httpx.ConnectTimeout` on connect timeout
- `httpx.ReadTimeout` on read timeout

### mongoengine

```python
connect(connectTimeoutMS=1000, socketTimeoutMS=1000, serverSelectionTimeoutMS=1000)
```

Raises `pymongo.errors.ServerSelectionTimeoutError`

### mysqlclient

```python
MySQLdb.connect(connect_timeout=1)
```

Raises `MySQLdb._exceptions.OperationalError`

### opensearch-py

```python
OpenSearch(timeout=1)
```

Raises `opensearchpy.exceptions.ConnectionError`

### psycopg

```python
psycopg.connect(connect_timeout=1)
```

Raises `psycopg.OperationalError`

### psycopg2

```python
psycopg2.connect(connect_timeout=1)
```

Raises `psycopg2.OperationalError`

### pymemcache

```python
Client(host, connect_timeout=1, timeout=1)
```

Raises `socket.timeout`

### pymongo

```python
MongoClient(connectTimeoutMS=1000, socketTimeoutMS=1000, serverSelectionTimeoutMS=1000)
```

Default: 20s connect timeout, 30s server selection timeout

Raises `pymongo.errors.ServerSelectionTimeoutError`

### redis

```python
Redis(socket_connect_timeout=1, socket_timeout=1)
```

Raises `redis.exceptions.TimeoutError`

### requests

```python
requests.get(url, timeout=1)
```

Raises

- `requests.exceptions.ConnectTimeout` on connect timeout
- `requests.exceptions.ReadTimeout` on read timeout

### SQLAlchemy

```python
create_engine(url, connect_args={'connect_timeout': 1})
```

Raises `sqlalchemy.exc.OperationalError`

### trino

```python
trino.dbapi.connect(request_timeout=1)
# or
trino.dbapi.connect(request_timeout=(1, 1)) # (connect, read)
```

Raises

- `requests.exceptions.ConnectTimeout` on connect timeout
- `requests.exceptions.ReadTimeout` on read timeout

### typesense

```python
Client({'connection_timeout_seconds': 1})
```

Raises

- `requests.exceptions.ConnectTimeout` on connect timeout
- `requests.exceptions.ReadTimeout` on read timeout

## Don’t see a library you use?

[Let us know](https://github.com/ankane/python-timeouts/issues/new). Even better, [create a pull request](https://github.com/ankane/python-timeouts/pulls) for it.

## Running the Tests

```sh
git clone https://github.com/ankane/python-timeouts.git
cd python-timeouts
pip install -r requirements.txt
```

To run all tests, use:

```sh
pytest
```

To run individual tests, use:

```sh
pytest tests/test_redis.py
```
