# vPackets - Deploy NSX-T Infrastructure - Simple Topology



by Nicolas MICHEL [@vpackets](https://twitter.com/vpackets) / [LinkedIn](https://www.linkedin.com/in/mclnicolas/) / [Blog](http://vpackets.net/) 

_**This disclaimer informs readers that the views, thoughts, and opinions expressed in this series of posts belong solely to the author, and not necessarily to the author’s employer, organization, committee or other group or individual.**_

## Introduction

The purpose of this entire repository is to automate the deployment of my NSX-T infrastructure in my lab.

Before running the code, you need to fill all the variables in the answerfile.yml file. These variables are unique to your infrastructure.

You also need to have a valid NSX-T license in order to deploy the edge node.

### Infrastructure Deployed

This repository will deploy the following virtual machines:

- 1x NSX-T Manager
- 6x NSX-T Edge
- 5x Cumulus VX (4 Top of Rack and 1 Spine)
____

This repository will configure the following on NSX-T:

- NSX-T: Compute Manager
- NSX-T: License
- NSX-T: Uplink Profiles
- NSX-T: IP Pools
- NSX-T: Transport Zones
- NSX-T: Transport Zones Profiles
- NSX-T: Transport Nodes
- NSX-T: Edge Clusters
____



### Code Tree


-----
.
├── README.md
├── deploy.yml
├── playbooks
│   ├── 01-deploy-nsxtmanager.yml
│   ├── 02-configure-compute-manager.yml
│   ├── 03-configure-nsxtmanager-license.yml
│   ├── 04-configure-nsxtmanager-uplinkprofiles.yml
│   ├── 05-configure-nsxtmanager-ippools.yml
│   ├── 06-configure-nsxtmanager-transportzones.yml
│   ├── 07-configure-nsxtmanager-transportnodesprofiles.yml
│   ├── 08-configure-nsxtmanager-transportnodes.yml
│   ├── 09-deploy-edgenodes.yml
│   ├── 10-configure-nsxtmanager-edgeclusters.yml
│   ├── 11-deploy-cumulus.yml
│   ├── 95-delete-nsxtmanager-edgeclusters.yml
│   ├── 96-delete-edgenodes.yml
│   ├── 97-unconfigure-nsxtmanager-transport-collections.yml
│   ├── 98-unconfigure-nsxtmanager-transportnodes.yml
│   ├── 99-unconfigure-compute-manager.yml
│   ├── library
│   │   ├── __init__.py
│   │   ├── nsxt_accept_eula.py
│   │   ├── nsxt_certificates.py
│   │   ├── nsxt_certificates_facts.py
│   │   ├── nsxt_compute_collection_fabric_templates.py
│   │   ├── nsxt_compute_collection_fabric_templates_facts.py
│   │   ├── nsxt_compute_collection_transport_templates.py
│   │   ├── nsxt_compute_collection_transport_templates_facts.py
│   │   ├── nsxt_deploy_ova.py
│   │   ├── nsxt_edge_clusters.py
│   │   ├── nsxt_edge_clusters_facts.py
│   │   ├── nsxt_fabric_compute_managers.py
│   │   ├── nsxt_fabric_compute_managers_facts.py
│   │   ├── nsxt_fabric_nodes.py
│   │   ├── nsxt_fabric_nodes_facts.py
│   │   ├── nsxt_ip_blocks.py
│   │   ├── nsxt_ip_blocks_facts.py
│   │   ├── nsxt_ip_pools.py
│   │   ├── nsxt_ip_pools_facts.py
│   │   ├── nsxt_licenses.py
│   │   ├── nsxt_licenses_facts.py
│   │   ├── nsxt_logical_ports.py
│   │   ├── nsxt_logical_ports_facts.py
│   │   ├── nsxt_logical_router_ports.py
│   │   ├── nsxt_logical_router_ports_facts.py
│   │   ├── nsxt_logical_router_static_routes.py
│   │   ├── nsxt_logical_routers.py
│   │   ├── nsxt_logical_routers_facts.py
│   │   ├── nsxt_logical_switches.py
│   │   ├── nsxt_logical_switches_facts.py
│   │   ├── nsxt_manager_auto_deployment.py
│   │   ├── nsxt_manager_auto_deployment_facts.py
│   │   ├── nsxt_manager_status.py
│   │   ├── nsxt_policy_bfd_config.py
│   │   ├── nsxt_policy_gateway_policy.py
│   │   ├── nsxt_policy_group.py
│   │   ├── nsxt_policy_ip_block.py
│   │   ├── nsxt_policy_ip_pool.py
│   │   ├── nsxt_policy_security_policy.py
│   │   ├── nsxt_policy_segment.py
│   │   ├── nsxt_policy_tier0.py
│   │   ├── nsxt_policy_tier1.py
│   │   ├── nsxt_principal_identities.py
│   │   ├── nsxt_principal_identities_facts.py
│   │   ├── nsxt_repo_sync.py
│   │   ├── nsxt_repo_sync_facts.py
│   │   ├── nsxt_route_advertise.py
│   │   ├── nsxt_transport_node_collections.py
│   │   ├── nsxt_transport_node_collections_facts.py
│   │   ├── nsxt_transport_node_profiles.py
│   │   ├── nsxt_transport_node_profiles_facts.py
│   │   ├── nsxt_transport_nodes.py
│   │   ├── nsxt_transport_nodes_facts.py
│   │   ├── nsxt_transport_zones.py
│   │   ├── nsxt_transport_zones_facts.py
│   │   ├── nsxt_upgrade_eula_accept.py
│   │   ├── nsxt_upgrade_eula_accept_facts.py
│   │   ├── nsxt_upgrade_groups.py
│   │   ├── nsxt_upgrade_groups_facts.py
│   │   ├── nsxt_upgrade_history.py
│   │   ├── nsxt_upgrade_plan.py
│   │   ├── nsxt_upgrade_plan_facts.py
│   │   ├── nsxt_upgrade_postchecks.py
│   │   ├── nsxt_upgrade_pre_post_checks_facts.py
│   │   ├── nsxt_upgrade_prechecks.py
│   │   ├── nsxt_upgrade_run.py
│   │   ├── nsxt_upgrade_status_summary_facts.py
│   │   ├── nsxt_upgrade_uc.py
│   │   ├── nsxt_upgrade_uc_facts.py
│   │   ├── nsxt_upgrade_upload_mub.py
│   │   ├── nsxt_upgrade_upload_mub_facts.py
│   │   ├── nsxt_uplink_profiles.py
│   │   ├── nsxt_uplink_profiles_facts.py
│   │   ├── nsxt_virtual_ip.py
│   │   ├── nsxt_virtual_ip_facts.py
│   │   └── nsxt_vm_tags.py
│   ├── module_utils
│   │   ├── __init__.py
│   │   ├── common_utils.py
│   │   ├── nsxt_base_resource.py
│   │   ├── nsxt_resource_urls.py
│   │   ├── policy_communicator.py
│   │   ├── policy_resource_specs
│   │   │   ├── __init__.py
│   │   │   └── security_policy.py
│   │   ├── vcenter_utils.py
│   │   └── vmware_nsxt.py
│   └── plugins
│       └── doc_fragments
│           └── vmware_nsxt.py
-----



# Deployment

## 01 - Deploy NSX-T Manager

Only one NSX-T Manager will be deployed in this Lab environment.

## 02 - Configure Compute Manager

In the first task, the playbook will check if the vCenter is registered as a compute manager to the NSX-T Manager. Since the intent of this entire repository is to deploy a greenfield lab environment, this step is not necessary but it has been useful to run that task in some corner cases for my lab (hence why the code is still there).

The second task will register the vCenter as a computer manager to the NSX-T Manager.

## 03 - Add a license to the NSX-T Manager.

This playbook will configure a license (NSX Data Center Enterprise Plus)to the NSX-Manager.

## 04 - Configure the NSX-T Uplink Profiles.

2 uplink profiles will be created:

- Compute:
  - Default Teaming Policy for the TEP: PNIC-01 (uplink-1) and PNIC-02 (uplink-2)
  - Policy: Loadbalance Src ID
  - Vlan 110

- Edge:
  - Default Teaming Policy for the TEP: PNIC-01 (uplink-1) and PNIC-02 (uplink-2)
  - Policy: Loadbalance Src ID
  - Vlan 120
  - Named Teaming Policy: 
    - TOR-1 : 
      - Uplink-1
      - Failover Order
    - TOR-2 : 
      - Uplink-2
      - Failover Order

It is unnecessary to configure the MTU for the uplink profile as the MTU is handled at the vSphere level since we are using a VDS instead of an NVDS for the compute managers.


## 05 - Configure IP Pools

2 IP Pools are created for the TEP. One pool will be dedicated for the Compute Servers and one pool will be dedicated for the Edge Virtual Machines. It is totally supported to have all the TEPs in the same pool but I wanted to create 2 pools to demonstrate that Layer 3 between the compute and edge racks was a totally valid architecture for NSX-T

## 06 - Transport Zones:

2x Transport zones are created in this playbook. One transport zone is for the Overlay while the other one is a Vlan Transport zone.


## 07 - Configure the Transport Nodes Profile:

This playbook creates a Transport Node Profile for the compute hosts.
It is necessary when you want to configure all host in a cluster so that they leverage the same template. 

- Type: VDS
- Mode: Standard
- Compute Manager: vCenter
- VDS: ATX-VDS
- Transport Zone: Overlay (the compute hosts have no need to be part of the VLAN Transport Zone in this architecture)
- Uplink Profile: UP-Compute
- IP Assignement: 
  - IP pool:
    - IPPool-IPV4-TEP-COMPUTE
- Teaming Policy
  - uplink1 : dvUplink-1
  - uplink2 : dvUplink-2

## 08 - Configure the Transport Nodes:

This playbook will instal NSX-T on all the hosts that are part of the Compute cluster.

## 09 - Deploy the Edge Nodes:

This playbook will install several NSX-T Edge (6) to match the architecture needs.

- Form Factor: 
  - Medium
- Edge Switch Name: 
  - EDGE-NVDS
- Transport Zone:
  - Overlay (Inter Edge - Compute Traffic)
  - VLAN (Traffic exchanged with the physical fabric)
- Uplink Profile:
  - UP-Edge
- IP Assignement:
  - Use IP Pool
    - IPPool-IPV4-TEP-EDGE
- Teaming Policy
  - Uplink-1 : DPG-TRUNK-TOR-01
  - Uplink-2 : DPG-TRUNK-TOR-02


DPG Trunk TOR 01 has the following Teaming configuration (vSphere related):
- Active uplinks:
  - dvUplink1
- Standby uplinks:
  - dvUplink2 
- Unused uplinks:
  -  dvUplink3, dvUplink4 

DPG Trunk TOR 02 has the following Teaming configuration (vSphere related):
- Active uplinks:
  - dvUplink2
- Standby uplinks:
  - dvUplink1 
- Unused uplinks:
  -  dvUplink3, dvUplink4 

## 10 - Configure the Edge Clusters on the NSX-T Manager:

This playbook will group the edge nodes in pairs. The default nsx-default-edge-high-availability-profile will be used as it fulfill our needs (BFD Probe 500ms / BFD Declare dead 3)

- Edge cluster 01:
  - Edge node 01
  - Edge node 02

- Edge cluster 02:
  - Edge node 03
  - Edge node 04

- Edge cluster 03:
  - Edge node 05
  - Edge node 06

## 11 - Deploy Cumulus VX Top of Rack and Spine.:

This playbook will deploy 5 Cumulus VX. 
4 Cumulus VX will act as Top of Racks for the NSX-T Architecture. The remaining cumulus VX will be the Spine that will interconnect all the networks (physical and virtual).

## Running the main playbook

```sh
sudo ansible-playbook deploy.yml
```

# To Do List:

- Bring down the environment.
- Readme doc with links and images

## Timing
Time on my hardware: 1 hour and 51 minutes

## Notes 
The answerfile-json is here as an example and to check if I can improve the code using json instead of yml.