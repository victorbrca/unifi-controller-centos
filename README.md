Role Name: unifi-controller-centos
=========

A role to install/upgrade UniFi Network Controller on CentOS. It has currently been tested with CentOS 7.

Requirements
------------

If you are not using `firewalld`, make sure to set the variable `firewalld_enabled` to false.

Notes
---

#### Testing

Please make sure you have a backup or test in lower level environments before running for the first time.

#### MongoDB

The role will install the MongoDB repo (currently version 3.4), as below (even on upgrades). If you would like to manually install MongoDB, or install a different version, make the appropriate changes in `tasks/main.yml`.

```none
[mongodb-org-3.4]
baseurl = https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck = 1
gpgkey = https://www.mongodb.org/static/pgp/server-3.4.asc
name = MongoDB Repository
```

Note that if you have the older version of MongoDB (installed via Epel) the role will remove it and install version 3.4 from MongoDB's repo.

#### Backup

Two backup files are created in the `{{ backup_destination }}` folder:
+ A full backup of the install (`{{ unifi_base_dir }}/UniFi`)
+ A backup of the data folder (`{{ unifi_base_dir }}/UniFi/data`)

Role Variables
--------------

Default variables can be changed in `defaults/main.yml`.

**Variables that need to be set:**
+ `unifi_version`
+ `firewalld_interface`


The variable `unifi_version` should be set to the version of the controller that you are trying to install/upgrade. You can find the latest version by visiting Ubiquiti's [official download page](https://www.ui.com/download/unifi/default/default/). You can make sure that the link (`https://www.ubnt.com/downloads/unifi/{{ unifi_version }}/UniFi.unix.zip`) works by changing `{{ unifi_version }}` for the actual version (for example `https://www.ubnt.com/downloads/unifi/5.6.42/UniFi.unix.zip`)

**Optional variables that can be changed (and their default value):**

| Variable | Default |
|:----:|:----:|
| `unifi_user` | `ubnt` |
| `unifi_base_dir` | `/opt` |
| `unifi_install_dir` | `"{{ unifi_base_dir }}/UniFi"` |
| `backup_destination` | `/opt` |
| `firewalld_enabled` | `true` |
| `firewalld_zone` | `public` |


Dependencies
------------

+ root/sudo access
+ Internet connection
+ The `unzip` binaries (installed with role)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - unifi-controller-centos

License
-------

MIT.

Author Information
------------------

- [Victor Mendonça](https://victormendonca.com/) - ([GitHub](https://github.com/victorbrca))
