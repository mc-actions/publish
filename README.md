# Publish folder to S3

Use `mc` CLI to upload file or folder to s3 storage. Check out [`mc-actions/configure` docs](https://github.com/marketplace/actions/minio-cli-configure-action) to find out how to set up your s3 storage provider.

## Examples

Upload `static` folder of your repo to the root of `mybucket` bucket on server `https://minio.compny`:

```yaml
steps:
- name: Checkout repository
  uses: actions/checkout@v4
- name: Confugure S3 client
  uses: mc-actions/configure@v1
  with:
    s3_server: 'https://minio.compny'
    s3_access_key: '${{ secrets.S3_ACCESS_KEY }}'
    s3_secret_key: '${{ secrets.S3_SECRET_KEY }}'
- name: Publish repository
  uses: mc-actions/publish@v1
  with:
    from: './static'
    server_bucket: 'mybucket'
```

## Action inputs

The following action inputs are available to configure `mc`:

| Name           | description                                                                                                                                                          | Example           |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| `server_alias` | Any string <br/> Optional, default `default` <br/><br/> Name of server to use in CLI. Do not edit if you will use other [mc-actions](https://github.com/mc-actions). | `play`            |
| `s3_bucket`    | Any string <br/> Required <br/><br/> Name of bucket to store files in                                                                                                | `mybucket`        |
| `from`         | Any string <br/> Required <br/><br/> Path to file or folder to upload                                                                                                | `./dist`          |
| `to`           | Any string <br/> Optional, default root of bucket <br/><br/> Where to store document in `/absolute/path/to/folder` format                                            | `/path/to/folder` |
