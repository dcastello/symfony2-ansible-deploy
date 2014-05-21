Symfony2 deploy with Ansible
============================

Install
-------

Choose a directory to clone the project

    cd /path/to/somewhere/deploys
    git clone git@github.com:dcastello/symfony2-ansible-deploy

Configuration
-------------

TODO

Examples
--------

The project has tow main roles: *setup* and *deploy*. **Setup** is used to create the main structure and **deploy** to next deploy. 

    $ ansible-playbook -i <host inventory> <playbook>
    
To create main structure for development environment:

    $ ansible-playbook -i devserver deploy_setup.yml
    
Second deploy and next deploys:

    $ ansible-playbook -i devserver deploy.yml
    
    