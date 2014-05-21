Deploying Symfony2 with Ansible
===============================

Install
-------

Choose a directory to clone the project

    cd /path/to/somewhere/deploys
    git clone git@github.com:dcastello/symfony2-ansible-deploy

Configuration
-------------

1. Main files

 * **production**: Production servers inventory
 * **staging**: Development servers inventory
 * **group_vars/devservers**: List of variable to fill for development environment (Symfony2 and database vars) 
 * **group_vars/prodservers**: List of variable to fill for production environment (Symfony2 and database vars)

2. group_vars variable list


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

3. production/staging inventory example


    \# staging
    [devservers]
    dev.example.com
    
    \# production
    [prodservers]
    example.com

Task list by role
------------------

1. **Setup** tasks


2. **Deploy** tasks

Examples
--------

The project has tow main roles: *setup* and *deploy*. **Setup** is used to create the main structure and **deploy** to next deploy. 

    $ ansible-playbook -i <host inventory> <playbook>
    
To create main structure for development environment:

    $ ansible-playbook -i devserver deploy_setup.yml
    
Second deploy and next deploys:

    $ ansible-playbook -i devserver deploy.yml
    
    