Ansible role - Full mail server installation inc webmail, ssl and spam filterr
=====

[![Build Status](https://travis-ci.org/repleo/ansible-role-mail.svg?branch=master)](https://travis-ci.org/repleo/ansible-role-mail)
[![Ansible Galaxy](http://img.shields.io/badge/galaxy-repleo.mail-660198.svg?style=flat)](https://galaxy.ansible.com/repleo/mail)

This role installs and configures a complete mail server installation. The mail server supports:
* SMTP, with authentication and TLS/SSL and STARTTLS
* Spam filter via Spamassassin including 10 year old Bayesian knowledge file
* Courier IMAP including SSL support
* Rainloop webmail client

Easy to configure:
* provide domain names
* provide SSL keys and certificates

and have your mail server up and running in 10 minutes

Requirements
------------

This role requires Ansible 2.0 or higher and platform requirements are listed in the metadata file.

Role Variables
--------------

   # General config.
   rainloop_hostname: mail.example.com

   # SSL Configuration.
   rainloop_ssl: no
   rainloop_redirect_http_to_https: yes
   rainloop_ssl_certificate: "/etc/nginx/ssl/rainloop.crt"
   rainloop_ssl_certificate_key: "/etc/nginx/ssl/rainloop.key"

   # Database config.
   rainloop_db_user: rainloop
   rainloop_db_password: rainloop
   rainloop_db_host: localhost
   rainloop_db_name: rainloopdb


Dependencies
------------

- repleo.rainloop
- repleo.postfix
- repleo.courier-imap

Example Playbook
----------------

Install rainloop
```yaml
- { role: repleo.mail,
    mail_ssl: yes,
    mail_ssl_imap_certificate: /etc/courier/imap.repleo.nl-chain.pem,
    mail_ssl_imap_certificate_key: /etc/courier/imap.repleo.nl.key,
    mail_destinations: "repleo.nl, $mydomain, $myhostname, localhost.$mydomain, localhost",
    mail_networks: "127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128",
    mail_test_mail: jeroen@repleo;nl,
    mail_ssl_smtp_certificate_key: /etc/postfix/tls/smtp.repleo.nl.key,
    mail_ssl_smtp_certificate: /etc/postfix/tls/smtp.repleo.nl_chain.pem,
    mail_webmail_hostname: berichten.repleo.nl,
    mail_ssl_webmail_certificate: /etc/nginx/ssl/berichten.repleo.nl-chain.pem,
    mail_ssl_webmail_certificate_key: /etc/nginx/ssl/berichten.repleo.nl.key
  }

```

License
-------

GPL v3 - (c) 2016, Repleo, Amstelveen

Author Information
------------------

Repleo, Amstelveen, Holland -- www.repleo.nl  
Jeroen Arnoldus (jeroen@repleo.nl)


