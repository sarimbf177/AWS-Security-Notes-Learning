**CloudFront Authorization Header**
. It is used to forward the authorization header to the origin.
. Cache policy is set up for this on cloudfront and authorization header is whitelisted.
Note: This can be used for all the origin types except S3 origin.


**CloudFront - Restric ALB Access**
. Cloudfront can be used to restrict the ALB access by adding a custom header to the request.
_How it works:_
. When a user sends a request, it goes to the cloudfront edge location. CloudFront adds a custom header to the request then sends to the ALB. 
. ALB checks the custom header filter and if it works then the request is processed. 
. On top of this, a restriction on the ALB SG can be set up to allow only the CloudFront prefix IPs mentioned on the AWS CloudFront IPs list online.


**CloudFront - Integration with Cognito**
. Cognito can be integrated with Cloudfront.

_How it works:_
1. User Authenticates with Cognito. 
2. Cognito sends back the JWT (JSON Web Token) to the user.
3. User request is then sent to the CloudFront along with the JWT Token.For e.g: GET/private/image.jpeg + JWT Token.
4. CloudFront sends the JWT Token to lambda. 
5. Lambda@Edge is set up to verify the JWT Token with cognito.  
6. If the verification is successful, Lambda sends back the OK status to CloudFront and then the request is processed.