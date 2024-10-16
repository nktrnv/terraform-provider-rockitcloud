---
subcategory: "VPC (Virtual Private Cloud)"
layout: "aws"
page_title: "aws_default_vpc_dhcp_options"
description: |-
  Manage the default VPC DHCP Options resource.
---

# Resource: aws_default_vpc_dhcp_options

Provides a resource to manage the default AWS DHCP Options Set in the current region.

Each AWS region comes with a default set of DHCP options.
**This is an advanced resource**, and has special caveats to be aware of when
using it. Please read this document in its entirety before using this resource.

The `aws_default_vpc_dhcp_options` behaves differently from normal resources, in that
Terraform does not _create_ this resource, but instead "adopts" it
into management.

## Example Usage

Basic usage with tags:

```terraform
resource "aws_default_vpc_dhcp_options" "default" {
  tags = {
    Name = "Default DHCP Option Set"
  }
}
```

## Argument Reference

The arguments of an `aws_default_vpc_dhcp_options` differ slightly from [`aws_vpc_dhcp_options`][tf-vpc-dhcp-options] resources.
Namely, the `domain_name`, `domain_name_servers` and `ntp_servers` arguments are computed.
The following arguments are still supported:

* `netbios_name_servers` - (Optional) List of NETBIOS name servers.
* `netbios_node_type` - (Optional) The NetBIOS node type (1, 2, 4, or 8). AWS recommends to specify 2 since broadcast and multicast are not supported in their network. For more information about these node types, see [RFC 2132](http://www.ietf.org/rfc/rfc2132.txt).
* `owner_id` - The ID of the project that owns the DHCP options set.
* `tags` - (Optional) A map of tags to assign to the resource.

### Removing `aws_default_vpc_dhcp_options` from your configuration

The `aws_default_vpc_dhcp_options` resource allows you to manage a region's default DHCP Options Set,
but Terraform cannot destroy it. Removing this resource from your configuration
will remove it from your statefile and management, but will not destroy the DHCP Options Set.
You can resume managing the DHCP Options Set via the cloud console.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - ID of the DHCP Options Set.
* `arn` - ARN of the DHCP Options Set.

## Import

VPC DHCP Options can be imported using the `dhcp options id`, e.g.,

```
$ terraform import aws_default_vpc_dhcp_options.default_options dopt-d9070ebb
```

[tf-vpc-dhcp-options]: vpc_dhcp_options.html
