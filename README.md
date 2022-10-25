# AWS to GCP migration | Rule of thumb | Important notes

## 📚 Foundation
- Understand the enterprise/business process, workflows, folders and users to create "IAM" hierarchy on GCP;
- Define labels (e.g.: prd -> production, env -> enviroment, etc);

## 📚 AWS S3 to GCP Cloud Storage
- Always consider the AWS S3 Outbound Data Transfer (avoid transfers between different continents to avoid higher costs);
- Always consider the GCP PUT/POST cost using GCP Data Transfer S3->Cloud Storage;
- Use AWS and GCP pricing calcualtor to estimate costs;
- https://calculator.aws/#/estimate
- https://cloud.google.com/products/calculator
- Always consider the AWS S3 Outbound Data Transfer (avoid transfers between different continents to avoid higher costs);
- Always consider the GCP PUT/POST cost using GCP Data Transfer S3->Cloud Storage;
- Double-check both S3/Cloud Storage data for full application cutover;

## 📚 VPN site-to-site AWS to GCP

```
Redundant VPN

From the Google side:

1) Create a Cloud Router with BGP ASN -> Add: peering/table network

2) Create a Cloud HA VPN Gateway with two IPs (interfaces)

7) Create a Peer VPN Gateway with 4 interfaces

8) Open the AWS VPNs dowload configuration files in 7), transcribe the Virtual Private Gateway in Outside IP Addresses in IPSec Tunnel #1 and #2 in the interfaces field and create

9) Click on Cloud VPN Gateways, on Add VPN Tunnel and select the Peer VPN Gateway

10) Create 4 VPN Tunnels (redundancy). Also place and select the Cloud Router

11) Fill in the Pre Shared Key from the configuration files downloaded from AWS and create

12) Create the BGP sessions by manually transcribing the Virtual Private Gateway into Inside IP Addresses in IPSec Tunnel #1 and #2 and with the AWS ASN

13) Check if the VPNs are UP on the GCP and AWS side by clicking on them

17) You can use the Google Newtork Intelligence Center tool to troubleshoot connectivity via VPN and/or Shared Networks


On the AWS side:

3) Create two Customer Gateway with BGP ASN and the two Google VPN interface IPs

4) Create a Virtual Private Gateway with different ASN than Google allocated

5) Create two Site-to-Site VPN connections with Target Gateway as the Virtual Private Gateway you created in
4) and Customer Gateway ID with both created in 3)

6) Download the configuration of both VPNs created as Generic and Vendor Agnostic

14) Attach Virtual Private Gateway to RDS VPC

15) Go to Route tables, Route Propagation and enable for Virtual Private Gateway

16) If you want, you can test by creating a micro EC2 on AWS in the same VPC as the RDS and with ICMP IPv4 enabled in the EC2 Security Group, just to ping on the GCP side of the EC2's private IPv4
```
