# cross-zone load balancing

- by default, load balancer routes traffic to all registered instances in all enabled AZs
- Eg: 2 AZs, 2 in Zone A, 8 in Zone B
  If no cross-zone load balancing:
- Zone A: each instance gets 50%/2 = 25%
- Zone B: each instance gets 50%/8 = 6.25%

If cross-zone load balancing enabled:

- Zone A: each instance gets 100%/10 = 10%
- Zone B: each instance gets 100%/10 = 10%

- cross-zone load balancing is enabled by default for Application Load Balancer
- cross-zone load balancing is disabled by default for Network Load Balancer
- cross-zone load balancing is not available for Classic Load Balancer
