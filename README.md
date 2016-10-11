### Introduction
#### Install a Docker image from the online Package repository

The Docker installer for Windows is now available in an online package repository.  They can be found and installed using the Docker provider of PackageManagement (a.k.a. <a href="http://www.oneget.org">OneGet</a>) PowerShell module.  The provider needs to be installed before using it. The following PowerShell cmdlets can be used to install the provider.
* Import-Module -Name Docker -Force
* Import-Packageprovider -Name Docker -Force

Once the provider is installed and imported, you can search, download, or install Docker using OneGet PowerShell cmdlets:
* Find-Package
* Save-Package
* Install-Package
* Uninstall-Package
* Get-Package

#### Register a source

##### Register an URL to be used with DockerMsftProvider
	Register-PackageSource -ProviderName DockerMsftProvider -Name AlternateSource -Location https://contoso.com/metaData.json

##### Enlist all the registered sources
	Get-PackageSource -ProviderName DockerMsftProvider

#### Search a Docker installer 

##### Example 1: Find the latest version of all available Docker installers. 
	Find-Package –providerName DockerMsftProvider
   
##### Example 2: Search by version, according to –RequiredVersion, -MinimumVersion, and –MaximumVersion requirements. With –AllVersions parameter, all available versions of Docker installers are returned. Without it, only the latest version is returned.
    Find-Package –providerName DockerMsftProvider –AllVersions

#### Install docker

##### Example 1: Install the latest version of docker to the local machine.
	Install-Package -Name docker -ProviderName DockerMsftProvider -Verbose

##### Example 2: Install docker with pipeline result from the search cmdlets.	
	Find-Package –ProviderName DockerMsftProvider | Install-Package -Verbose

#### Download Docker
You can download and save Docker installer without installation, using Save-Package. This cmdlet accepts pipeline result from the search cmdlets. If you have multiple sources, please provide the source for download.

##### Example 1: Download and save Docker installer to a directory that matches the wildcard path. The latest version will be saved if you do not specify the version requirements.	
	Save-Package –ProviderName DockerMsftProvider -Name Docker -Path .\temp -MinimumVersion 1.2.3

##### Example 2: Download and save Docker installer from the search cmdlets.
	Find-package –ProviderName DockerMsftProvider | Save-Package -Path .

#### Get docker

##### Example 1: Inventory docker installation on the local machine.
	 Get-Package –ProviderName DockerMsftProvider

#### Uninstall docker
Uninstalls Docker from the local machine.

##### Example 1: Uninstall docker from the local machine.
	Uninstall-Package -ProviderName DockerMsftProvider -Name dOcKeR -Verbose

#### Update docker
Updates current installation of docker with the requested version

##### Example 1: Update docker
	Install-Package -Name docker -ProviderName DockerMsftProvider -Verbose -Update

### Version
0.1.0.0

### Version History

#### 0.1.0.0
	Initial release

#### 0.1.0.1
	Bug fixes

#### 0.1.0.2
	Bug fixes

#### 0.1.0.3
	Bug fixes

### Dependencies
1. Nuget binaries