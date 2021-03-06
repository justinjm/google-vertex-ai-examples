# Creating a Vertex environment

You can use the [Terraform](https://www.terraform.io/) scripts in the `terraform` folder to automatically provision the environment required by the samples. 

The scripts perform the following actions:
1. Enable the required Cloud APIs
2. Create a regional GCS bucket
3. Create an instance of Vertex Notebooks
4. Create service accounts for Vertex Training and Vertex Pipelines
5. Create an instance of Vertex Tensorboard

## Provision Environment

To provision the environment:

- Open Cloud Shell

[![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/justinjm/google-vertex-ai-examples.git)


- Navigate to `~/google-vertex-ai-examples/00-env-setup/terraform`
```
LOCAL_DIR=~/google-vertex-ai-examples
cd $LOCAL_DIR/terraform
```

- Update the `terraform.tfvars` file with the values reflecting your environment (refer [Customize Configuration](#Customize-Configuration) to understand the variables for customization). Alternatively, you can provide the values using the Terraform CLI `-var` options when you execute `terraform apply` in the next step.

- Execute the following commands. :
```
terraform init
terraform apply
```

- To destroy the environment, execute:
```
terraform destroy
```

## Customize Configuration

You can customize your configuration using the following variables in `terraform.tfvars`:

|Variable|Required|Default|Description|
|--------|--------|-------|-----------|
|name_prefix|Yes||Prefix added to the names of provisioned resources. **The prefix should start with a letter and include letters and digits only**.|
|project_id|Yes||GCP project ID|
|network_name|No|default|Name of the network for the Notebook instance. The network must already exist.|
|subnet_name|No|default|Name of the subnet for the Notebook instance. The subnet must already exist.|
|subnet_region|No|us-central1|Region where the subnet was created.|
|zone|Yes||GCP zone for the Notebook instance. The zone must be in the region defined in the `subnet_region` variable|
|machine_type|No|n1-standard-4|Machine type of the  Notebook instance|
|boot_disk_size|No|200GB|Size of the Notebook instance's boot disk|
|image_family|No|tf-2-4-cpu|Image family for the Notebook instance|
|gpu_type|No|null|GPU type of the Notebook instance. By default, the Notebook instance will be provisioned without a GPU|
|gpu_count|No|null|GPU count of the Notebook instance|
|install_gpu_driver|No|false|Whether to install a GPU driver|
|region|No|Set to subnet_region.|GCP region for the GCS bucket and Artifact Registry. It is recommended that the same region is used for all: the bucket, the registry and the Notebook instance. If not provided the `egion` will be set to `subnet_region`.|
|force_destroy|No|false|Whether to force the removal of the bucket on terraform destroy. **Note that by default the bucket will not be destroyed**.|


## Acknowledgements

Original Author: [Rajesh Thallum](https://github.com/RajeshThallam/) - [vertex-ai-labs](https://github.com/RajeshThallam/vertex-ai-labs)