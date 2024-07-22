---
subcategory: "CloudWatch"
layout: "aws"
page_title: "aws_cloudwatch_metric_alarm"
description: |-
  Manages a CloudWatch metric alarm.
---

[metrics]: https://docs.cloud.croc.ru/en/services/monitoring/metrics.html
[dimensions]: https://docs.cloud.croc.ru/en/services/monitoring/metrics.html#dimensions
[default-tags]: https://www.terraform.io/docs/providers/aws/index.html#default_tags-configuration-block

# Resource: aws_cloudwatch_metric_alarm

Manages a CloudWatch metric alarm.

## Example Usage

```terraform
variable instance_id {}

resource "aws_cloudwatch_metric_alarm" "example" {
  alarm_name          = "terraform-test-metric-alarm"
  alarm_description   = "This metric monitors EC2 CPU utilization"
  metric_name         = "CPUUtilization"
  namespace           = "AWS/EC2"
  comparison_operator = "GreaterThanOrEqualToThreshold"
  statistic           = "Average"
  evaluation_periods  = 2
  period              = 120
  threshold           = 80
  alarm_actions       = ["example@mail.com:EMAIL"]
  dimensions = {
    InstanceId = var.instance_id
  }
}
```

## Argument Reference

The following arguments are supported:

* `actions_enabled` - (Optional) Indicates whether actions should be executed during any changes to the alarm state. Defaults to `true`.
* `alarm_actions` - (Optional) Actions, which must be executed when this alarm transitions to the `alarm` state. Each action must be between 1-1024 characters in length. You can specify a maximum of 5 actions.
* `alarm_description` - (Optional) The alarm description. Must be between 1-255 characters in length.
* `alarm_name` - (Required) The name for the alarm. This name must be unique within the project. Must be between 1-255 characters in length.
* `comparison_operator` - (Required) The arithmetic operation to use when comparing the specified `statistic` and `threshold`. Valid values are `GreaterThanOrEqualToThreshold`, `GreaterThanThreshold`, `LessThanThreshold`, `LessThanOrEqualToThreshold`.
* `datapoints_to_alarm` - (Optional) The number of datapoints that must be breaching to trigger the alarm. Minimum value is 1.
* `dimensions` - (Required) The alarm dimensions. See docs for [dimensions][dimensions].
* `evaluation_periods` - (Required) The number of periods which is compared to the threshold. Minimum value is 1.
* `insufficient_data_actions` - (Optional) Actions, which must be executed when this alarm transitions to the `insufficient_data` state. Each action must be between 1-1024 characters in length. You can specify a maximum of 5 actions.
* `metric_name` - (Required) The name of the metric that associated with the alarm. Must be between 1-255 characters in length. See docs for [supported metrics][metrics].
* `namespace` - (Required) The namespace of the metric with which the alarm is associated. Must be between 1-255 characters in length. See docs for the [list of namespaces and supported metrics][metrics].
* `ok_actions` - (Optional) Actions, which must be executed when this alarm transitions to the `ok` state. Each action must be between 1-1024 characters in length. You can specify a maximum of 5 actions.
* `period` - (Required) The period in seconds over which the specified `statistic` is applied. Value must be divisible by 60, minimum value is 60.
* `statistic` - (Required) The statistic for the metric. Valid values are `SampleCount`, `Average`, `Sum`, `Minimum`, `Maximum`.
* `threshold` - (Required) The value, to which metric values will be compared.
* `treat_missing_data` - (Optional) Defines how periods without values would be interpreted. Valid values are `missing`, `ignore`, `breaching` and `not_breaching`. Defaults to `missing`.
* `unit` - (Optional) The unit of the metric associated with the alarm. Valid values are `Percent`, `Bytes` and `Count`.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The name of the alarm.

->  **Unsupported attributes**
These attributes are currently unsupported:

* `arn` - The ARN of the CloudWatch metric alarm. Always `""`.
* `evaluate_low_sample_count_percentiles` - Indicates whether the alarm state should change during periods with too few data points to be statistically significant. Always `""`.
* `extended_statistic` - The percentile statistic for the metric associated with the alarm. Always `""`.
* `metric_query` Enables you to create an alarm based on a metric math expression. Always empty.
    * `account_id` - The ID of the account where the metrics are located, if this is a cross-account alarm.
    * `expression` - The math expression to be performed on the returned data, if this object is performing a math expression.
    * `label` - A human-readable label for this metric or expression.
    * `metric` - The name for this metric.
        * `dimensions` - The dimensions for this metric.
        * `metric_name` - The name for this metric.
        * `namespace` - The namespace for this metric.
        * `period` - The period in seconds over which the specified `stat` is applied.
        * `stat` - The statistic to apply to this metric.
        * `unit` - The unit for this metric.
    * `return_data` - Specify exactly one `metric_query` to be `true` to use that `metric_query` result as the alarm.
* `tags` - A map of tags to assign to the resource. Always empty.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider [`default_tags` configuration block][default-tags]. 
Always includes only tags inherited from the provider `default_tags` or empty if there is no `default_tags` specified.
* `threshold_metric_id` - The threshold metric ID. Always `""`.

## Import

CloudWatch metric alarm can be imported using the `alarm_name`, e.g.,

```
$ terraform import aws_cloudwatch_metric_alarm.test terraform-test-metric-alarm
```
