Demo1 - Set up Jenkins single tire architecutre (In Docker Container)
    -> Launch EC2 Machine
    -> Install Docker ( Run docker-install.sh)
    -> Make sure 8080 port is opened in Jenkins master nachine
    -> spin up a jenkins Container with volume
    -> docker container run -d \ -p 8080:8080 \ -v jenkins:/var/jenkins_home \ --name jenkins-local \jenkinsjenkins:lts
    -> you shoul be able to access jenkins with port 8080
    -> Install suggested plugins
    -> Create a freestyle job with simple echo "hello world"
    -> Run the job and make sure it is successful


Demo2 - Set up Slave EC2 Machine and add slave worker node to Master
    -> Open port 22 in slave Machne
    -> Install Java in Slave/worker node
    -> sudo apt-get update && sudo apt-get install default-jre -y
    -> Managed nodes -> nodes -> create a node
    -> peovide private Ip of Worker node and keypair.pem as credentials
    -> Make sure worker node is up with 2 executers

Above approch is good but it is best if master decides when to scal up worker nodes and when to scale down
for that we need to do a automation 

Demo3 - Set up Automation to spin up worker EC2 machines as per load
    -> Install Amazon ec2 plugin
    -> Create an Iam role with EC2Fullaccess and attach it to Jenkins Master
    -> Create an AMI of Jenkins slave Machine as we will be specinfing for scaling same machine configuration
    -> Manage jenkins -> clouds -> Create a new cloud ( worker)
    -> Use EC2 instance profile to obtain credentials
    -> select region
    -> provide EC2 Key Pair's Private Key
    -> Test connection and make sure it is success
    -> AMI - Provide ami id that we have created
    -> Instance Type - T2Micro
    -> Security Group ID - of slave Machine
    -> Remote FS root -> /home/ubuntu
    -> Remote user -> ubuntu
    -> AMI Type -> unix
    -> Remote ssh port -> 22
    -> Lables -> worker
    -> Number of Executors - 2
    -> Subnet IDs for VPC - Slave machine subnet ID
    -> Minimum number of instances - 1
    -> Instance Cap -> 10 machines ( as per your estiamted scale requirment)
    -> Save
    -> As soon as you save an EC2 Worker machine spins up in aws
    -> As per the load machines scales up and down when there is no need

We may think like this is alot of setup, but remember this is one time setup and we have automated the setup :)


Demo-4 Role based access enablement and usage
    -> When user logs into jenkins with admin cred users can access entire jenkins jobs
    -> But in reeal world all users ahveing admin access is not possible and not secure
    -> Default Authorization in Jenkins is -> Logged in users can do anything
    -> Install a plugin "Role-based Authorization stratagy"
    -> Manage jenkins -> security -> "select Role-based stratagy"
    -> Login from admin user created jobs
    -> under manage roles -> created a new global role called developer with over all [view, buil view, cancle  build, view build] permissions
    -> then assign a user with developer role -> login and verify
    -> only he should see jobs
    -> Now if we re log in with admin and create item level role and assign [ with patter "dev.*"]
    -> developer now should only have build access for dev jobs

Demo-5 What if admin password is forgotten and needs to be reset
    -> config.xml is configuration file of jenkns is in docker volume so apth is [ /var/lib/docker/volumes/jenkins/_data]
    -> ture to false <useSecurity>false</useSecurity>
    -> Remove complete authourization stratagy class part
    -> Remove securityRealm class as well
    -> Leave <disableRememberMe> as it is
    -> Now stop the docker container and remove the container
    -> Run container agian docker container run -d \ -p 8080:8080 \ -v jenkins:/var/jenkins_home \ --name jenkins-local \ jenkins/jenkins:lts
    -> Now refresh Jenkins in browser "we will not have any login admin or any user" bcz we disabled user
    -> Now manage jenkins -> select Authentication as jenkins own user database 
    -> Now we can reset the admin password -> users -> admin -> settings -> security -> reset password
    -> Choose Authorization from any one can do anything to logged user can do anything
    -> 

    -> we desable security -> reset admin password -> then enable security again




