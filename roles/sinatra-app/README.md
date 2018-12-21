Ansible Role: Sinatra-app
=========

Install Ruby, Bundler and deploys a Sinatra application on Ubuntu 14.04 

Requirements
------------

None.

Role Variables
--------------
The following variables are listed in /vars/main.yml

    app_directory: "/home/ubuntu/sinatra_app"
The directory where the Sinatra application files are located.

    packages:
      - ruby
The list of packages to be installed on the server using Ansible's apt module. You can add more packages by adding to the list.

Dependencies
------------

None.

Example Playbook
----------------
    - hosts: sinatra-app-server
      remote_user: ubuntu
      roles:
         - sinatra-app

License
-------

BSD

Author Information
------------------

Alex Fan 