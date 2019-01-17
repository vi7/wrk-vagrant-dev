Vagrant based local dev env
---------------------------

## Provision

### TODO

**packages:**

- epel-release repo
- IUS repo https://centos7.iuscommunity.org/ius-release.rpm
- vim-enhanced
- tmux2u (IUS)
- git2u (IUS)
- python36u/pip (IUS)
- ansible (from pip)

**puppet project:**

- rfi repo IP at /etc/hosts:

    ```
    172.22.4.57 repo repo.inw.rfiserve.net
    ```

- CentOS-Base:

    ```
    [base]
    name=centos7 - Base
    baseurl=http://repo/centos7-$basearch/RPMS.os/
    gpgcheck=1
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    #exclude=*i?86*
    enabled=1
    metadata_expire=1h

    [updates]
    name=centos7 - Updates
    baseurl=http://repo/centos7-$basearch/RPMS.updates/
    gpgcheck=1
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    #exclude=*i?86*
    enabled=1

    #[addons]
    #name=CentOS-7 - Addons
    #baseurl=http://repo/centos7-$basearch/RPMS.addons/
    #gpgcheck=1
    #gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    #exclude=*i?86*
    #enabled=0
    metadata_expire=1h

    [extras]
    name=centos7 - Extras
    baseurl=http://repo/centos7-$basearch/RPMS.extras/
    gpgcheck=1
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    #exclude=*i?86*
    enabled=1
    metadata_expire=1h

    [centosplus]
    name=centos7 - Plus
    baseurl=http://repo/centos7-$basearch/RPMS.centosplus/
    gpgcheck=1
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    #exclude=*i?86*
    enabled=0
    metadata_expire=1h
    ```

- epel

    ```
    [epel]
    name=RFI EPEL repository mirror: CentOS$releasever ($basearch) Epel
    enabled=1
    baseurl=http://repo/centos$releasever-$basearch/RPMS.epel
    gpgcheck=0
    metadata_expire=1h
    ```

- rfi repo:
  
    ```
    [rfi]
    name=RFI repository for local RPM builds (tested, stable): CentOS$releasever ($basearch) Base                                                                       
    enabled=1
    baseurl=http://repo/centos$releasever-$basearch/RPMS.rfi
    gpgcheck=0
    metadata_expire=5m
    ```

- package (rfi repo): puppet-agent-5.5.3
- package: rfi-infradb-rails4-1.0-20000
- ?? add VM to the hosts.yaml at puppet::modules/puppet/files/hostinfo/hosts.yaml
- ?? run magic to update hieradata and infradb
  - ?? add VM to hieradata::puppet/code/environments/production/hieradata/devices/${HOSTNAME}.yaml:

      ```yaml
      ---
      rfi::device:
        clusters:
        cpu: 1 x 2.6GHz Virtual
        disk: 1 x 20GB vm_data
        environment: reserved
        interfaces:
          enp0s3:
            macaddr:
            ipaddr:
            zone: internal
        location: local
        memory: 2G
        name: localhost.localdomain
        note: vdmitriev vagrant
        organization: rfi
        os: centos7
        rfi-db-id:
        services:
        type: virtual machine
        vendor_alias: Vagrant
      classes:
        - dummy_module
      ```

  - ?? add VM to the infradb: /opt/infradb4/db/sqlite.db
- run standalone puppet: /opt/infradb4/puppet/code/environments/production/modules/rfi/files/standalone.sh

