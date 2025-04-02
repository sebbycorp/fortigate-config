# FortiGate Configuration Backup

This repository contains the configuration backup for a FortiGate 80F firewall.

## Device Information

- **Hostname**: fw-maniak-hq
- **Model**: FortiGate 80F
- **Serial Number**: FGT80FTK22061709
- **Firmware Version**: v7.4.7, Build 2731
- **Management IP**: 172.16.10.1

## System Configuration

```
{
  "language": "english",
  "hostname": "fw-maniak-hq",
  "alias": "FortiGate-80F",
  "timezone": "US/Eastern",
  "admin-timeout": 5,
  "gui-theme": "jade"
}
```

## Network Interfaces

### Main Interfaces

| Interface | Type | IP Address | Status | Purpose |
|-----------|------|------------|--------|---------|
| BELL_35 | PPPoE | 74.12.8.53/32 | up | WAN |
| internal | hard-switch | 172.16.99.1/24 | up | Internal LAN |
| fortilink | aggregate | 10.255.1.1/24 | up | FortiSwitch Management |
| dev-ntw | VLAN (99) | 192.168.86.1/24 | up | Development Network |

### Other Interfaces

- **a**: Physical interface (part of fortilink aggregate)
- **b**: Physical interface (part of fortilink aggregate)
- **internal1**: Physical interface
- **internal2**: Physical interface

## Firewall Policies

### Policy 1: nat-internal-out

```
{
  "policyid": 1,
  "status": "enable",
  "name": "nat-internal-out",
  "srcintf": [{"name": "internal"}],
  "dstintf": [{"name": "BELL_35"}],
  "action": "accept",
  "srcaddr": [{"name": "all"}],
  "dstaddr": [{"name": "all"}],
  "service": [{"name": "ALL"}],
  "nat": "enable",
  "logtraffic": "disable",
  "utm-status": "disable"
}
```

### Policy 2: corp

```
{
  "policyid": 2,
  "status": "enable",
  "name": "corp",
  "srcintf": [{"name": "corp"}],
  "dstintf": [{"name": "BELL_35"}],
  "action": "accept",
  "srcaddr": [{"name": "all"}],
  "dstaddr": [{"name": "all"}],
  "service": [{"name": "ALL"}],
  "nat": "enable",
  "logtraffic": "all",
  "utm-status": "enable"
}
```

## Address Objects

The configuration includes the following custom address object:

- **mcpdemo_subnet**: 172.31.0.0/24

## Address Groups

The configuration includes the following address group:

- **mcpdemo**: Contains the address object "mcpdemo_subnet"

## Backup Information

This configuration was exported on April 2, 2025, using the FortiGate REST API.

---

### How to Use This Configuration

This backup can be used as a reference for the current configuration state of the firewall. To restore this configuration:

1. Access the FortiGate web interface
2. Navigate to Administration > Configuration > Backup
3. Upload the configuration file

For specific configuration changes, it's recommended to use the FortiGate CLI or Web UI directly.

### API Access

The FortiGate can be managed via its REST API. Example curl commands:

```bash
# Get firewall policies
curl -k -X GET "https://172.16.10.1/api/v2/cmdb/firewall/policy" \
  -H "Authorization: Bearer YOUR_API_TOKEN"

# Get interfaces configuration
curl -k -X GET "https://172.16.10.1/api/v2/cmdb/system/interface" \
  -H "Authorization: Bearer YOUR_API_TOKEN"
```

*Note: Replace YOUR_API_TOKEN with a valid API token.*