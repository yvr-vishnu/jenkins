Demo

Step - 1 ( Installation ) 
 Create 2 EC2 Machines
	1) Jenkins Master ( Install docker ) ( open 8080 port ) ( Run Jenkins container using below command )
	2) Jenkins Worker ( Install Docker & Java ) ( open 8080 port ) ( open 22 port internally meaning in sg ingress -> ssh 22 give same sg id and my ip as well )
	
	
 jenkins install command - > docker container run -d \ -p 8080:8080 \ -v jenkins:/var/jenkins_home \ --name jenkins-local \ jenkins/jenkins:lts
 
 
 Step - 2 ( Jenkins Architecture cofiguration )
 
 Access jenkinks -> Install Suggested Plugins ->  manage jenkins -> manage nodes -> Add worker nodes
 
 
 Step - 3 ( Creating a sample job )
 
 General 
 Source code management ( None GIT)
 Build Trigger
 Build Environment ( Delete workspace before build starts )
 Buid Steps ( Commands that we want to execute during the build ) ( echo "hello" )
 Post Build Actions ( Irrespective of build results if we want to run some commands we use this )
 
 General
	description  ( Woker )
	Discard old builds ( log rotation )
	GitHub Project (
	This project is parameterized  ( takes user input example BRANCH Selction -> choices ( dev,cert,qa,prod)
	Throttle builds  ( How many build can be executed in one hour or one day or one week )
	Excute concurent builds if neccessary ( If we want more than one build to run in parallel in same job we can mention number here )
	Restrict where this project can run  ( we can mention worker so always build run on worker not master )
	
 Source code management ( None GIT)
 
 Build Trigger 
	Trigger builds remotely: Trigger builds via HTTP requests.
	Build after other projects are built: Trigger this job after specific jobs are completed.
	Build periodically: Set a schedule for when the job should run.
	GitHub hook trigger for GITScm polling: Trigger builds when there are changes pushed to a GitHub repository.
	Poll SCM: Check the source code repository for changes at specified intervals.
	
Job should run successfully


Main Dis-advantage of free style job is ----> we dont know who,when,what changes are made to the job ( there is no version traking) 

That is why we want a best approch than this and the best approch is jenkinks file where we define everything in code

Jenkins file is two types
 1 Sciptive ( node {} ) ( old )
 2 declarative  ( pipeline {} )  ( new )
 
Functioanlity of both are same only syntax is differnt

STEP4 
	Wirte this file and practice running job
	jenkins-syntax-declerative-1

 