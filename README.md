# Luke
Simple scripts and templates for scaffolding a basic Django project


## Prerequisites
+ [Oracle's VirtualBox](https://www.virtualbox.org/)
+ [Vagrant](http://www.vagrantup.com/)
+ [Python](http://www.python.org/)
+ [Fabric](http://www.fabfile.org/)
+ [fabutils](https://github.com/vinco/fabutils)


## Usage
1. Download the repository's tarball and extract it to your project's directory

    ```bash
    $ mkdir myproject
    $ cd myproject
    $ wget https://github.com/gGonz/luke/archive/master.tar.gz -O - | tar -xz --strip 1
    ```

2. Set your project's name in `evironments.json`, `fabfile.py` and `provision/provision.sh`

    ```json
    # myproject/environments.json
    {
        "vagrant": {
            "django_settings": "myproject.settings.devel",
        }
    }
    ```

    ```python
    # myproject/fabfile.py
    ...
    # urun('createdb luke -l en_US.UTF-8 -E UTF8 -T template0')
    urun('createdb myproject -l en_US.UTF-8 -E UTF8 -T template0')
    ... 
    # urun('dropdb luke')
    urun('dropdb myproject')
    ...
    ```

    ```bash
    # myproject/provision/provision.sh
    ...
    # PROJECT_NAME=luke
    PROJECT_NAME=myproject
    ...
    ```

3. Create the virtual machine

    ```bash
    $ vagrant up
    ```
4. Redirect the required domains to your localhost

    # /etc/hosts
    192.168.33.2  http://luke.local/

5. Build the environment inside the virtual machine
    
    ```bash
    $ fab environment:vagrant bootstrap
    ```

6. Run the development server
    
    ```bash
    $ fab environment:vagrant runserver
    ```

7. Init your repository

    ```bash
    $ git init
    ```
