## Serverless for Beginners

### Lab 1: Creating a serverless transcoding pipeline in AWS

- **Create two S3 Buckets**
  - one for video mp3 files
  - one for transcoded files
- **Create Event-Driven Lambda function**
  - When mp3 is added to bucket, trigger lambda function
  - lambda function creates three transcoded variants
  - lambda adds files to transcoded bucket

### Lab 2: Setup website and authenticate user w/ Auth0

- **Create Auth0 Account**
