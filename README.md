# how to configure multiple github or version control accounts, access the content without password

# generate ssh public and private key, to follow the command prompt
# -t ed25519: This specifies the type of key to create
# -C "label": The -C option is used to add a comment to the key,label for the SSH key, ii will appedn end of pub key content

ssh-keygen -t ed25519 -C "label"

# once excute the above command prompt will ask file name
# then 2 file will be create, one end with .pub extension and two without any extension
# it is used to start the SSH agent and set up the environment variables necessary for the SSH agent to function within your current shell session

eval "$(ssh-agent -s)"


# add private keys to the SSH agent, allowing the SSH agent to use those keys for authentication when connecting to SSH servers
ssh-add private_key_file_name


# ensure keys are added
ssh-add -l


# create file name as 'config' without any extension
# example ssh configuration file
# github

# Account1
User git
Host github.com-personal
HostName github.com
IdentityFile ~/.ssh/private_key_file(available wihtout any extension)

# Account2
User git
Host github.com-work
HostName github.com
IdentityFile ~/.ssh/private_key_file(available wihtout any extension)


# gitlab
# Account3
User git
Host gitlab.com-personal
Hostname gitlab.com
IdentityFile ~/.ssh/private_key_file(available wihtout any extension)

# add public key to version control hosting environment
# open public key copy past the related version control tool (gitlab.com or github.com)
# if github go to github setting > select ssh and gpc key page > add new ssh key, past you public key 
# if gitlab go to github profile > ssh keys > add new ssh key, past you public key


# ensure ssh connection
ssh -T Host
# the Host is name of config file Host value, example
ssh -T github.com-personal

# how to clone repo with ssh connection

git clone git@github.com:xxx/xxx.git

# This part specifies the Git username (git) and the host (github.com). In this context, it signifies the user (git) that is accessing the github server.
# xxx/xxx.git: This part specifies the path to the repository. The first set before the slash (/) represents the namespace or user/group where the repository resides. xxx.git is the name of the repository itself.
# modify the url like below we connect our git account as we config the file above

git clone git@github.com-personal:xxx/xxx.git

# the above modified url will clone the account1 related repo, with asking password
