# For Creating Docker Image from Dockerfile

* copy the proxy folder in your host
* config the configurations file as per requirements
  > ntp server
  > swift.conf
  > proxy-server.conf
 
* swift.conf - as per requirements and reference with https://docs.openstack.org/swift/queens/install/finalize-installation-rdo.html
* proxy-server.conf - as per requirements and reference with https://docs.openstack.org/swift/queens/install/controller-install-rdo.html

# For building docker image
* use docker build -t imagename:version .
* launch container instance with --net=host and run swift-ring-builder commands with storage nodes arguments take reference from 
https://docs.openstack.org/swift/queens/install/initial-rings.html
* run chown swift. /etc/swift/*.gz
* restart your all services or restart your container 
* open respective port on host  8080 .
* make image of your container and launch many instances of it .
* after this you can move towards to installation of swift-storage nodes

* Copy all the ring files from proxy node to storage nodes for this copy all the ring files to files folder of storage.
* then use storage docker file 

or another method to done this

# download docker image  
docker pull baba230896/swift-proxy
* then perform required changes in configuration, swift-ring-builder configurations and in last 
* restart services. make  image of your container and lanuch instance.

