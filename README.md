# ansible-role-spamassassin

[![Build Status](https://github.com/systemli/ansible-role-spamassassin/workflows/Integration/badge.svg?branch=main)](https://github.com/systemli/ansible-role-spamassassin/actions?query=workflow%3AIntegration)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-spamassassin-blue.svg)](https://galaxy.ansible.com/systemli/spamassassin/)

Role to install & maintain spamassassin (including DKIM, pyzor and razor checks)

## Role Variables

Defaults:

    ## general
    spamassassin_user: debian-spamd
    spamassassin_group: debian-spamd
    spamassassin_home_dir: /var/lib/spamassassin
    spamassassin_log_dir: /var/log/spamassassin

    # Write spamassassin config files (only install spamassassin and configure
    # cronjob if set to False)
    spamassassin_configure: True

    ## file: /etc/default/spamassassin

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

    # manual welcomelisting
    # In spamassassin 4.0.0 whitelist has been renamed to welcomelist and blacklist to blocklist, see
    # https://cwiki.apache.org/confluence/display/spamassassin/WelcomelistBlocklist
    # the role variable spamassassin_whitelist has been renamed to spamassassin_welcomelist accordingly.
    # If spamassassin_whitelist is set in host vars and non-empty, it will be merged with spamassassin_welcomelist
    ## file: /etc/spamassassin/whitelist.cf resp. /etc/spamassassin/welcomelist.cf
    spamassassin_welcomelist: []

    # Add addtional update channels, which should be updates by the daily
    # sa-update cronjob. E.g.:
    # spamassassin_additional_update_channels:
    #   - address: spamassassin.heinlein-support.de
    #     gpg: no
    spamassassin_additional_update_channels: []

    # Enable additional pyzor check
    spamassassin_pyzor_enabled: False

    spamassassin_pyzor_config_dir: /etc/spamassassin/.pyzor

    # Enable additional razor chek
    spamassassin_razor_enabled: True

    spamassassin_razor_config_dir: /etc/spamassassin/.razor

    # Enable monit monitoring
    spamassassin_monit_enabled: False

    # Enable spam training by users and domain
    # spamassassin_spamtraining_users:
    #    - domain: myfirstdomain.org
    #      users:
    #       - admin
    #       - foo
    #    - domain: myseconddomain.org
    #      users:
    #       - admina
    #       - foobar
    spamassassin_spamtraining_users: []

    # Set custom spamassassin scores
    # spamassassin_custom_scores:
    #    - name: SPF_FAIL
    #      score: "0 1.5 0 0.919"
    spamassassin_custom_scores: []

    # On Debian 12/Bookworm, this role will per default install 'spamd' alongside spamassassin
    # On Debian 11/Bullseye, 'spamd' will not be installed per default, except:
    #   1. bullseye-backports are enabled in your apt sources AND spamassassin is already installed with version >=4.0.0-1
    #   2. bullseye-backports are enabled in your apt sources AND 'spamd' package is added to the 'spamassassin_packages' variable
    # Note that this role does not take care of adding bullseye-backports to your apt sources!
    spamassassin_packages:
      - spamassassin
      - spamc
      - libmail-spf-perl
      - libmail-dkim-perl
      - procps  # provides /bin/kill, should actually be a dependency



## Download


Download latest release with `ansible-galaxy`

	ansible-galaxy install systemli.spamassassin

## Example Playbook


    - hosts: servers
      roles:
         - { role: systemli.spamassassin }

## Testing & Development

Molecule, Goss, Docker, and Github Actions are used for continous testing.
You can easily test the role locally with

    molecule test

This requires Molecule, Vagrant and `python-vagrant` to be installed.

## License

GPLv3

## Author Information

https://www.systemli.org
