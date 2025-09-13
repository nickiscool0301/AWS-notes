# Sign URLs and Cookies

- Use signed URLs and signed cookies to control access to content.

## CloudFront Key Pairs

- create signed URLS ans signed cookies
- Only AWS account root user can manage CloudFront key pairs
- Each account can have up to 2 ACTIVE key pairs
- Key pairs:
  - Public key: CF uses to verify URL signatures
  - Private key: user use to sign URLS
- Cannot use IAM roles to manage CF key pairs

## Step

- Root user creates key pair in AWS console
- Download .pem file (private key)
- Upload public key to CF
- Associate public key with trusted signer (AWS account or CloudFront OAI)
