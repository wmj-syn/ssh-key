# ssh-key
Setting up ssh keys for different accounts in gitlab


## Generate ssh key pairs
Generate two ssh key pairs, one for the student account and the other for the staff account

```
ssh-keygen -o -t rsa -b 4096 -C "email@example.com"
```
The two ssh key pairs can be stored in ~/.ssh/gitlab_staff and ~/.ssh/gitlab_student

## Add the key to the Gitlab server

Copy the corresponding public ssh key to the corresonping Gitlab account. (Avatar-Settigns-ssh keys)

## Setup the config file

To identify which ssh key is related to the which account, setup the config file as follows:

```
Host gitlab_staff
    HostName gitlab.mech.kuleuven.be
    User git
    IdentityFile ~/.ssh/gitlab_staff/id_rsa

Host gitlab_student
    HostName gitlab.mech.kuleuven.be
    User git
    IdentityFile ~/.ssh/gitlab_student/id_rsa
```

The Host can be self-determined.

## Some ssh commands
Start the ssh agent
```
eval $(ssh-agent -s)
```

Connect to the host
```
ssh -T git@Host (gitlab_staff, gitlab_student)
```

## A better way to simplify the procedure
Using the method above needs to tell ssh explicitly which account to use (to specify the location of the key) everytime using the ssh. Another way could be creating a symbolic link to the gitlab_staff account by default, and change the link when necessary.

```
cd ~/.ssh
ln -s gitlab_staff/id_rsa
```



