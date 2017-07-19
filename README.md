# Static Site sample

### SSL

Both staging and production apps redirect http to https and have SSL enabled. The apps are delivered using two separate AWS Cloudfront CDNs, one for production and one for staging.

This website is generated using Jekyll. After a successful CI run passes, the app will automatically be built and uploaded to an Amazon S3 bucket. Additionally, a cache invalidation on the appropriate Cloudfront distribution will also be triggered.

***Note that a cache invalidation must be triggered for new change in the S3 bucket to show up for all users. An invalidation can be manually triggered through the AWS console if the automatic trigger fails. Invalidating `/*` means that the cache for all files in the S3 bucket will be invalidated***

The settings for this deployment can be seen in `circle.yml`. We are using CircleCI for continuous integration. In the `deployment` block, settings for the S3 upload and cache invalidation are listed there.

Detailed steps for Cloudfront and S3 HTTPS support:
- static files uploaded to S3
- enable website hosting on the S3 bucket
- create a Cloudfront CDN distribution XXXXXX.cloudfront.net
- in the distribution add the S3 bucket URL
- redirect all HTTP traffic to HTTPS for Cloudfront and choose a proper SSL certificate (use Amazon ACM to generate one as appropriate)
- Add domain to list of CNAME records in Cloudfront for that distribution
- Add a CNAME record *.domain.com to the cloudfront URL: XXXXXX.cloudfront.net
