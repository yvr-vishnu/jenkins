Demo1- In jenkins source code management add github repo url and run build
    -> It is successful
    -> but in real world scenarios we use private githubs
    -> For that log in to machine where job runs in my case it is master, in your case it might be slave
    -> run ssh-keygen -> go to .ssh folder -> copy public key 
    -> Go to your github repo -> settings -> ssh & gpg key -> ssh key -> add new key -> add pub key there
    -> Now take any private repo from your github
    -> Add that to source code management in jenkins add git hub private url
    -> build it it should be success
    -> go to .ssh folder