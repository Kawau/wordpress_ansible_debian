## Repository with Ansible files for automation of setting up Wordpress environment on a Linux Debian 9.1 OS.

Requirements:
- Debian 9.1 (to check your current version of Debian, simply run `lsb_release -a` in terminal;
- Ansible 2.2.1 (to check your current version of Ansible, simply run `ansible --version` in terminal;
- Access to sudo.

After downloading the repo, enter the 'ansible' folder, open the terminal there and run `ansible-playbook playbook.yaml` command.
That's all.

What will happen is that Ansible will run the playbook.yaml, which contains four parts, or 'roles' as Ansible calls them: server, php, mysql and wordpress. 

Each part consists of downloading and installing certain packages and configuring them if needed.

In 'server' role, Ansible downloads and installs apache2, mysql-server, libapache2-mod-php, php7.0 and python-mysqldb packages.

In 'php' role, Ansible downloads and installs php extensions packages, that is php7.0-gd and php-ssh2.

In 'mysql' role, Ansible creates mysql database and a mysql user with access to this database. This database will be the main database for Wordpress. The name for both the database and the user as well as the user password are defined in 'main.yml' file, in `ci/ansible/roles/mysql/defaults` folder. Change them if needed.

Lastly, in 'wordpress' role, Ansible downloads and extracts newest version of Wordpress, updates apache2 site and updates Wordpress configuration file with mysql database info.

If the run was smooth and no errors occurred, simply open `http://localhost` in your web browser to see default Wordpress page inviting you to start the setup.

Don't worry if the playbook takes a while to do its job, it didn't freeze - it could be downloading packages. 

If a status of a task is 'changed', it's good - this means Ansible installed or updated some info in your system.

With any questions, contact me on Slack.
