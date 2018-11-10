# sssd service installation

## Software Installation

- redhat
- ubuntu
  ```bash
  sudo apt install krb5-user samba sssd chrony
  ```


  ## Kerberos Configuration

  file location : /etc/sssd/sssd.conf

  ```bash
    [sssd]
    config_file_version = 2
    domains = haifa.ibm.com
    services = nss, pam, pac
    debug_level = 5

    [pam]
    debug_level = 5

    [domain/haifa.ibm.com]
    id_provider = ad
    ad_server = _srv_
    ad_hostname = miq-qa-0021.xiv.ibm.com
    ad_gpo_access_control = disabled
    ad_enable_dns_sites = true
    auth_provider = ad
    chpass_provider = ad
    access_provider = ad
    debug_level = 5

    ldap_schema = ad
    ldap_id_mapping = False
    fallback_homedir = /home/%d/%u
    default_shell = /bin/bash
    cache_credentials = true

    #Access control
    ldap_access_order = expire
    ldap_account_expire_policy = ad
    ldap_force_upper_case_realm = true
    #simple_allow_groups = xiv_ldap_users_dl

    subdomains_provider = none
ldap_referrals = false


  ```