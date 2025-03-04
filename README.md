# Postgres S3 backups

A slightly moidified version of [railway/postgres-s3-backups](https://github.com/railwayapp-templates/postgres-s3-backups) to backup your PostgreSQL database to S3 via a cron.

Upgraded to Node 22 and Postgres 17 by default and with fixed support for Backblaze B2 and Cloudflare R2.

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/template/eIOwd0?referralCode=h-EWY1)

## Configuration

- `AWS_ACCESS_KEY_ID` - AWS access key ID.

- `AWS_SECRET_ACCESS_KEY` - AWS secret access key, sometimes also called an application key.

- `AWS_S3_BUCKET` - The name of the bucket that the access key ID and secret access key are authorized to access.

- `AWS_S3_REGION` - The name of the region your bucket is located in, set to `auto` if unknown.

- `BACKUP_DATABASE_URL` - The connection string of the database to backup.

- `BACKUP_CRON_SCHEDULE` - The cron schedule to run the backup on. Example: `0 5 * * *`

- `AWS_S3_ENDPOINT` - The S3 custom endpoint you want to use. Applicable for 3-rd party S3 services such as Cloudflare R2 or Backblaze R2.

- `AWS_S3_FORCE_PATH_STYLE` - Use path style for the endpoint instead of the default subdomain style, useful for MinIO. Default `false`

- `RUN_ON_STARTUP` - Run a backup on startup of this application then proceed with making backups on the set schedule.

- `BACKUP_FILE_PREFIX` - Add a prefix to the file name.

- `BUCKET_SUBFOLDER` - Define a subfolder to place the backup files in.

- `SINGLE_SHOT_MODE` - Run a single backup on start and exit when completed. Useful with the platform's native CRON schedular.

- `SUPPORT_OBJECT_LOCK` - Enables support for buckets with object lock by providing an MD5 hash with the backup file.

- `BACKUP_OPTIONS` - Add any valid pg_dump option, supported pg_dump options can be found [here](https://www.postgresql.org/docs/current/app-pgdump.html). Example: `--exclude-table=pattern`

- `DISABLE_S3_CHECKSUM_VALIDATION` - Disables default S3 request checksum validation which is [not supported](https://github.com/aws/aws-sdk-js-v3/issues/6810) by some S3 providers like [Backblaze B2](https://www.backblaze.com/docs/cloud-storage-s3-compatible-api#unsupported-features) and [Cloudflare R2](https://developers.cloudflare.com/r2/api/s3/api/). This only impacts the communication between the application and the S3 service, not the backup itself.

- `NODE_VERSION` - The Node version to use for the build stage. Default `22.14.0`

- `PG_VERSION` - The Postgres version to use for the build stage. Default `17`