# ace-box-ext-demo-auto-remediation-easytravel

This external use case contains a demo for Auto Remediation using Dynatrace + Ansible Tower + ServiceNow.

## Release overview and ACE-BOX support

Please see below table on ace-box support:
| Use Case Version | Supported ACE Box version |
| --- | --- |
| v1.0.0 | v1.12.6 |
| v1.1.0 | v1.13.0 |

## Components deployed

The following components get deployed:

- MicroK8s
- Dynatrace OneAgent
- EasyTravel "Classic" with the EasyTravel Launcher App exposed via ingress
- Gitea with org and repo created
- AWX (Ansible Tower open source) installed and configured
- ACE Dashboard with links

## Prerequisites

- A Dynatrace Environment
- A [ServiceNow developer instance](https://developer.servicenow.com/dev.do) (tested with the Tokyo release of ServiceNow)

> Note: while this was tested with ServiceNow Tokyo, screenshots below are from an older release

## Running the sandbox

Check out [ace-box documentation](https://github.com/Dynatrace/ace-box/blob/dev/docs/external-use-case.md) for more information and provite this git repo URL as the use-case!

```
use_case="https://github.com/dynatrace-ace/ace-box-ext-demo-auto-remediation-easytravel.git"
```

In addition, the following extra vars need to be provided:
```
extra_vars = {
  servicenow_instance_id       = <servicenow_instance_id> # e.g. "dev12345"
  servicenow_instance_user     = <servicenow_instance_user> 
  servicenow_instance_password = <servicenow_instance_password>
}
```

## Setting up the demo
In order to run the demo, a few extra steps need to be completed once the ACE-BOX has been provisioned.

Please check the ace dashboard with the link to the use case for more info, or navigate to [Use Case Readme](roles/my-use-case/files/repos/autoremediation-demo/README.md)
