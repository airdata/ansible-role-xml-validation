Role Name
=========

[![.github/workflows/test.yml](https://github.com/airdata/ansible-role-xml-validation/actions/workflows/molecule_test.yml/badge.svg)](https://github.com/airdata/ansible-role-xml-validation/actions/workflows/test.yml)

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables

--------------
| VariableName              	| Default Value      	|        	| Mandatory 	|
|---------------------------	|--------------------	|--------	|-----------	|
| env                       	| dev                	| String 	| yes       	|
| xsd_templates_folder     	  | templates/         	| String 	| yes       	|
| xml_templates_folder 	      | templates/         	| String 	| yes       	|
| xml_file           	        | - xml-file.xml    	| List   	| Y         	|
| xsd_file                	  | - xsd-schema.xsd  	| List   	| Y         	|



Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

    ---
    - name: Install roles requirements
      hosts: localhost
    
      pre_tasks:
        - name: Creating requirements file
          copy:
            dest: "requirements.yml"
            content: |
              - src: git@github.com:airdata/ansible-role-xml-validation.git
                scm: git
    
        - name: Install ansible-galaxy requirements
          local_action:
            command ansible-galaxy install -r requirements.yml --roles-path roles --force
          delegate_to: localhost


    - name: Run role xml_validation
      hosts: all
      gather_facts: yes
      vars:
        templates_folder: templates/dev
        xml_file:
          - xml-file2.xml
          - xml-file3.xml
        xsd_file:
          - xsd-schema2.xsd
          - xsd-schema3.xsd
        env: test
    
      tasks:
        - name: ansible-role-xml-validation
          include_role:
            name: ansible-role-xml-validation



License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
