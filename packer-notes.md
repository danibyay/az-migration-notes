# Packer

Packer was used to create a base image with compliance packages, and then use this image to create VMs in azure.

Some environment variables have to be set first. (Azure service principal info)

To build the image:

> packer build template.json

## troubleshoot

on some redhat distributions, there is already a binary called packer, so I had to be explicit, create an soft link, and not just use packer.

> ln -s /usr/bin/packer /home/me/packer.io

> ~/packer.io build template.json

## Caveats

But actually I didn't use this because this server didn't have access to everything the image needed due to networking issues. and the server that I ended up using didn't have this problem.

 
So, I deployed the image to another subscription and then moved it to where I wanted it using the GUI in azure portal.

Also, I learned you cannot move images from regions.


## File structure

    roles/
        dynatrace/
        filebeat/
        java_install/
        os-configs/
        packages-services/
    playbook.yml
    template.json

## Playbook

The playbook is used by a provisioner inside the packer template

        ---
        - hosts: default
        remote_user: azureuser
        become: true
        vars:
            some: JADF
            vars: false
            necesary: false
        roles:
            - packages-services
            - os-configs
            - java_install
            - filebeat
            - dynatrace