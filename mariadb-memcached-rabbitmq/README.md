# Docker Image Contains: 
> mariadb-server
> memcached 
> rabbitmq
> centos with systemd

Docker image can be download from docker hub: docker pull baba230896/centos_d-mariadb-memcached-rabbitmq

# For Creating Docker image from Dockerfile
* copy mariadb-memcached-rabbitmq folder to your host and get into the directory
* change configuration files as per requirements 
  * for ntp.conf
    use your ntp server for better convenience
  * for my.cnf
    use bind-address as 0.0.0.0 for all devices or as per your ip address of network interface
* use docker build -t imagename:version .
* wait and check the image from docker image

# For Container
* open respective port of mariadb:3306, rabbitmq:5672, memcached:11211 and ntp:123 on your host
* use docker run -d --name=depends_on_you --net=host image_id
* for persistant storage you can use -v option
* after all steps you can use all services on host_ip:port with respective client

* use mysql_secure_installation 

add openstack user in rabbitmq-server (set any password you like for "password")
* rabbitmqctl add_user openstack password
* rabbitmqctl set_permissions openstack ".*" ".*" ".*"
