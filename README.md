<<<<<<< HEAD
# CloudLaunch

## Task 1 – S3 Static Website
- Created S3 bucket: cloudlaunch-site-bucket.
- Enabled *static website hosting*.
- Uploaded HTML/CSS/JS files.
- Configured bucket policy for public read access.
- (Optional) Deployed CloudFront for HTTPS and caching.

- *S3 Website URL:*
  http://mycloudlaunch-site-bucket.s3-website-eu-west-1.amazonaws.com

---

## Task 2 – IAM Least Privilege
- Created three buckets:
  - alt-school-cloudlaunch-private-bucket
  - mycloudlaunch-site-bucket
  - cloudlaunch-visible-only-bucket2
- Designed and attached a *custom IAM policy* with:
  - ListBucket on all three buckets.
  - GetObject + PutObject on cloudlaunch-private-bucket.
  - GetObject only on cloudlaunch-site-bucket.
  - ❌ No DeleteObject anywhere.
  - ❌ No object access to cloudlaunch-visible-only-bucket.

---

## IAM Policy JSON

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ListAllThreeBuckets",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": [
        arn:aws:s3:::alt-school-cloudlaunch-private-bucket,
        arn:aws:s3:::cloudlaunch-visible-only-bucket2,
        arn:aws:s3:::mycloudlaunch-site-bucket"
      ]
    },
    {
      "Sid": "PrivateBucketReadWriteNoDelete",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::cloudlaunch-private-bucket/*"
    },
    {
      "Sid": "SiteBucketReadOnly",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::cloudlaunch-site-bucket/*"
    }
  ]
}
>>>>>>> 9222344 (first commit)
