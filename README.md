Deploy Base ArcGIS Enterprise on Single Machine (Windows)

Prerequisites

Required ArcGIS Software Repository Content

Certificate

License

ArcGIS Server service account

Resources

Deployment steps

Step 1: Install Cinc Client

Step 2: Download Chef Cookbooks for ArcGIS

Step 3: Download ArcGIS Enterprise 11.0 Setups

Step 4: Run

Prerequisites
Required ArcGIS Software Repository Content
The following ArcGIS setup archives must be available in the ArcGIS software repository directory for both initial deployments and upgrades:

Windows

·       ArcGIS_DataStore_Windows_114_192943.exe

·       ArcGIS_Server_Windows_114_192938.exe

·       ArcGIS_Server_Windows_114_192938.exe.001

·       ArcGIS_Web_Adaptor_for_Microsoft_IIS_114_192944.exe

·       Portal_for_ArcGIS_Windows_114_192940.exe

·       Portal_for_ArcGIS_Windows_114_192940.exe.001

·       Portal_for_ArcGIS_Web_Styles_Windows_114_192942.exe

·       dotnet-hosting-8.0.6-win.exe (Will be downloaded from the internet if the file is not present)

·       WebDeploy_amd64_en-US.msi (Will be downloaded from the internet if the file is not present)

Certificate
License
·       ArcGIS Enterprise License files for portal and server

ArcGIS Server service account  
Resources
Deployment steps
Step 1: Install Cinc Client
·       Start Windows PowerShell terminal as administrator and run:

·       > . { iwr -useb https://omnitruck.cinc.sh/install.ps1 } | iex; install -version 17

Step 2: Download Chef Cookbooks for ArcGIS
·       arcgis-5.1.0-cookbooks.zip

·       Extract the contents of arcgis-5.1.0-cookbooks.zip archive to C:\cinc

Step 3: Download ArcGIS Enterprise 11.0 Setups
·       The setup archives are downloaded to C:\Software\Archives

·       Create directory C:\Software\AuthorizationFiles\11.0 and copy the software authorization files for 11.0 ArcGIS Server and Portal for ArcGIS to that directory.

·       Create directory C:\Temp and copy the SSL certificate to that directory.

·       Copy file C:\cinc\templates\arcgis-enterprise-base\11.0\windows\arcgis-enterprise-primary.json to C:\cinc

·       Update the required attributes within the template arcgis-enterprise-primary.json file

·       Required attribute changes:

arcgis.run_as_password - (Windows only) password of 'arcgis' Windows user account

arcgis.repository.archives - ArcGIS software repository directory("C:\\Software\\Archives")

arcgis.iis.keystore_file - "C:\\Temp\\.pfx"

arcgis.iis.keystore_password - (Windows only) Specify password of the SSL certificate file

arcgis.server.private_url - ""

arcgis.server.wa_url -"",

arcgis.server.admin_username - "",

arcgis.server.admin_password - Specify primary site administrator account password

arcgis.server.authorization_file - "C:\\Software\\AuthorizationFiles\\11.4\\Server.prvc"

arcgis.server.directories_root - "C:\\arcgisserver"

arcgis.server.config_store_connection_string - "C:\\arcgisserver\\config-store"

arcgis.server.system_properties.WebContextURL - ""

arcgis.data_store.data_dir - "C:\\arcgisdatastore"

arcgis.data_store.backup_location - "C:\\arcgisbackup\\relational"

arcgis.portal.wa_url - ""

arcgis.portal.private_url - ""

arcgis.portal.admin_username - ""

arcgis.portal.admin_email - ""

arcgis.portal.admin_full_name - ""

arcgis.portal.security_question - "What city were you born in?"

arcgis.portal.authorization_file - "C:\\Software\\AuthorizationFiles\\11.4\\Portal.json"

arcgis.portal.user_license_type_id - “creatorUT"

arcgis.web_adaptor.dotnet_setup_path - "C:\\Software\\Archives\\dotnet-hosting-8.0.6-win.exe"

arcgis.web_adaptor.web_deploy_setup_path - "C:\\Software\\Archives\\WebDeploy_amd64_en-US.msi"

Step 4: Run
·       Start a command prompt window as administrator and run:

> cinc-client -z -j arcgis-enterprise-primary.json
