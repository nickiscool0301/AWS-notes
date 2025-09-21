# AWS KMS (Key Management Service)

## What is KMS?
- Managed service for encryption keys
- Creates and controls encryption keys used to encrypt data
- Integrated with most AWS services

## Key Types

### Customer Managed Keys (CMK)
- You create, own, and manage
- Can enable/disable, rotate, delete
- Cost: $1/month per key + usage
- If you want cross-account encryption, you must use SSE-KMS with customer managed CMKs, not AWS managed keys

### AWS Managed Keys
- Created/managed by AWS services
- Free to use
- Automatic rotation every year
- Cannot delete or manage directly

### AWS Owned Keys
- Used by AWS services internally
- No additional cost
- Not visible in your account

## Key Operations

### Encrypt
- Encrypt data up to 4KB directly
- Returns ciphertext

### Decrypt
- Decrypt ciphertext
- Must have permission to use the key

### GenerateDataKey
- Creates data encryption key (DEK)
- Returns plaintext + encrypted version
- Use plaintext to encrypt, store encrypted version

### GenerateDataKeyWithoutPlaintext
- Returns only encrypted data key
- Use with Decrypt to get plaintext key

## Envelope Encryption
- Encrypt data with Data Encryption Key (DEK)
- Encrypt DEK with KMS Customer Master Key (CMK)
- Store encrypted data + encrypted DEK together
- Decrypt: Use KMS to decrypt DEK, then decrypt data

## Key Policies
- JSON-based access control
- Similar to IAM policies
- Default policy gives root user full access
- Can grant cross-account access

## Multi-Region Keys
- Same key ID across multiple regions
- Replicated automatically
- Each region has independent key material
- Useful for global applications

## Key Rotation
- Automatic rotation available for CMKs
- Rotates every year
- Old key versions remain available for decryption
- Cannot rotate imported key material

## Important Limits
- 4KB max data size for direct encryption
- Regional service
- API request limits apply
- Key policies max 32KB

## Common Use Cases
- EBS volume encryption
- S3 bucket encryption
- RDS encryption
- Lambda environment variables
- Parameter Store SecureString
- Secrets Manager

## Best Practices
- Use least privilege access
- Enable key rotation
- Monitor key usage with CloudTrail
- Use separate keys for different applications
- Consider cross-region replication needs