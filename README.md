# Deploying Symfony2 with Ansible

## Installation

Choose a directory to clone the project. The directory doesn't need to be inside Symfony structure. 

```
    cd /path/to/somewhere/deploys
    git clone git@github.com:dcastello/symfony2-ansible-deploy
```

## Configuration

### Main files

 * **production**: Production servers inventory
 * **staging**: Development servers inventory
 * **group_vars/devservers**: List of variable to fill for development environment (Symfony2 and database vars) 
 * **group_vars/prodservers**: List of variable to fill for production environment (Symfony2 and database vars)

### group_vars variable list

```yaml
    symfony2_project_root: '/var/www/dev.example.com'
    symfony2_project_name: 'My Project'
    symfony2_project_repo: 'url to your GIT repo'
    symfony2_project_branch: master
    symfony2_project_php_path: /usr/local/bin/php
    symfony2_project_env: dev
    symfony2_project_console_opts: ''
    symfony2_project_composer_opts: ''
    database_driver: 'pdo_mysql'
    database_port: null
    database_host: 'localhost'
    database_name: 'name'
    database_user: 'user'
    database_password: 'passwd'
    ansible_ssh_user: user
```

### Production/Staging inventory example

```yaml
    # staging
    [devservers]
    dev.example.com
```

```yaml
    # production
    [prodservers]
    example.com
```

## Task list by role

### **Setup** tasks

- [x] Generate release directory name
- [x] Create *release* dir
- [x] Create *shared* dir
- [x] Create *shared/web/uploads* dir
- [x] Create *shared/app/logs* dir
- [x] Create *shared/app/config* dir
- [x] Generate parameters.yml from template to *shared/app/config*
- [x] Install composer

### **Deploy** tasks

- [x] Generate release directory name
- [x] Pull sources from the repository
- [x] Set permissions to cache directory
- [x] Create *app/logs* symlink
- [x] Create *web/uploads* symlink
- [x] Create *app/config/parameters.yml* symlink
- [x] Run composer install
- [x] Dump assets
- [x] Migrating database
- [x] Create symlink to new release

## Examples

The project has two main roles: *setup* and *deploy*. **Setup** is used to create the main structure and **deploy** to next deployments. 

```
    $ ansible-playbook -i <host inventory> <playbook>
```
    
To create main structure for development environment:

```
    $ ansible-playbook -i /path/to/devserver /path/to/deploy_setup.yml
```
    
Second deploy and next deploys:

```
    $ ansible-playbook -i /path/to/devserver /path/to/deploy.yml
```

## TODO

- Rollback functionality
- Limit number of releases available
