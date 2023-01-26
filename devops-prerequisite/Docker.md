## Docker ->

1. container images are in docker hub
2. install docker on the host system
3. `docker pull centos`
4. `docker run centos `
5. `docker ps`
6. `docker ps -a`
7. `docker run --name mohit centos`
8. `docker run -it --name shubham centos /bin/bash`
9. `ctr + c , ctr + p + q`
10. `docker exec -it shubham /bin/bash`
11. `docker images`
12. `docker stats`
13. `docker system df`
14. `-itd` -> d will daemonise the container, we will not get the terminal in return which we were getting with -it, but the container will keep on running
15. `systemd` -> manages system's services
16. `docker rm -f server1 server2` -> to delete containers
17. `docker start server1`
18. `docker inspect server1`
19. `ps -aux | grep sshd` -> to see if sshd service is running or not
20. `/usr/sbin/sshd -D &` -> to run the sshd service in background
21. `/usr/sbin/sshd -D fg` -> to run sshd service in foreground
22. `ps` -> to see currently running processes

<!-- dpass ->  33#nA4GU2cgr52M , name -> dexterlabhunter-->

<!-- 
yum install openssh-server openssh-clients
Add/change this line with this  ‘UsePAM yes’ in  /etc/ssh/sshd_config
ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key
ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key 
ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key 
run ‘/usr/sbin/sshd -D’ to start ssh service -->


## Dockerfile -> 

1. `docker commit` -> image from a container (not recommended) -> state save method
2. create docker image from `Dockerfile`. Create Dockerfile and mention the commands in it
3. then run the `docker run -it <other options>` command using that image to create the container, things we intall in docker container, mention those commands in `Dockerfile`
4. `docker build Dockerfile` -> to build an image from a file
5. `docker build -t angular /home/devops/angular/`

## Push image to dockerhub ->

 1. made changes to file, then created image from it with `docker build`
 2. push the image to dockerhub , create the repository with the same name as image local repository
 3. pull the image with `docker pull`
 4. run the image with `docker run`
 5. if we made changes to `Dockerfile`, then we can create an image with a new version, then when we `push` the image then in dockerhub there will not be two images, but inside the image there will be two types with different versions
 6. then `pull` the image with new version
 7. then `run` it and we cna also do port forwarding with `docker run -it -p 2222:22` 







