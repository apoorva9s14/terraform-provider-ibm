---
subcategory: "VPC infrastructure"
layout: "ibm"
page_title: "IBM : is_backup_policy_plans"
description: |-
  Get information about backup policy plans.
---

# ibm_is_backup_policy_plans

Provides a read-only data source for BackupPolicyPlanCollection. You can then reference the fields of the data source in other resources within the same configuration using interpolation syntax.

**Note:** 
VPC infrastructure services are a regional specific based endpoint, by default targets to `us-south`. Please make sure to target right region in the provider block as shown in the `provider.tf` file, if VPC service is created in region other than `us-south`.

**provider.tf**

```terraform
provider "ibm" {
  region = "eu-gb"
}
```

## Example Usage

```terraform
data "ibm_is_backup_policy_plans" "example" {
  backup_policy_id = ibm_is_backup_policy.example.id
  name             = "example-backup-policy-plan"
}
```

->**Note:**  Backup Policy Jobs are getting enhanced, will be available soon.

## Argument Reference
Review the argument references that you can specify for your data source. 

- `backup_policy_id` - (Required, string) The backup policy identifier.
- `name` - (Optional, string) The unique user-defined name for this backup policy plan.

## Attribute Reference
In addition to all argument reference list, you can access the following attribute references after your data source is created.

- `id` - The unique identifier of the BackupPolicyPlanCollection.
- `plans` - (List) Collection of backup policy plans. 
	
	Nested `plans` blocks have the following structure:
	- `active` - (Boolean) Indicates whether the plan is active.
	- `attach_user_tags` - (List) User tags to attach to each resource created by this plan.
	- `copy_user_tags` - (Boolean) Indicates whether to copy the source's user tags to the created resource.
	- `created_at` - (String) The date and time that the backup policy plan was created.
	- `cron_spec` - (String) The cron specification for the backup schedule.

		->**Note** The backup policy jobs (which create and delete backups for this plan) will not start until this time, and may start for up to 90 minutes after this time.All backup schedules for plans in the same policy must be at least an hour apart.
		
	- `deletion_trigger` (List) `deletion_trigger` block has the following structure:
		
		Nested scheme for `deletion_trigger`:
		- `delete_after` - (Integer) The maximum number of days to keep each backup after creation.
		- `delete_over_count` - (Integer) The maximum number of recent backups to keep. If absent, there is no maximum.
	- `href` - (String) The URL for this backup policy plan.
	- `id` - (String) The unique identifier for this backup policy plan.
	- `lifecycle_state` - (String) The lifecycle state of this backup policy plan.
	- `name` - (String) The unique user-defined name for this backup policy plan.
	- `resource_type` - (String) The type of resource referenced.
