# Terraform with local backend

Local backend means that teraform will store the state on locally on your client.  
See https://developer.hashicorp.com/terraform/language/settings/backends/local

# How to 
## Clone this repository
```
git clone https://github.com/paulboekschoten/tf_local_backend.git
```

## Go into the directory `tf_local_backend`
```
cd tf_local_backend
```

Notice that there is no `terraform.tfstate` file present.

## Initialise terraform
```
terraform init
```

Example output
```
Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/null...
- Installing hashicorp/null v3.2.1...
- Installed hashicorp/null v3.2.1 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```


## Run terraform plan
```
terraform plan
```

Example output:
```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # null_resource.helloWorld will be created
  + resource "null_resource" "helloWorld" {
      + id = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

## Run terraform apply
```
terraform apply
```

Example output:
```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # null_resource.helloWorld will be created
  + resource "null_resource" "helloWorld" {
      + id = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

null_resource.helloWorld: Creating...
null_resource.helloWorld: Provisioning with 'local-exec'...
null_resource.helloWorld (local-exec): Executing: ["/bin/sh" "-c" "echo hello world"]
null_resource.helloWorld (local-exec): hello world
null_resource.helloWorld: Creation complete after 0s [id=4947773363057025]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

Notice that there now is a `terraform.tfstate` file.
The content of this file, should look like this:
```
{
  "version": 4,
  "terraform_version": "1.4.4",
  "serial": 1,
  "lineage": "784eeb7d-1056-7076-b62d-a845fb71f0b6",
  "outputs": {},
  "resources": [
    {
      "mode": "managed",
      "type": "null_resource",
      "name": "helloWorld",
      "provider": "provider[\"registry.terraform.io/hashicorp/null\"]",
      "instances": [
        {
          "schema_version": 0,
          "attributes": {
            "id": "4947773363057025",
            "triggers": null
          },
          "sensitive_attributes": []
        }
      ]
    }
  ],
  "check_results": null
}
```