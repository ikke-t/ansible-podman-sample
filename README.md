# Ansible Podman Examples


This repo is for publishing some examples how to use ansible to automatize
containers using podman.

# To get started

Naturally, do have ansible installed. Then setup the project:

```
git clone https://github.com/ikke-t/ansible-podman-sample.git
cd ansible-podman-sample
```

get dependencies:

```
ansible-galaxy role install -r roles/requirements.yml -p roles
ansible-galaxy collection install -r collections/requirements.yml -p collections

```

# Grafana

To setup grafana, do run:

```
cp roles/ikke_t.grafana_podman/tests/test.yml run-container-grafana-podman.yml
ansible-playbook -i edge, -u cloud-user -b \
  -e container_state=running \
  run-container-grafana-podman.yml
```

If you are on RHEL Edge target, do add the package manager info:

```
ansible-playbook -i edge, -u cloud-user -b \
  -e container_state=running \
  -e ansible_pkg_mgr=atomic_container \
  run-container-grafana-podman.yml
```

To delete grafana, do run:

```
ansible-playbook -i edge, -u cloud-user -b \
  -e container_state=absent  \
  -e nuke=true \
  -e ansible_pkg_mgr=atomic_container \
  run-container-grafana-podman.yml
```

Be careful with the nuke option, as it will also remove the user.


Author: Ilkka Tengvall
License: BSD
