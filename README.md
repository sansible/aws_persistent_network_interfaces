# AWS Persistent Network Interfaces

Attaches an AWS ENI and configues it for use.




## Role Variables

Check [default variables](defaults/main.yml) for more details.




## Example Playbook

This example assumes EC2 has a tag named "instanceeniid" with ENI id. That ENI will
be attached as `eth1`

```YAML
- role: sansible.aws_persistent_network_interfaces
```

This example will attach third ENI as `eth1`. The ENI needs to be in the same AZ and have
tags "Environment" and "Application"

```YAML
- role: sansible.aws_persistent_network_interfaces
  sansible_persistent_network_interfaces_device_index: 2
  sansible_persistent_network_interfaces_aws:
    assigned_eni_instance_tag: ~
    tagged_eni_lookup_filters:
      "tag:Environment": dev
      "tag:Application": my-application
```

This example will attach second ENI as `ens6`. The ENI needs to be in the same AZ and it's
Id needs to be saved in EC2 instance tag named "eniid"

Check which instance types uses enhanced networking and as a result network interfaces
are named ens5 (instead eth0), ens6, ...
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/enhanced-networking.html

```YAML
- role: sansible.aws_persistent_network_interfaces
  sansible_persistent_network_interfaces_device_name: ens6
  sansible_persistent_network_interfaces_device_index: 1
  sansible_persistent_network_interfaces_aws:
    assigned_eni_instance_tag: eniid
```
