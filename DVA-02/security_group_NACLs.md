# Security Group

- SG is stateful
- Allowing inbound traffic automatically allows the response outbound traffic
- By default, SG denies all inbound traffic and allows all outbound traffic
- Can only allow rules, cannot create deny rules

# Network ACLs

- NACL is stateless
- Must create rules to allow both inbound and outbound traffic
- By default, NACL allows all inbound and outbound traffic
- Can create both allow and deny rules
- Each rule has a number, lower number has higher priority
- If no rule matches, the default action is to deny
