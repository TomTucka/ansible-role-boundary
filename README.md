# ansible-role-boundary

A role to build production grade HashiCorp Boundary. This role has been built to be used in conjunction
with [Packer](https://packer.io/) to build production-grade machine images that can be used to deploy Boundary into a cloud or data-center environment.

This role isn't used for deploying or orchestrating Boundary, that should be done using [Terraform](https://terraform.io/).


## Usage

Galaxy File:
```yml
---
- name: ansible-role-boundary
  src: https://github.com/tomtucka/ansible-role-boundary.git

```

Playbook File:
```yml
---
- name: Prepare Image for HashiCorp Boundary
  hosts: all
  become: true
  roles:
    - ansible-role-boundary

```

Packer Config:
```hcl
provisioner "ansible-local" {
  galaxy_file   = "../ansible/requirements.yml"
  playbook_file = "../ansible/install.yml"
  galaxy_roles_path = "/usr/share/ansible/roles"

  extra_arguments = [
    "--extra-vars",
    "'boundary_version=${var.boundary_version}'",
  ]
}
```
