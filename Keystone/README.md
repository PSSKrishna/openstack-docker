Note: Use this when you are willing to create own docker image easily & use as a templates, 
      if not then go to above shown directory From Docker image and download keystone docker image

# Docker Image Contains:
> centos with systemd
> keystone

Add a User and Database on MariaDB for Keystone
for noobs
---
* create database keystone_db;
* grant all privileges on keystone_db.* to keystone_user@'localhost' identified by 'password'; 
* grant all privileges on keystone_db.* to keystone_user@'%' identified by 'password';
* flush privileges;
* exit

It contains some docker build arguments so you have to create your own docker image 
* keystone_host
* password = adminpassword [ default ]
* keystone_user

# For Creating Docker Image using Dockerfile
* copy keystone folder to your host and get into the directory
* change configuration files as per requirements  ( Basic changes you have to done )
  * for ntp.conf
    use your ntp server for better convenience  
  * for keystone.conf 
    * memcache_servers = ip:11211
    * ( MariaDB connection info ) - change mariadb_host, password, username, database name
      connection = mysql+pymysql://username:password@mariadb_host/database_name
    * search this type of block [token] and changes its provider 
      [token]
      provider = fernet     
* use docker build -t imagename:version --build-arg keystone_host=keystone_host_ip --build-arg password=adminpassword \
     --build-arg keystone_user=keystone_user .
* wait and check the image from docker images
* open respective port of keystone:5000 and 35357, httpd:80 on host

# For Container : 

docker run -d --net=host image_id

If selinux is enabled then
* setsebool -P httpd_use_openstack on 
* setsebool -P httpd_can_network_connect on 
* setsebool -P httpd_can_network_connect_db on 

For Verify Keystone Service ( all commands run for keystone client packages like centos: openstack-utils python-openstackclient)
* export OS_USERNAME=admin
* export OS_PASSWORD=ADMIN_PASSWORD (which is used in docker build command)
* export OS_PROJECT_NAME=admin
* export OS_USER_DOMAIN_NAME=Default
* export OS_PROJECT_DOMAIN_NAME=Default
* export OS_AUTH_URL=http://keystone_host:35357/v3
* export OS_IDENTITY_API_VERSION=3

 for verification create project and user

