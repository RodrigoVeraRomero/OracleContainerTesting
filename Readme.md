# Oracle Database on Container AND Application inserting demo data
## DOCKER WINDOWS SERVER INSTALATION

### Install Hyper-V Feature
```powershell  
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
```

### Install Docker Windows Fearure
```powershell  
Install-WindowsFeature containers -Restart
```
```powershell  
Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
Get-PackageProvider -ListAvailableget-packagesource -ProviderName DockerMsftProvider
Install-Package -Name docker -ProviderName DockerMsftProvider
Start-Service Docker

```

# Switch to Linux Containers
```powershell  
Set-Content -Value "`{`"experimental`":true`}" -Path C:\ProgramData\docker\config\daemon.json
Restart-Service docker
cd 'C:\Program Files\'
mkdir "Linux Containers"
cd '.\Linux Containers\'
curl -OutFile release.zip https://github.com/linuxkit/lcow/releases/download/v4.14.35-v0.3.9/release.zip
Expand-Archive -DestinationPath . .\release.zip

```

### Download Oracle Oficial Enterprise 19.3.0.0 Image
For enterprise edition you must have oracle account and login <tenancyId>/User
  
```powershell
docker login <region-key>.ocir.io
docker pull container-registry.oracle.com/database/enterprise:19.3.0.0
```
### Download Oracle Oficial Express:21.3.0.0
For this excercise will use this Free Image
```powershell
docker pull container-registry.oracle.com/database/free:23.2.0.0
```
### Run a container in an specific port and password
```powershell
 docker run -dit -p 1521:1521 --memory=4g -v C:\Users\rvradmin\Documents\Oracle:/opt/oracle/oradata -e ORACLE_PWD=Pssword1 --name oracle_db container-registry.oracle.com/database/express:latest
```
