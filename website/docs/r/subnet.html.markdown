---
subcategory: "VPC (Virtual Private Cloud)"
layout: "aws"
page_title: "aws_subnet"
description: |-
  Provides an VPC subnet resource.
---

# Resource: aws_subnet

Provides an VPC subnet resource.

For more information, see the documentation on [Subnets][subnets].

## Example Usage

### Basic Usage

```terraform
resource "aws_vpc" "example" {
  cidr_block = "10.1.0.0/16"
}

resource "aws_subnet" "example" {
  vpc_id     = aws_vpc.example.id
  cidr_block = "10.1.1.0/24"

  tags = {
    Name = "Main"
  }
}
```

## Argument Reference

The following arguments are supported:

* `availability_zone` - (Optional) AZ for the subnet.
* `cidr_block` - (Required) The IPv4 CIDR block for the subnet.
* `map_public_ip_on_launch` - (Optional) Indicates whether public IP addresses will be associated with instances created in this subnet. Addresses are associated only if there are available allocated Elastic IP addresses. Default is `false`.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider [`default_tags` configuration block][default-tags] present, tags with matching keys will overwrite those defined at the provider-level.
* `vpc_id` - (Required) The VPC ID.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The ID of the subnet
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider [`default_tags` configuration block][default-tags].

->  **Unsupported attributes**
These exported attributes are currently unsupported:

* `arn` - ARN of the subnet. Always `""`.
* `assign_ipv6_address_on_creation` - Whether an IPv6 address is assigned on creation. Always `false`.
* `availability_zone_id` - AZ ID of the subnet. Always `""`.
* `customer_owned_ipv4_pool` - Identifier of customer owned IPv4 address pool. Always `""`.
* `enable_dns64` - Indicates whether DNS queries made to the Amazon-provided DNS Resolver in this subnet return synthetic IPv6 addresses for IPv4-only destinations. Always `false`.
* `enable_resource_name_dns_aaaa_record_on_launch` - Indicates whether to respond to DNS queries for instance hostnames with DNS AAAA records. Always `false`.
* `enable_resource_name_dns_a_record_on_launch` - Indicates whether to respond to DNS queries for instance hostnames with DNS A records. Always `false`.
* `ipv6_cidr_block_association_id` - Association ID of the IPv6 CIDR block. Always `""`.
* `ipv6_native` - Indicates whether this is an IPv6-only subnet. Always `false`.
* `map_customer_owned_ip_on_launch` - Whether customer owned IP addresses are assigned on network interface creation. Always `false`.
* `outpost_arn` - ARN of the Outpost. Always `""`.
* `owner_id` - The ID of the project that owns the subnet. Always `""`.
* `private_dns_hostname_type_on_launch` - The type of hostnames assigned to instances in the subnet at launch. Always `""`.

## Timeouts

`aws_subnet` provides the following [Timeouts](https://www.terraform.io/docs/configuration/blocks/resources/syntax.html#operation-timeouts)
configuration options:

- `create` - (Default `10m`) How long to wait for a subnet to be created.
- `delete` - (Default `20m`) How long to wait for a subnet to be deleted.

## Import

Subnets can be imported using the `subnet id`, e.g.,

```
$ terraform import aws_subnet.public_subnet subnet-12345678
```

[default-tags]: https://www.terraform.io/docs/providers/aws/index.html#default_tags-configuration-block
[subnets]: https://docs.cloud.croc.ru/en/services/networks/subnets.html
