# IMS Provisioning for Wazi environment

The IMS provisioning playbook samples demonstrate how to allocate the required
data sets and configure them to provision IMS and related services.

It is a good practice to review the playbook sample contents before executing
them. It will help you understand the requirements in terms of space, location,
names, authority, and the artifacts that will be created and cleaned up.
Although samples are written to operate without the need for the user’s
configuration, flexibility is written into the samples because it is not easy
to determine if a sample has access to the host’s resources. Review the
playbook notes sections for additional details and configuration.


## Playbook Summary

- [**provision-tmdb-wazi.yml**](provision-tmdb-wazi.yml)  - allocating required data sets and kicking off many IMS services. The playbook contains the following main tasks:
  - Set up runtime environment
  - Validate user inputs
  - Track request type in instance status block (new instance create, delete or reconciliation)
  - Check for duplicate IMS, IMSPlex and port numbers
  - Create work datasets, system and runtime datasets
  - Create PROCLIB members
  - Define IMS RACF and APF datasets
  - Create DBRC and IMS Catalog resources
  - Create and configure CSL components (SCI, RM, OM) 
  - Create and configure IMS Connect and ODBM
  - Configure AT-TLS for IMS Connect and ODBM ports
- [**deprovision-tmdb-wazi.yml**](deprovision-tmdb-wazi.yml)  - deallocating data sets and stopping IMS services. The playbook contains the following main tasks:
  - Set up runtime environment
  - Track request type in instance status block (new instance create, delete or reconciliation)
  - Stop all IMS resources
  - Shut down IMS
  - Stop IMS Connect and ODBM
  - Stop CSL components (SCI, RM, OM)
  - Delete work, system and runtime datasets
  - Delete IMS Catalog datasets
  - Delete IMS PROCLIB members
  - Remove AT-TLS ports from Policy Agent
- [**query-ims.yml**](query-ims.yml) - provides examples of how to query status of different IMS services.  
  
These examples utilize the roles defined below.

## Role Summary

This project uses roles to provide an object-oriented model to provision IMS.  Each role is responsible for a specific area.  These roles can be re-used in different playbooks.

- [**check_duplicate_ims**](roles/check_duplicate_ims) - Check if the IMSID requested is already up
- [**check_duplicate_imsplex**](roles/check_duplicate_imsplex) - Check if the IMSPlex requested is already up
- [**check_inputs**](roles/check_inputs) - Check if the IMSID, IMSPlex, and port numbers are valid
- [**check_port**](roles/check_port) - Check if port numbers requested are reserved or in use
- [**deprovsion_ims**](roles/deprovision_ims) - deprovisions IMS: shutdown and delete all datasets created by IMS provision playbook
- [**ims_apf**](roles/ims_apf) - adds authorization of IMS datasets to zOS
- [**ims_catalog**](roles/ims_catalog) - allocates, loads, and deletes IMS catalog
- [**ims_common**](roles/ims_common) - provides services such as start/stop IMS control regions and IMS Connection
- [**ims_common_queue**](roles/ims_common_queue) - provides dataset definition and query or CQS
- [**ims_dataset**](roles/ims_dataset) - creates and deletes IMS definition data sets and libraries
- [**ims_dbrc**](roles/ims_dbrc) - sets up DBRC defaults and prepares DBRC
- [**ims_exit**](roles/ims_exit) - prepares security and connection exit for IMS
- [**ims_gen**](roles/ims_gen) - prepares DBDGEN, PSBGEN, and ACBGEN
- [**ims_iefjobs**](roles/ims_iefjobs) - creates IEF jobs
- [**ims_initialize**](roles/ims_initialize) - reserves ICON ports and sends PROCLIB templates to zOS
- [**ims_online_change**](roles/ims_online_change) - enables the online change utility
- [**ims_operations_manager**](roles/ims_operations_manager) - defines, starts, stops, and queries operations manager
- [**ims_proclib**](roles/ims_proclib) - defines BPE configuration and copies PROCLIB
- [**ims_racf**](roles/ims_racf) - prepares RACF security for IMS
- [**ims_region**](roles/ims_region) - starts IMS regions
- [**ims_resource_manager**](roles/ims_resource_manager) - defines, starts, stops and queries RM
- [**ims_structured_call_interface**](roles/ims_structured_call_interface) - defines, starts, stops, and queries SCI
- [**ims_sysdef**](roles/ims_sysdef) - prepares system definition data set
- [**ims_tls**](roles/ims_tls) - configure AT-TLS ports
- [**install-bzip2**](roles/install-bzip2) - copies and installs utility zip file on zOS
- [**monitor_ims**](roles/monitor_ims) - checks to see if IMS is up or down.
- [**provision_ims**](roles/provision_ims) - this is the main role to provision IMS.  It utilizes other roles to allocate datasets, prepare datasets and start all IMS services
- [**save-templates-to-datasets**](roles/save-templates-to-datasets) - copies templates from USS to zOS data sets
- [**send-template**](roles/send-template) - sends a template file from the local host to zOS
- [**send-templates**](roles/send-templates)  - sends multiple templates in a directory from local host to zOS
- [**set_up_run_environment**](roles/set_up_run_environment)  - setting up the initial environment for playbook execution
- [**stop_jmp**](roles/stop_jmp) - stop JMP (Java) region
- [**stop_mpp**](roles/stop_mmp) - stop MPP region
- [**submit-rexx**](roles/submit-rexx) - runs a REXX script on zOS


Inside each role:

* `./tasks` contains tasks that can be performed by the role.
  Sub-folder names describe the use of the contained files.
* `./tasks/main.yml` contains the default tasks performed by the role.


## Requirements
* IBM z/OS core collection 1.5.0
* IBM z/OS IMS collection 1.2.0
* IBM® Wazi Sandbox 2.4 or IBM® Extended z/OS® ADCD for Z Development and Test Environment built upon the general release of ADCD z/OS® V2R5 December Edition of 2022 or later

## Getting Started

Consult the [Operator Collection SDK](https://github.com/IBM/operator-collection-sdk) for basic concepts and tutorials before modifying this collection for your own use. 

## Copyright

© Copyright IBM Corporation 2023

## License
Licensed under [Apache License](https://opensource.org/licenses/Apache-2.0).

