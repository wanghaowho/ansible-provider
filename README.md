# Ansible ECS Module
Ansible ECS Module is a new ansible module, and you can manage Alicloud ECS more flexibly and conveniently via it. Next to introduce simply this module.
## module/ecs.py
There are two files in the module directory:  

- ecs_module.py
  - This file describes some function that can operate ecs via ECS Module and lists some params can be used. Finally, it lists several playbook examples that operate ecs.
- ecs.py
  - This file is the ECS Module implement, contins getting playbook params and ecs operation, such as create, start, stop, restart and delete one or more ecs instances.

## utils/ecs.py
In the utils directory, the file ecs.py identifies and gains playbook params, and provides this params to module/ecs.py. In addition, this file implements connection between ansible and Alicloud ecs api via footmark.

## footmark
footmark is a Python package that provides interfaces to Alicloud Web Services, which allows Python developers to write software that makes use of Alicloud ECS.
### Install footmark
footmark can be intalled conveniently via pip:

	$ sudo pip install footmark


## roles
There are some playbook that can be used to operate ecs in the roles directory. In every playbook, you need to input some params, and you can view every param description in the module/ecs_module.py.
There is ecs module file in the directory library, and you must put library/ecs.py into roles before you execute playbook.


## How to use ECS Module
### Install ecs SDK, footmark and ecsutils

	$ sudo pip install aliyun-python-sdk-ecs
	$ sudo pip install aliyun-python-sdk-ecs --upgrade
	$ sudo pip install footmark
	$ sudo pip install ecsutils
### Update footmark and ecsutils
If you want to update footmark and ecsutils, you can execute commands:

	$ sudo pip install footmark --upgrade
	$ sudo pip install ecsutils --upgrade
### Install module/ecs.py
Download roles directory in anywhere and make library/ecs.py in the roles. If not, you can put ecs.py into library(if not, make it), and move the library to the roles. The final folder structure after install ecs module:

	- roles
	  - library
	    - ecs.py
	  - start.yml
### Execute playbook
Before you execute playbook, you should input your access-key pairs(`acs_access_key` and `acs_secret_access_key`) in the playbook or set environment variable:`ACS_ACCESS_KEY` and `ACS_SECRET_ACCESS_KEY`. Then input others ecs params in the playbook. Finally, move to roles and execute follow command:

	$ ansible-playbook start.yml

### Package ecsutils
When you modify utils/ecs.py, you need to package and distribute it. First, you need to edit utils/__init__.py and set a new version to '__version__ '. Second execute command as follows:

    # build ecsutils package
    $ python setup.py sdist

    # make sure your enviroment has installed twine, if not, execute command:
    $ sudo pip install twine

    # distribute new ecsutils
    # upload your project
	$ twine upload dist/<your-ecsutils-package>
Finally, use `--upgrade` to update ecstuils.

	   
