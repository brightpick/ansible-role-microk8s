Ansible role: microk8s
=========

![main Build status](https://github.com/Provizanta/ansible-role-microk8s/actions/workflows/main.yml/badge.svg)

Install and configure a microk8s Kubernetes instance

Requirements
------------

None

Role Variables
--------------

These variables are defined in [defaults/main.yml](./defaults/main.yml):

    microk8s_addons: []

    microk8s_hosts: {}

    microk8s_channel: "latest/stable"

    microk8s_extra_args: {}     # key: file in /var/snap/microk8s/current/args/, value: extra content

    microk8s_update: true

    microk8s_drain_node_on_update: false

    # kubelet uses pflag to process arguments
    # its behavior is to use the last value of a repeated flag
    microk8s_kubelet_additional_args: []

Dependencies
------------

None

Example Playbook
----------------

    - name: Converge
      hosts: all
      roles:
        - role: ansible-role-microk8s
          vars:
            microk8s_drain_node_on_update: true
            microk8s_addons:
              - dns
              - storage
            microk8s_channel: latest/stable
            microk8s_hosts:
              # add insecure registry at registry.example.com
              registry.example.com: |
                server = "http://registry.example.com"

                [host."http://registry.example.com"]
                capabilities = ["pull", "resolve"]
            microk8s_extra_args:
              containerd: |
                -l=debug
            microk8s_kubelet_additional_args:
              - --rotate-certificates=true
              - --rotate-server-certificates=true

License
-------

MIT

Author Information
------------------

Tibor Csóka
