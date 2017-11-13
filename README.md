# Ansible playbook for automated deployment of Wordpress on Linux Debian 9.1 OS.
---
This playbook will download, install and configure Apache2, MySQL, PHP and WordPress on your localmachine. After running a single Ansible file, you should have a whole LAMP + Wordpress environment up and running on your host.

#Requirements
---
- Debian 9.1 (to check your current version of Debian, simply run `lsb_release -a` in terminal);
- Ansible 2.2.1 (to check your current version of Ansible, simply run `ansible --version` in terminal);
- Access to sudo.

#Usage
---
After downloading the repo, enter the `ansible` folder, open the terminal there and run `ansible-playbook playbook.yaml` command.
That's all.

#How it works
---
What will happen is that Ansible will run playbook.yaml, which contains four parts, or **roles** as Ansible calls them: *server*, *php*, *mysql* and *wordpress*. Each role consists of **tasks** of downloading and installing certain packages and configuring them if needed. When running the playbook, in terminal you will see tasks being started and completed one after another.

In *server* role, Ansible downloads and installs **apache2**, **mysql-server**, **libapache2-mod-php**, **php7.0** and **python-mysqldb** packages.

In *php* role, Ansible downloads and installs php extensions packages, that is **php7.0-gd** and **php-ssh2**.

In *mysql* role, Ansible creates a mysql database and a mysql user with access to this database. This database will be the main database for Wordpress. **The name for both the database and the user as well as the user password are defined in 'main.yml' file, in `ci/ansible/roles/mysql/defaults` folder. Change them there if needed.**

Lastly, in *wordpress* role, Ansible downloads and extracts newest version of Wordpress, updates apache2 site and updates Wordpress configuration file with mysql database info.

#After running
---
If the run was smooth and no errors occurred, simply open `http://localhost` in your web browser to see default Wordpress page inviting you to start the setup.

Don't worry if the playbook takes a while to do its job, it didn't freeze - it could be downloading packages.
If a status of a task is green 'ok', great - everything was already configured.
If a status of a task is 'changed', it's good - this means Ansible installed or updated some info in your system.
If an error occurs, read its description and try to find a solution in Google.

#Config
---
Beside `playbook.yaml`, there is also `ansible.cfg` and `hosts` file in main ansible folder. The `ansible.cfg` file is a default Ansible configuration file and its role here is only to point Ansible to location of the `hosts` file.
The `hosts` file is a list of hosts for Ansible to run its tasks on. By default, it's only content is **localhost**, as this repo is designed to deploy Wordpress on a machine you run it on.

---
With any questions, contact me on Slack.
