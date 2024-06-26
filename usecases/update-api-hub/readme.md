

## update ApiHub and buils SSApps use case

Update the installation of ApiHub with new configuration (eg. updated bdns).

Chart name: update-api-hub-info <br/>
Plugin : update-api-hub-info

### Update ApiHub installation configuration

#### Step 1: Clone your private config repository in the folder "private_configs"


1. After the repository was cloned, change the directory to the "private_configs" folder
```shell
cd private_configs
```
2. Create a folder which will represent your installation, like "network_name/charts/epi-update-api-hub-info" and change the directory to that folder
```shell
cd network_name/charts/epi-update-api-hub-info
```

#### Step 2: Install the helm chart and the plugin

1. Register the official, or the forked helm charts repository
```shell
helm repo add helm-charts https://raw.githubusercontent.com/axiologic-pla/helm-charts/master/charts/releases
```
2. Install the helm chart _update-api-hub-info_
```shell
helm pull helm-charts/update-api-hub-info --untar
```
3. Install the _update-api-hub-info_ plugin
```shell
helm plugin install https://github.com/axiologic-pla/helm-charts/plugins/update-api-hub-info
```

#### Step 3: Adjust private_configs/network_name/charts/epi-update-api-hub-info/update-api-hub-info/values.yaml

The file contains parametrization for different sets of values:
1. specific data for the download of the public shared information
2. specific data for the use case network, company name, etc.
3. different annotations or configurations for the deployment

#### Step 4: Install the helm chart

1. Use the _update-api-hub-info_ plugin to aggregate and generate the new updated configuration. 
   The execution of the plugin will produce:
   1. _update-api-hub-info.plugin.json_ file that will contain all the generated information, like bdns, etc. The json file will be used by the helm charts.
   
   
```shell
helm update-api-hub-info -i ./values.yaml -o .
```

2. Install the helm chart
```shell
helm install update-api-hub-info . -f ./values.yaml
```

#### Step 5: Backup your installation and private information

Upload to your private repository all the data located in the folder _private_configs/network_name/charts/epi-update-api-hub-info_


