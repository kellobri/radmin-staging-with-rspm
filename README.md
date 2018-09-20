# Local Staging Workflow for R Package Installation Testing

**Goal: Use Vagrant + VirtualBox as a local staging platform for testing package installations from an RStudio Package Manager repository against configuration updates and changes.**

- The `staging-test.yml` Ansible playbook sets up the environment - customize tasks to suit your testing needs (example):
  - Update to yum: `yum update -y`
  - EPEL install
  - Installs recommended system packages
  - Builds a specified version of R from source (`build-R.yml`)
- The `install-packages.yml` tasks set and run the package installation test
  - Points R package installation to a [RStudio Package Manager](https://www.rstudio.com/products/package-manager/) Repository (customize location to your staging repository)
  - Installs R packages from the RStudio Package Manager Repository
  - Reports all package installation successes, failures and errors


### Testing Packages on CentOS Linux 7 x86_64 Vagrant Box

Add the vagrant box, initialize and start:

```
vagrant box add centos/7
vagrant init centos/7
vagrant up
```

Vagrant Tools:

- Update/Additional provisioning runs: `vagrant provision`
- SSH into the box: `vagrant ssh`

### Ansible Playbooks

- Main playbook: `staging-test.yml`
  - Builds R from source: `build-R.yml`
  - Sets CRAN repo and installs packages: `install-packages.yml`
