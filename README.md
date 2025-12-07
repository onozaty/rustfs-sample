# rustfs-sample

RustFSを動作確認するためのサンプルです。

- [rustfs/rustfs: 🚀2\.3x faster than MinIO for 4KB object payloads\. RustFS is an open\-source, S3\-compatible high\-performance object storage system supporting migration and coexistence with other S3\-compatible platforms such as MinIO and Ceph\.](https://github.com/rustfs/rustfs)

## RustFSへのアクセス方法

DevContainer内からは``http://rustfs:9000``(S3 API)と``http://rustfs:9001``(Webコンソール)でアクセスできます。  
ホストからは``http://localhost:9000``/``9001``を使ってください。

## AWS CLI

### 準備

```bash
export AWS_ACCESS_KEY_ID=rustfsadmin
export AWS_SECRET_ACCESS_KEY=rustfsadmin
```

### List Buckets

```
aws --endpoint-url=http://rustfs:9000 s3 ls
```

```
$ aws --endpoint-url=http://rustfs:9000 s3 ls
2025-12-07 14:08:22 sample-bucket
```

### Upload

```
aws --endpoint-url=http://rustfs:9000 s3 cp README.md s3://sample-bucket/README.md
```

```
$ aws --endpoint-url=http://rustfs:9000 s3 cp README.md s3://sample-bucket/README.md
upload: ./README.md to s3://sample-bucket/README.md           
```

### List Objects

```
aws --endpoint-url=http://rustfs:9000 s3 ls s3://sample-bucket/
```

```
$ aws --endpoint-url=http://rustfs:9000 s3 ls s3://sample-bucket/
2025-12-07 23:07:20        363 README.md
```

### Generate Pre-signed URL

```
aws --endpoint-url=http://rustfs:9000 s3 presign s3://sample-bucket/README.md --expires-in 3600
```

```
$ aws --endpoint-url=http://rustfs:9000 s3 presign s3://sample-bucket/README.md --expires-in 3600
http://rustfs:9000/sample-bucket/README.md?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=rustfsadmin%2F20251207%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20251207T231531Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=c6dfcdaecb842d070885f204441f9f220e2bbb77a80d6e69eef4c05e835c1f4e

$ curl "http://rustfs:9000/sample-bucket/README.md?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=rustfsadmin%2F20251207%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20251207T231531Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=c6dfcdaecb842d070885f204441f9f220e2bbb77a80d6e69eef4c05e835c1f4e"
```
