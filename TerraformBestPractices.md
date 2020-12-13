
## Terraform Best practices

### Overview 
A consolidate quick step guide without going OCI or Terraform documentation

### Best practice guidelines 
#### Reference image by OCID 
Specify the image OCID directly, rather than locating it using the oci_core_image data source.
<pre><code>variable "image_id" {
  type = "map"
  default = {
    // See https://docs.cloud.oracle.com/iaas/images/
    // Oracle-provided image "Oracle-Linux-7.4-2018.02.21-1"
    us-ashburn-1 = "ocid1.image.oc1.iad..<unique_ID>"
    eu-frankfurt-1 = "ocid1.image.oc1.eu-frankfurt-1..<unique_ID>"
  }
}</code></pre>
Compute instance can use as 
<pre><code>
resource "oci_core_instance" "TFInstance" {
  image = "${var.image_id[var.region]}"
  ...
}
</code></pre>
#### Reference availability domains in a list instead of lookup
Method-1 - explicitly list the Availability Domain names for the regions in your configuration
<pre><code>
variable "ad_list" {
  type = "list"
}
// Index:
resource "oci_core_instance" "nat" {
  availability_domain = "${var.ad_list[var.nat_instance_ad_index]}"
  ...
}
// Or iterate through all the ADs:
resource "oci_core_subnet" "nat" {
  count = "${length(var.ad_list)}"
  availability_domain = "${var.ad_list[count.index]}"
  ...
}
// set the ad names for your tenant and region
variable "ad_list" {
  type = "list"
  default = ["kIdk:PHX-AD-1","kIdk:PHX-AD-2","kIdk:PHX-AD-3"]
}
</code></pre>
Method-2 set ad_list by using oci_identity_availability_domains. Not to use inside the module 
<pre><code>
data "oci_identity_availability_domains" "ad" {
  compartment_id = "${var.tenancy_ocid}"
}
 
data "template_file" "ad_names" {
  count = "${length(data.oci_identity_availability_domains.ad.availability_domains)}"
  template = "${lookup(data.oci_identity_availability_domains.ad.availability_domains[count.index], "name")}"
}
  
module "ssm_network" {
  ad_list = "${data.template_file.ad_names.*.rendered}"
  ...
}
</code></pre>

### References 
* [Terraform best practices](https://docs.cloud.oracle.com/en-us/iaas/Content/API/SDKDocs/terraformbestpractices.htm)
* [Terraform OCI Provider](https://registry.terraform.io/providers/hashicorp/oci/latest/docs/guides/best_practices)
