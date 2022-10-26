# app-easytravel-classic

This currated role can be used to deploy EasyTravel one the ACEBOX including the web launcher.
This role does not reploy EasyTravel on Kubernetes, but rather directly on the VM

## Using the role

### Role Requirements
Tthis role has no direct dependencies on other roles.

### Deploying EasyTravel

```yaml
- include_role:
    name: app-easytravel-classic
```

Variables that can be set are as follows:

```yaml
---
easytravel_classic_download_location: "{{ role_path }}/files/dynatrace-easytravel-linux-x86_64.jar"
easytravel_classic_install_location: "{{ role_path }}/files/easytravel-2.0.0-x64"
easytravel_classic_apache_port: 8079 #Which port on the local machine exposes EasyTravel
easytravel_classic_launcher_port: 8094 #Which port on the local machine exposes EasyTravel Launcher
easytravel_classic_domain: "easytravel-classic.{{ ingress_domain }}" # (Opt)When leveraging an ingress controller, which domain to use for EasyTravel
easytravel_classic_launcher_domain: "easytravel-launcher.{{ ingress_domain }}" # (Opt)When leveraging an ingress controller, which domain to use for EasyTravel Launcher
easytravel_classic_namespace: "easytravel-classic" # (Opt) when using the ingress capabilities, in which namespace to deploy the kubernetes resources
easytravel_classic_release_stage: "easytravel-classic" # For the Release Inventory, which Stage to set
```

### (Optional) To enable observability with Dynatrace OneAgent

> Note: Since EasyTravel Classic is not deployed on Kubernetes, the operator cannot be used and the OneAgent must be deployed using the installer
```yaml
- include_role:
    name: dt-oneagent-classic
```


### Configure Dynatrace using Monaco

To enable monaco:

```yaml
- name: Deploy Monaco
  include_role:
    name: monaco
```

> Note: the below applies Dynatrace configurations with the monaco project embedded in the role

```yaml
- include_role:
    name: app-easytravel-classic
    tasks_from: apply-monaco
```

To delete the configuration:

```yaml
- include_role:
    name: app-easytravel
    tasks_from: delete-monaco
```

Dynatrace Configurations List:

    Infrastructure:
      - "auto-tag/app"
      - "auto-tag/environment"
      - "conditional-naming-processgroup/ACE Box - containername.namespace"
      - "conditional-naming-service/app.environment"
      - "synthetic-location/ACE-BOX"
    
    Easytravel Aplication Specific:
        - "app-detection-rule/app.easytravel.prod"
        - "app-detection-rule/app.easytravel-angular.prod"
        - "application-web/app.easytravel.prod"
        - "application-web/app.easytravel-angular.prod"
        - "auto-tag/easytravel-prod"
        - "management-zone/easytravel-prod"
        - "synthetic-monitor/webcheck.easytravel.prod"
        - "synthetic-monitor/webcheck.easytravel-angular.prod"
        - "synthetic-monitor/browser.easytravel-angular.prod.home"
        - "synthetic-monitor/browser.easytravel.prod.home"