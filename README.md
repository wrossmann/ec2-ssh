ec2-ssh
=======

Connect via region/instance shortcuts without having to keep track of dynamic hostnames.

Requirements
------------
1. `ssh`
2. SSH keys already set up with your ec2 instances.
    * You can still get the hostname with `ec2-get-dns region instance-id`
3. `bash`
4. `python`
5. `boto` [`pip install boto`]
    * `pip` may require `python-dev` or `python-devel` to install `boto`

Installation
------------
Best placed in `~/bin`, though as long as `ec2-ssh` and `ec2-get-dns` are in the same folder everything should be fine.

Remember to `chmod +x ec2-ssh ec2-get-dns`

Usage
-----
Simply: `ec2-ssh shortcut-name`

Invoking ec2-ssh the first time will prompt you to create `~/.ec2list`, the format is:

    shortcut-name:ec2-region:instance-id[:username]

Eg:

    web-1:us-west-2:i-12345678

The 4th field for the username is optional, if not present 'ec2-user' is used.

ec2-get-dns
-----------
Invoked by: `ec2-get-dns region instance-id` or `ec2-get-dns -s shortcut-name`

If the instance exists and is running will print the public DNS name, otherwise will print a message to stderr and exit with non-zero status: `1`.

Useful for something like:

    scp /home/user/myfile.txt ec2-user@$(ec2-get-dns -s web1):/var/www/site1.com/html/
