# ACI with Custom DNS

## Change YAML settings
Change the networkProfile and Location to fit your Vnet / Subnet with Microsoft.ContainerInstance/containerGroups delegation

## Get the network profile of an existing Vnet
```
az network profile list --resource-group GROUP  --query [0].id --output tsv
```

## Create the Container Group
Create the Resourcegroup in the same region
```
az group create --name myResourceGroup --location northeurope
az container create --resource-group myResourceGroup --file aci_dns.yaml

az container exec -g MyResourceGroup --name myContainerGroup --container-name aci-tutorial-app --exec-command "/bin/sh"

/usr/src/app # /bin/cat /etc/resolv.conf
nameserver 8.8.8.8
```
### Reference

ACI API: https://docs.microsoft.com/en-us/rest/api/container-instances/containergroups/createorupdate
```
   "dnsConfig": {
      "nameServers": [
        "1.1.1.1"
      ],
      "searchDomains": "cluster.local svc.cluster.local",
      "options": "ndots:2"
    },
```
ACI Container Group YAML Reference: https://docs.microsoft.com/de-de/azure/container-instances/container-instances-reference-yaml
