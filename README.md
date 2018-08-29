# Custom JupyterHub Templates for Pangeo Binderhub

## Usage

This repository should be referenced from the values.yaml file in your BinderHub deployment.

```yaml
template:
  path: "/etc/binderhub/templates/templates"
  static:
    path: "/etc/binderhub/templates/static"
    urlPrefix: extra_static/

initContainers:
  - name: git-clone-templates
    image: alpine/git
    args:
      - clone
      - --single-branch
      - --branch=master
      - --
      - https://github.com/pangeo-data/pangeo-custom-binderhub-templates.git
      - /etc/binderhub/templates
    securityContext:
      runAsUser: 0
    volumeMounts:
      - name: custom-templates
        mountPath: /etc/binderhub/templates
extraVolumes:
  - name: custom-templates
    emptyDir: {}
extraVolumeMounts:
  - name: custom-templates
    mountPath: /etc/binderhub/templates
```
