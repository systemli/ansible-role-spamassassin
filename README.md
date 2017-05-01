ansible-role-spamassassin
=========

[![Build Status](https://travis-ci.org/systemli/spamassassin.svg?branch=master)](https://travis-ci.org/systemli/ansible-role-spamassassin) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-spamassassin-blue.svg)](https://galaxy.ansible.com/systemli/spamassassin/)

Role to install & maintain spamassassin (including DKIM and pyzor checks)

Role Variables
--------------

Defaults:

    ## general
    spamassassin_user: spamd
    spamassassin_home_dir: /var/log/spamassassin/
    
    ## file: /etc/default/spamassassin
    
    spamassassin_enabled: true
    spamassassin_automatic_rule_update_enabled: true
    spamassassin_nice_level: 0
    
    ## file: /etc/spamassassin/local.cf
    
    # Rewrite the mail header?
    spamassassin_rewrite_header_enabled: true
    spamassassin_rewrite_header: "Subject *****SPAM*****"
    
    # Allowed 0, 1, 2 - see https://spamassassin.apache.org/full/3.0.x/dist/doc/Mail_SpamAssassin_Conf.html
    spamassassin_report_safe: 0
    
    # Set the score required before a mail is considered spam
    spamassassin_required_score: 5.0
    
    # Whether to use the naive-Bayesian-style classifier built into SpamAssassin.
    spamassassin_use_bayes: 1
    
    # Whether to use rules using the naive-Bayesian-style classifier built into SpamAssassin.
    spamassassin_bayes_auto_learn: 1
    
    # What networks or hosts are 'trusted' in your setup.
    spamassassin_trusted_networks: []
    
    # Allowed: nfsafe, flock, win32
    spamassassin_lock_method: flock
    
    # If you receive mail filtered by upstream mail systems, like a spam-filtering ISP or mailing list,
    # and that service adds new headers (as most of them do), these headers may provide inappropriate cues
    # to the Bayesian classifier, allowing it to take a ``short cut''. To avoid this, list the headers using this setting.
    spamassassin_bayes_ignore_header:
      - X-Bogosity
      - X-Spam-Flag
      - X-Spam-Status

    # Enable additional pyzor check
    spamassassin_pyzor_enabled: False 

    spamassassin_pyzor_config_dir: /etc/mail/spamassassin/.pyzor/
 
    # Enable monit monitoring
    spamassassin_monit_enabled: False

Download
--------

Download latest release with `ansible-galaxy`

	ansible-galaxy install systemli.spamassassin

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: systemli.spamassassin }



## Testing

Make sure your user is in the `docker` group. To only test your current setup, do

    molecule test

To test different versions of ansible, do

    tox

If your role depends on other roles from [Ansible Galaxy](https://galaxy.ansible.com/), uncomment the dependency lines in `molecule.yml` and add the dependencies in `tests/requirements.yml`.

## License

GPL

## Author Information

https://www.systemli.org
