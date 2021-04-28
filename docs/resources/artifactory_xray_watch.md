# Xray Watch Resource

Provides a Xray watch resource.

## Example Usage

```hcl
# Create a new Xray watch for all repositories
resource "xray_watch" "example" {
  name  = "watch-name"
  description = "watching all repositories"
  resource {
    type = "all-repos"
    name = "All Repositories"
  }
  assigned_policies {
    name = xray_policy.example.name
    type = "license"
  }
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) Name of the watch (must be unique)
* `description` - (Optional) Description of the watch
* `active` - (Optional) Whether or not the watch will be active
* `resource` - (Required) Nested argument describing the resource to be watched. Defined below.
* `assigned_policies` - (Required) Nested argument describing policies that will be applied. Defined below.

### resource

The top-level `resource` block contains a list of one or more resource objects that each support the following:

* `type` - (Required) Type of resource to be watched
* `name` - (Required) A name describing the resource
* `bin_mgr_id` - (Optional) The ID number of a binary manager resource
* `repo_type` - (Optional) Type of repository (e.g. local or remote)
* `filters` - (Optional) Nested argument describing filters to be applied. Defined below.

#### filters

The nested `filters` block contains a list of one or more filters to be applied, each of which supports the following:

* `type` - (Required) The type of filter, such as `regex` or `package-type`
* `value` - (Required) The value of the filter, such as the text of the regex or name of the package type

### assigned_policies

The top-level `assigned_policies` block contains a list of one or more policy objects that each support the following:

* `name` - (Required) The name of the policy that will be applied
* `type` - (Required) The type of the policy


## Import

Watches can be imported using their name, e.g.

```
$ terraform import xray_watch.example watch-name
```
