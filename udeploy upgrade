# Steps to migration
1. raise SN request to ICG GL PA UDEPLOY REQUEST to kick off the migration.
  may need fill team details in form attached in [udeploy guide] 
   
2. work with SA to install new agents onto servers to which we need install packages via udeploy
	https://collaborate.citi.net/docs/DOC-371753
	
prepare the packages 

```sh
	mkdir /tmp/udeploy_install;
	cd /tmp/udeploy_install;
	cp /net/stealth/export1/home1.localhost/sw/Linux/uDeploy_Agent_6.2.0.0.707419.tar /tmp/udeploy_install/;
	tar -xf /tmp/udeploy_install/uDeploy_Agent_6.2.0.0.707419.tar;
```
ask SA to run following command with root to install
	
```sh
	cd /tmp/udeploy_install/ibm-ucd-agent-install;
	./install-agent-linux.sh prod
```	

3. Map your components with resources/groups once resource/agent is available in 6.2 HA env. please refer to [env mapping]. general steps are listed below:
* 
	 
	
> udeploy 6.2 integration with Hermes is not available yet. so need update packages manually with udclient.
so use [udagent] to upload rpms to udeploy 6.2
```sh
cd C:\citi\Ref Data\udeploy upgrade
.\udclient -weburl https://releasedeployment.ti.citigroup.net:8443 -username sw92854 login
udclient -weburl https://releasedeployment.ti.citigroup.net:8443 createVersion -component DataProcessService -name DataProcessService_2.0_D5-1598806
udclient -weburl https://releasedeployment.ti.citigroup.net:8443 addVersionFiles -component DataProcessService -version DataProcessService_2.0_D5-1598806 -base C:\citi\localPackages\DataProcessService
```	
> if any issues please refer to [udeploy guide] 

   [udagent]: <https://releasedeployment.ti.citigroup.net:8443/tools/udclient.zip>
   [udeploy guide]: <https://collaborate.citi.net/groups/application-and-release-management/blog/2016/05/26/migration-to-udeploy-62-ha-env>
   [env mapping]: <https://www.ibm.com/support/knowledgecenter/SS4GSP_6.1.2/com.ibm.udeploy.doc/topics/app_environment_mapping.html>
