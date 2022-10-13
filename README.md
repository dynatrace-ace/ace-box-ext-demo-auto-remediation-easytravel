# ace-box-ext-demo-auto-remediation-easytravel

This ACE-BOX external use case is a demo for auto remediation using Ansible and the EasyTravel App.
This also leverages ServiceNow.

## Components deployed

The following components get deployed:

- microk8s
- Dynatrace Operator with OneAgent and Kubernetes ActiveGates
- Dynatrace CloudAutomation (Keptn)
- Sonarqube
- Dashboard with predefined links

## Running the sandbox

Check out [ace-box documentation](https://github.com/Dynatrace/ace-box/blob/dev/docs/external-use-case.md) for more information and provite this git repo URL as the use-case!

```
use_case="https://github.com/dynatrace-ace/ace-box-sandbox-github-actions.git"
```

In addition, the following extra vars need to be provided:
```
extra_vars = {
  servicenow_instance_id       = <servicenow_instance_id> # e.g. "dev12345"
  servicenow_instance_user     = <servicenow_instance_user> 
  servicenow_instance_password = <servicenow_instance_password>
}
```

## References

- https://github.com/SonarSource/helm-chart-sonarqube
