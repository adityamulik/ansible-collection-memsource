Post Translation Role
=========

The post_translation role is used to pull translated strings from Memsource client for the specified languages, commit, and push those strings back to the code repository.

Requirements
------------

The project_name variable provided for the pre_translation role needs to be provided assuming that pre_translation is run before post_translation script to extract latest strings from the Memsource client.

Role Variables
--------------

Below are mandatory variables required.
- email
- github_username
- github_token
- translation_supported_langs (Default - can be overridden)
- upstream_repo_url
- repo_branch
- downstream_repo_url
- project_name
- memsource_username (To be provided from command-line)
- memsource_password (To be provided from command-line)

Dependencies
------------

The pre_translation role should be executed for the latest strings to be translated on Memsource client.

Playbook
----------------

The playbook pull.yml is available under playbooks/ directory will be used to run the role:

    ---
    - name: Generic Localization - Post-translation
      hosts: localhost
      vars_files:
        - "vars/common.yml"
        - "vars/pull_vars.yml"
      roles:
        - role: community.memsource.post_translation

Execution Steps
---------------

Ansible Playbook (pull.yml) will be used to run this role.

1. Provide the required variables from command-line as per below or can be added to roles/post_translation/default/main.yml
    One way of providing vars using command-line can be as below example
    ```ansible-playbook playbooks/pull.yml -e memsource_username=$MEMSOURCE_USERNAME -e memsource_password=$MEMSOURCE_PASSWORD -e email=test@abc.com```
    or
    Another way of providing vars using command-line can be using a separate yml file (e.g. pull-vars.yml)
    ```ansible-playbook playbooks/pull.yml -e @pull-vars.yml```
2. Provide the memsource username and memsource password from command-line or using Ansible Vault
3. From the root path of the collection, run the below command

```ansible-playbook playbooks/pull.yml -e memsource_username=$MEMSOURCE_USERNAME -e memsource_password=$MEMSOURCE_PASSWORD```

4. A pull request will be generated in the upstream repository for merging the translated strings

License
-------

Apache-2.0

Author Information
------------------
- Aditya Mulik (aditya.mulik@gmail.com)
