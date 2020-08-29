# Connecting to GitHub with SSH

## Checking for existing SSH keys

Before you generate an SSH key, check for any existing SSH keys.

```
$ ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

## Generating new key

If you don't have an existing public and private key pair, then generate a new SSH key.

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This creates a new ssh key, using the provided email as a label.
When you're prompted to "Enter a file in which to save the key," press Enter. 
This accepts the default file location.

## Adding new key to ssh-agent

Start the ssh-agent in the background.

```
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

Add your SSH private key to the ssh-agent.

```
$ ssh-add ~/.ssh/id_rsa
```

[Add a new SSH key to your GitHub account](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account).



