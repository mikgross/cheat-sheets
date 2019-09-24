# create new ssh keys for github
List of commands to help create and configure a set of ssh keys on a github project.
Made on Ubuntu 18.04.3 LTS.

## generate the key
`ssh-keygen -t rsa -b 4096 -C "yourGitAccountEmailAddress"`

You will then be requested for a key name and a key passphrase for encryption.
It is important to remember the passphrase.

## add the key to trusted keys
`ssh-add ~/.ssh/nameOfKey`

## copy the public key
`xclip -sel clip < ~/.ssh/nameOfKey.pub`

## paste the public key in github
https://github.com/userName/projectName/settings/keys

(make sure to customize the url)

## configure access keys depending on projects
If you have multiple projects you would like to access through ssh, you need to configure multiple
ssh keys and as such point towards the right one when setting your project.

### in ~/.ssh/:
`vim config`

### type:
```
Host selectedHostName
        Hostname github.com
        User git
        IdentityFile `/.ssh/cheatSheets
```
### Save and exit

## push to git repo
got to your specific project folder on your machine and:

### initialize git
`git init`

### set remote
`git remote add origin git@selectedHostName:userName/projectName.git`

### stage and commit
`git push --set-upstream origin master`
`git stage *`
`git commit -m "first commit"`

### first push
`git push -u origin master`

## done!