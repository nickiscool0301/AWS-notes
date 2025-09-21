# EBS

## Encrypt

- We cannot encrypt an existing unencrypted volume
  - Create a snapshot of the volume
  - Encrypt the snapshot
  - Create a new volume from the encrypted snapshot
  - Attach the new volume to the instance
