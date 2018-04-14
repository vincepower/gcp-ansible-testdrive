# Google Cloud Platform Ansible Engine TestDrive

The following describes how to create the GCP Ansible Engine TestDrive.

There are a number of customizations that must be done prior to executing the scripts.  

## Running the Scripts

### Setting up the base VM

0. Need to be run from the setup-base-image directory
1. Configure to Ansible can connect to GCE using gce.ini and setup.yml as defined below
2. Run the playbook referencing the private key paired with keyfile.pub

```
ansible-playbook --private-key=<local key file> -i gce.py setup.yml
```
>**Note:** It is possible the above will fail without the full path for  gce.py`

#### gce.ini
* In order to run ansible with gce, authorization settings must first be defined in **ansible/gce.ini**

```
# If you are not going to use a 'secrets.py' file, you can set the necessary
# authorization parameters here.

gce_service_account_email_address='email address for the service account'
gce_service_account_pem_file_path='local pem path/file for the service account'
gce_project_id='name of the project to execute against'
```

#### setup.yml
* All `hosts` entries in **setup.yml** have to match the desired hosts output from `gce.py`

```
hosts:
```

#### keyfile.pub
* The public key to distribute


### Running the GCloud Installer

0. This command will need to be run from the orbitera directory
1. Execute some configuration changes due to the random generated subdomain
2. Enable the Extras repo and install Ansible
3. Assign a random password to the ansible user

```
gcloud --project openshift-test-drive deployment-manager deployments create <unique-gcp-instance-name> --template install.jinja
```

### Ansible Scripts Used

```
git clone https://github.com/vincepower/ansible-testdrive
```

