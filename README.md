# Secure Multi-Tier AWS Infrastructure

A portfolio lab demonstrating a multi-tier AWS architecture, secure network segmentation, managed database connectivity, operational monitoring, auditing, and security hardening in **US West (N. California), `us-west-1`**.

> **Lab note:** This is a learning environment. HTTP is currently used for the ALB demonstration. HTTPS, further IAM improvements, and additional audit coverage remain planned. Review AWS pricing and clean up billable resources when the lab is not in use.

## Architecture

- VPC with public, private application, and private database subnets across two Availability Zones.
- Internet-facing Application Load Balancer in public subnets.
- Auto Scaling application instances in private subnets.
- Amazon RDS MySQL in private DB subnets.
- NAT Gateway for private application-tier outbound access.
- AWS Systems Manager Session Manager for instance administration, without public SSH.
- CloudWatch alarms and SNS email notifications.
- Multi-region CloudTrail management-event logging.

See [`docs/architecture.md`](docs/architecture.md).

## Security controls

- App-tier inbound traffic restricted to the ALB security group on TCP/80.
- DB inbound MySQL TCP/3306 restricted to the application security group.
- Application instances have no public IP addresses.
- SSM access through an EC2 instance role.
- RDS is private and encrypted using an AWS-managed KMS key.
- CloudTrail log-file validation enabled.
- CloudWatch alarms connected to an SNS email topic.

## Security audit and remediation

See [`docs/security-audit.md`](docs/security-audit.md) and [`docs/remediation-log.md`](docs/remediation-log.md).

## Monitoring

See [`docs/monitoring-and-alerting.md`](docs/monitoring-and-alerting.md).

## Evidence

Add redacted screenshots to `screenshots/` as you collect evidence. Do not commit credentials, secrets, sensitive personal information, or unredacted account-sensitive details.

## Cost considerations

NAT Gateway, ALB, RDS, CloudWatch, CloudTrail storage, and other services may incur charges. Check the AWS Billing console and shut down or delete resources when the lab is paused, following a deliberate cleanup plan.
