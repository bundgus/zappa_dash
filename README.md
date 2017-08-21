#A [Dash example](https://plot.ly/dash/getting-started) deployed to AWS Lambda and API Gateway using [Zappa](https://github.com/Miserlou/Zappa)
Example at [https://bundgus-dash-example.bundgus.com/]('https://bundgus-dash-example.bundgus.com/])
---

##AWS Setup

* Domain Configuration
    * Register and host domain using Route 53
        * [AWS Route 53 console](https://console.aws.amazon.com/route53)
        * [AWS Docs: Working with Resource Record Sets](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html?ref_=pe_1764230_134333060)
        * cost:
            * registration cost for .com domain : $12 / year
            * DNS hosting cost : $0.50 / month
* Provision TLS Certificate
    * [AWS Certificate Manager console](https://aws.amazon.com/certificate-manager)
    * [AWS blog entry](https://aws.amazon.com/blogs/aws/new-aws-certificate-manager-deploy-ssltls-based-apps-on-aws/)
    * cost : free
* Create S3 Bucket
    * [AWS S3 console](https://s3.console.aws.amazon.com/s3)
    * cost:
        * S3 storage cost : First 50 TB / month	$0.023 per GB
        * S3 request cost : PUT, COPY, POST, or LIST Requests $0.005 per 1,000 requests
        * S3 request cost : GET and all other Requests	$0.004 per 10,000 requests
        * S3 data transfer cost : 
            * First 1 GB / month $0.000 per GB
            * Up to 10 TB / month $0.090 per GB


Make sure you are running Python 3.6 and you have a valid AWS account and your [AWS credentials file is properly installed](https://blogs.aws.amazon.com/security/post/Tx3D6U6WSFGOK2H/A-New-and-Standardized-Way-to-Manage-Credentials-in-the-AWS-SDKs).

##Create Python Virtual Environment

```
cd ~/.virtualenv
virtualenv -p /usr/bin/python3.6 lambda-dash-env
source lambda-dash-env/bin/activate
pip install -r requirements.txt
```

```
zappa deploy        
zappa certify
zappa status
```

* AWS Cloudfront
    * cost:
        * Data transfer (GB) First 10 TB / month $0.085
        * HTTPS requests per 10,000	$0.0100

* AWS Lambda
    * cost:
        * The Lambda free tier includes 1M free requests per month and 400,000 GB-seconds of compute time per month.
        * $0.20 per 1 million requests thereafter ($0.0000002 per request)
        * $0.00001667 for every GB-second used 
            * Memory 512MB, 800,000 free tier seconds per month, price per 100 ms: $0.000000834
        

Status: follow the progress on this issue: [https://github.com/plotly/dash/issues/22](https://github.com/plotly/dash/issues/22)