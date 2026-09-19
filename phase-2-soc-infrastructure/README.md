# Phase 2 — SOC Infrastructure

## Objective

Deploy and validate the central SOC infrastructure using Wazuh.

## Components

- Wazuh Manager 4.14.7
- Wazuh Indexer 4.14.7
- Wazuh Dashboard 4.14.7
- Wazuh API
- Ubuntu Server 24.04.5 LTS

## Deployment

The Wazuh stack was deployed as an all-in-one installation on the
dedicated `wazuh-server` VM.

### Wazuh Server

| Property | Value |
|---|---|
| Hostname | `wazuh-server` |
| OS | Ubuntu Server 24.04.5 LTS |
| vCPU | 4 |
| RAM | 6 GB |
| SOC-LAB IP | `10.10.10.103` |
| API Port | `55000` |

## Network

The Wazuh server is connected to the isolated `soc-lab` network:

`10.10.10.0/24`

The lab is isolated from the physical/home network.

## Validation

The following services were verified as operational:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Wazuh API

The Dashboard was successfully accessed from the host system.

The Dashboard API connection was verified as:

**ONLINE**

The Wazuh API was also directly tested on port `55000`.

## Architecture

```text
                    SOC-LAB
                 10.10.10.0/24
                       |
                       |
              +------------------+
              |   Wazuh Server   |
              |  10.10.10.103    |
              |                  |
              | Wazuh Manager    |
              | Wazuh Indexer    |
              | Wazuh Dashboard  |
              | Wazuh API :55000 |
              +------------------+
                       |
             ---------------------
             |                   |
        Windows 11             Kali
        Endpoint              Attacker