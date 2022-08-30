# dev_Multi-R
Deployment and Management of Multiple Versions of R Workspace and Notes

##### Links
- [https://support.rstudio.com/hc/en-us/articles/215488098-Installing-multiple-versions-of-R-on-Linux](https://support.rstudio.com/hc/en-us/articles/215488098-Installing-multiple-versions-of-R-on-Linux) <br/>

- [https://docs.rstudio.com/ide/server-pro/r-versions.html](https://docs.rstudio.com/ide/server-pro/r-versions.html) <br/>

##### Install Required Dependencies - RHEL 7
```
# Enable the Extra Packages for Enterprise Linux (EPEL) repository
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm 

# On RHEL 7, enable the Optional repository
sudo subscription-manager repos --enable "rhel-*-optional-rpms"

# If running RHEL 7 in a public cloud, such as Amazon EC2, enable the
# Optional repository from Red Hat Update Infrastructure (RHUI) instead
sudo yum install yum-utils
sudo yum-config-manager --enable "rhel-*-optional-rpms"
```

##### Specify R Version
`$export R_VERSION=4.1.3` <br/>

** Ansible Setting Environment Variable: <br/>
```
- name: Install R v4.x
  yum:
    name: https://cdn.rstudio.com/r/centos-7/pkgs/R-4.2.1-1-1.x86_64.rpm
#   name: https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm
    state: present
  environment:
    R_VERSION: 4.2.1
```

##### Download and Install R - RHEL 7
```
$curl -O https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm
$sudo yum install R-${R_VERSION}-1-1.x86_64.rpm
```


##### R RPM is a meta package that installs the following components
`$sudo dnf install R` <br/> 

| Component	     | Description                                                  |
|:---------------|:------------------------------------------------------------ | 
| R-core	       | The minimal R components necessary for a functional runtime  |
| R-core-devel	 | Core files for development of R packages (no Java)           |
| R-java	       | R with Fedora-provided Java Runtime Environment.             | 
| R-java-devel	 | Development package for use with Java enabled R components.  |
| libRmath	     | Standalone math library from the R project                   |
| libRmath-devel | Headers from the R standalone math library.                  |

#### Switch R Versions for RStudio Desktop
```
$export RSTUDIO_WHICH_R=/usr/bin/R4.2.1
$ssh -Y <system> rstudio

## Exit
$export RSTUDIO_WHICH_R=/usr/bin/R3.6.0
$ssh -Y <system> rstudio
```
