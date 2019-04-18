Role Name
=========

Install and configure [CVMFS](https://cernvm.cern.ch/portal/filesystem) client

Requirements
------------

* EL6/7

Role Variables
--------------

Manage CVMFS Yum repository and configure it.

    cvmfs_manage_yumrepo: true
    cvmfs_yumrepo_enabled: true
    cvmfs_yumrepo_testing_enabled: false
    cvmfs_yumrepo_config_enabled: false
    cvmfs_yumrepo_priority: 10

Manage the creation of a cvmfs user and group

    cvmfs_manage_cvmfs_user: true

Mount repositories using autofs or by explicit mount

    cvmfs_mount_repositories: [ autofs | mount ]

The configuration of a CVMFS client is described in more details at
 https://cvmfs.readthedocs.io/en/stable/

Some settings can be set by variables

Define the http proxy

    cvmfs_http_proxy:
      - http://squid01.example.org:3128|http://squid02.example.org:3128
      - DIRECT

The location of then cache is given by

    cvmfs_cache_base: /var/cache/cvmfs

The size of the cache can be set explicit using

    cvmfs_cache_quota: 4000

In case the cache is on a separate partition, its size can be given
as a fraction of the partition size

    cvmfs_quota_fraction: 0.85

Other settings can be done by a passing a hash to

    cvmfs_config:
      CVMFS_USE_GEOAPI: yes

Repositories and their settings are provided as a hash

   cvmfs_repositories:
     - name: cms.cern.ch
       config:
         CMS_CACHE_BASE: /var/lib/test
       env_vars:
         CMS_LOCAL_SITE: /cvmfs/cms.cern.ch/SITECONF/T2_AT_Vienna


Example Playbook
----------------


    - hosts: servers
      roles:
         - role: hephy.cvmfs
           vars:
             cvmfs_quota_limit: 4000
             cvmfs_repositories:
               - name: cms.cern.ch
                 env_vars:
                   CMS_LOCAL_SITE: /cvmfs/cms.cern.ch/SITECONF/T2_AT_Vienna
               - name: belle.cern.ch


License
-------

MIT

Author Information
------------------


Written by [Dietrich Liko](http://hephy.at/dliko) in April 2019

[Institute for High Energy Physics](http://www.hephy.at) of the
[Austrian Academy of Sciences](http://www.oeaw.ac.at)
