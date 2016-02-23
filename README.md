# ansible-openshift-on-openstack

Ansible scripts to deploy OpenShift on OpenStack
> [openshift-ansible][d5ce5a8d] is the official and original repo to perform OpenShift installation.  But it uses **heat** to perform the installation, which seems to require **admin** privileges.  And there are cases (CI/CD) when a non-admin user would want to install OpenShift. In that case we would want to use **nova** to perform the installation.

## Pre-requisites
This installation was performed using Mac OS X.

### OpenStack RC
+ Get the required configuration data for the target OpenStack environment
    > Login to the webportal (Horizon) of the target OpenStack environment.  
    > Download the OpenStack RC file by navigating to:  
    > **Project --> Compute --> Access & Security --> API Access**

+ Lets assume that the downloaded file is called _openstack-rc.sh_

+ Set the OpenStack related environment variables used by the installation script.

    ``` bash
        source openstack-rc.sh
    ```

### Dynamic inventory with OpenStack
Instead of using a static [inventory][1aba7ed9] file with ansible, we need a [dynamic *OpenStack* inventory][80bbae74].

+ Get the latest OpenStack inventory script
``` bash
    # install *shade* python component
    pip install shade
    wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/openstack.py
    chmod +x openstack.py
```

## Environment setup

Software component  |  Version
--|--
Ansible  |  2.0.0.2
Pip  |  8.0.2
Python  |  2.7.9
python-novaclient  |  3.2.0

## OpenShift install

``` bash
    ansible-playbook install-openshift.yml
```

  [d5ce5a8d]: https://github.com/openshift/openshift-ansible "Ansible to install OpenShift"
  [1aba7ed9]: http://docs.ansible.com/ansible/intro_inventory.html "Ansible inventory"
  [80bbae74]: http://docs.ansible.com/ansible/intro_dynamic_inventory.html "Dynamic inventory"
