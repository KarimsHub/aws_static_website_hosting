# AWS: Static Website Hosting on S3 with Cloudfront SSL

## Important steps to follow:
1. Load node.js and npm package for webpage Frontend
2. use npx create-react-app to execute the package for a deafult react app
3. npm start for launching the webpage on localhost:3000 to check if everything works fine and close process afterwards
4. In AWS console create two identical buckets in us-east1 (important because in every other AZ cloudfront wont work for static websites), one with www.sitename.com and one without (sitename.com) for redirecting users.
5. add files to the www. bucket. Files from "build" folder and the whole "static" folder
6. Permissions: unblock public in www. bucket + add bucket policy (change Resource!):
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}

7. Enable static website hosting on www. bucket (under Properties)
8. Enable redirect to https in none www. bucket (under Properties)
9. Open Route 53 to create a DNS for your website
10. Afterwards create records for both buckets. Create a Simple A record for wwww.sitename.com, pick S3 as an endpoint and choose the region the bucket was created in first place
11. Do the same for the none www. one
### For SSL Connection:
12. Open Certificate Manager in AWS to request an SSL Certificate
13. After that go to Cloudfront and create a distribution for the www. For origin domain you have to go to S3 an take the URL from the static website hosting in the bottom. Also change the Viewer Protocol Policy to Redirect HTTP to HTTPS. Furthermore you have to put the URL of the website in the "Alternate domain name" field and choose the ustom SSL certificate (which must be in us east1).
14. Change the A Records from both buckets in Route 53 to the Cloudfront Distribution




![ImgName](https://github.com/KarimsHub/Doubly_linked_list_datastructure/blob/master/sllvsdll.jpg?raw=true)

