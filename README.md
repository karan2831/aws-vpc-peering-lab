# AWS VPC Peering Lab

A hands-on AWS networking lab demonstrating VPC peering, reciprocal route-table configuration, subnet/route-table associations, security-group rules, and private-IP connectivity validation.

## Lab objectives

- Configure two VPCs with non-overlapping IPv4 CIDR ranges.
- Create subnets and review route-table associations.
- Establish an active VPC peering connection.
- Add reciprocal routes for the peer VPC CIDR.
- Configure security-group rules for controlled ICMP and SSH testing.
- Validate connectivity and document the results.

## Architecture

| Resource | CIDR / Address | Purpose |
|---|---|---|
| VPC A — `ewb-vpc-a` | `10.10.0.0/16` | Source/test VPC |
| VPC B — `ewb-vpc-b` | `10.20.0.0/16` | Peer/target VPC |
| VPC A public subnet | `10.10.1.0/24` | Public test instance subnet |
| VPC A private subnet | `10.10.2.0/24` | Private subnet |
| VPC B private subnet | `10.20.1.0/24` | Target instance subnet |
| VPC B target instance | `10.20.1.172` | Private-IP connectivity target |

**AWS Region:** Mumbai (`ap-south-1`)

## Implementation overview

1. Created two VPCs with non-overlapping CIDR blocks.
2. Created the required subnets and reviewed route-table associations.
3. Established and activated VPC peering.
4. Added routes to the opposite VPC CIDR through the peering connection on both sides.
5. Configured security-group access for ICMP and SSH testing.
6. Tested connectivity to the target instance's private IP.

## Validation results

- **ICMP:** The lab's recorded ping test to `10.20.1.172` succeeded with 4/4 replies and 0% packet loss.
- **TCP/22 reachability:** A port reachability probe succeeded.
- **SSH authentication:** **Not verified.** The attempted SSH login returned a public-key permission error. Therefore, successful SSH login is not claimed.

## Evidence

Selected AWS console screenshots are in [`screenshots/`](screenshots/).

The detailed report, including methodology, results, troubleshooting notes, and screenshot evidence, is available in [`docs/`](docs/).

## Key learning

VPC peering alone does not automatically provide connectivity. The peering connection must be active, the relevant route tables on both sides must direct peer-CIDR traffic through the connection, and security controls must permit the intended traffic.

## Cost-control note

The lab's four EC2 instances were reported stopped after testing. Stopped instances may still have billable attached EBS volumes, snapshots, or allocated public IPv4 resources. Review AWS Billing and Cost Management and remove unused resources when finished.

## References

- [AWS: VPC peering basics](https://docs.aws.amazon.com/vpc/latest/peering/vpc-peering-basics.html)
- [AWS: Update route tables for VPC peering](https://docs.aws.amazon.com/vpc/latest/peering/vpc-peering-routing.html)

## Security note

Do not commit AWS access keys, private keys (`.pem`), passwords, session tokens, or other secrets. Review screenshots for account IDs and other information you do not want public before making the repository public.
