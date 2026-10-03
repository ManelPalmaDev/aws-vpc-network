# AWS VPC Network

Basic AWS networking lab focused on creating a custom VPC, configuring subnets, route tables, internet connectivity and security groups.

## Objective

The objective of this lab is to understand the basic concepts of AWS networking by creating a custom VPC with public and private subnets and configuring controlled network connectivity between resources.

## AWS Services

* Amazon VPC
* Amazon EC2

## Environment

* AWS Region: `us-east-1`
* VPC CIDR: `10.0.0.0/16`
* Public subnet: `10.0.1.0/24`
* Private subnet: `10.0.2.0/24`
* Public EC2 instance: `public-server-instance`
* Private EC2 instance: `private-server`

## Architecture

```text
                         Internet
                            |
                            v
                    Internet Gateway
                            |
                            v
                     Public Subnet
                       10.0.1.0/24
                            |
                            v
                       Public EC2
                            |
                            | VPC local traffic
                            v
                     Private Subnet
                       10.0.2.0/24
                            |
                            v
                       Private EC2

Private subnet has no direct route to the Internet Gateway.
```

## Configuration

### 1. VPC

* Created a custom VPC.
* Configured the VPC CIDR block: `10.0.0.0/16`.

### 2. Subnets

Created two subnets:

* Public subnet: `10.0.1.0/24`
* Private subnet: `10.0.2.0/24`

The public subnet was configured to provide internet connectivity through an Internet Gateway.

The private subnet was configured without direct internet access.

### 3. Internet Gateway

* Created an Internet Gateway.
* Attached it to the VPC.
* Configured the required route for internet traffic from the public subnet.

### 4. Route Tables

Configured separate route tables for the public and private subnets.

The public route table includes:

```text
0.0.0.0/0 → Internet Gateway
```

The private route table contains only the local VPC route and does not have a direct route to the Internet Gateway.

### 5. EC2 Instances

Created two EC2 instances:

* One instance in the public subnet.
* One instance in the private subnet.

The instances were used to test network connectivity and access control.

### 6. Security Groups

Configured security groups to control network traffic to the EC2 instances.

The public instance allows:

* SSH from the required source.

The private instance allows:

* SSH from `10.0.1.0/24`.

### 7. Connectivity Tests

The following connectivity tests were performed:

* Internet → Public EC2
* Public EC2 → Internet
* Public EC2 → Private EC2
* Private EC2 → Internet: failed as expected

## Results

* A custom AWS VPC was successfully created.
* Public and private subnets were configured.
* Internet connectivity was configured for the public subnet.
* The private subnet was isolated from direct internet access.
* Network traffic between the EC2 instances was controlled using route tables and security groups.
* Connectivity between the public and private instances was successfully tested.

## Screenshots

* VPC configuration
* VPC subnets
* Internet Gateway
* Public route table
* Private route table
* Public EC2 instance
* Private EC2 instance
* Public Security Group
* Private Security Group
* Connectivity tests

## What I Learned

* Basic AWS VPC concepts
* CIDR addressing and subnetting
* Public and private subnets
* Internet Gateway
* Route tables
* Security groups
* EC2 network interfaces
* Basic network connectivity testing
