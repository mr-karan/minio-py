# Minio Python Library for Amazon S3 Compatible Cloud Storage [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/Minio/minio?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

The Minio Python Client SDK provides simple APIs to access any Amazon S3 compatible object storage server.

This quickstart guide will show you how to install the client SDK and execute an example python program. For a complete list of APIs and examples, please take a look at the [Python Client API Reference](https://docs.minio.io/docs/python-client-api-reference) documentation.

This document assumes that you have a working [Python](https://www.python.org/downloads/) setup in place.

## Download from pip

```sh

$ pip install minio

```

## Download from source

```sh

$ git clone https://github.com/minio/minio-py
$ cd minio-py
$ python setup.py install

```

## Initialize Minio Client

You need four items in order to connect to Minio object storage server.

| Params     | Description |  
| :------- | :---- |  
| endpoint | URL to object storage service. |  
| access_key| Access key is like user ID that uniquely identifies your account.   |   
| secret_key| Secret key is the password to your account.    |
|secure|Set this value to 'True' to enable secure (HTTPS) access.|

```python

from minio import Minio
from minio.error import ResponseError

minioClient = Minio('play.minio.io:9000',
                  access_key='Q3AM3UQ867SPQQA43P2F',
                  secret_key='zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG',
                  secure=True)

```


## Quick Start Example - File Uploader
This example program connects to a Minio object storage server, makes a bucket on the server and then uploads a file to the bucket.

We will use the Minio server running at [https://play.minio.io:9000](https://play.minio.io:9000) in this example. Feel free to use this service for testing and development. Access credentials shown in this example are open to the public.

#### file-uploader.py

```python 

# Import Minio library.
from minio import Minio
from minio.error import ResponseError

# Initialize minioClient with an endpoint and access/secret keys.
minioClient = Minio('play.minio.io:9000',
                    access_key='Q3AM3UQ867SPQQA43P2F',
                    secret_key='zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG',
                    secure=True)

# Make a bucket with the make_bucket API call.
try:
       minioClient.make_bucket("maylogs", location="us-east-1")
except ResponseError as err:
       print(err)
else:
        # Put an object 'pumaserver_debug.log' with contents from 'pumaserver_debug.log'.
        try:
               minioClient.fput_object('maylogs', 'pumaserver_debug.log', '/tmp/pumaserver_debug.log')
        except ResponseError as error:
               print(error)
 
```

#### Run file-uploader

```bash

$ python file_uploader.py

$ mc ls play/maylogs/
[2016-05-27 16:41:37 PDT]  12MiB pumaserver_debug.log

```

## API Reference

The full API Reference is available here. 
* [Complete API Reference](https://docs.minio.io/docs/python-client-api-reference)

### API Reference : Bucket Operations

* [`make_bucket`](https://docs.minio.io/docs/python-client-api-reference#make_bucket)
* [`list_buckets`](https://docs.minio.io/docs/python-client-api-reference#list_buckets)
* [`bucket_exists`](https://docs.minio.io/docs/python-client-api-reference#bucket_exists)
* [`remove_bucket`](https://docs.minio.io/docs/python-client-api-reference#remove_bucket)
* [`list_objects`](https://docs.minio.io/docs/python-client-api-reference#list_objects)
* [`list_incomplete_uploads`](https://docs.minio.io/docs/python-client-api-reference#list_incomplete_uploads)

### API Reference : File Object Operations

* [`fput_object`](https://docs.minio.io/docs/python-client-api-reference#fput_object)
* [`fget_object`](https://docs.minio.io/docs/python-client-api-reference#fget_object)

### API Reference : Object Operations

* [`get_object`](https://docs.minio.io/docs/python-client-api-reference#get_object)
* [`put_object`](https://docs.minio.io/docs/python-client-api-reference#put_object)
* [`stat_object`](https://docs.minio.io/docs/python-client-api-reference#stat_object)
* [`remove_object`](https://docs.minio.io/docs/python-client-api-reference#remove_object)
* [`remove_incomplete_upload`](https://docs.minio.io/docs/python-client-api-reference#remove_incomplete_upload)
* [`get_partial_object`](https://docs.minio.io/docs/python-client-api-reference#get_partial_object)

### API Reference : Presigned Operations

* [`presigned_get_object`](https://docs.minio.io/docs/python-client-api-reference#presigned_get_object)
* [`presigned_put_object`](https://docs.minio.io/docs/python-client-api-reference#presigned_put_object)
* [`presigned_post_policy`](https://docs.minio.io/docs/python-client-api-reference#presigned_post_policy)

## Full Examples

#### Full Examples : Bucket Operations

* [list_buckets.py](./examples/list_buckets.py)
* [list_objects.py](./examples/list_objects.py)
* [bucket_exists.py](./examples/bucket_exists.py)
* [make_bucket.py](./examples/make_bucket.py)
* [remove_bucket.py](./examples/remove_bucket.py)
* [list_incomplete_uploads.py](./examples/list_incomplete_uploads.py)
* [remove_incomplete_upload.py](./examples/remove_incomplete_upload.py)

#### Full Examples : File Object Operations

* [fput_object.py](./examples/fput_object.py)
* [fget_object.py](./examples/fget_object.py)

#### Full Examples : Object Operations

* [put_object.py](./examples/put_object.py)
* [get_object.py](./examples/get_object.py)
* [get_partial_object.py](./examples/get_partial_object.py)
* [remove_object.py](./examples/remove_object.py)
* [stat_object.py](./examples/stat_object.py)

#### Full Examples : Presigned Operations

* [presigned_get_object.py](./examples/presigned_get_object.py)
* [presigned_put_object.py](./examples/presigned_put_object.py)
* [presigned_post_policy.py](./examples/presigned_post_policy.py)

## Explore Further

* [Complete Documentation](https://docs.minio.io)
* [Minio Python SDK API Reference](https://docs.minio.io/docs/python-client-api-reference) 

## Contribute

[Contributors Guide](./CONTRIBUTING.md)

[![PYPI](https://img.shields.io/pypi/v/minio.svg)](https://pypi.python.org/pypi/minio)
[![Build Status](https://travis-ci.org/minio/minio-py.svg)](https://travis-ci.org/minio/minio-py)
[![Build status](https://ci.appveyor.com/api/projects/status/1d05e6nvxcelmrak?svg=true)](https://ci.appveyor.com/project/harshavardhana/minio-py)
