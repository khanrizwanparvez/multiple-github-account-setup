# multiple-github-account-setup
To use two different GitHub accounts on the same computer.

# 1. Generate SSH Keys for Each Github Account

**For Account 1 (First account)**

1. Open the terminal and generate a new SSH key for the first GitHub account
```
ssh-keygen -t rsa -b 4096 -C "your_first_email@example.com"
```

2. When prompted to specify a file to save the key, name it something unique, like id_rsa_firstAccount
**Enter file in which to save the key:**
```
/home/your_username/.ssh/id_rsa_firstAccount
```

3. Start the SSH agent in the background
```
eval "$(ssh-agent -s)"
```

4. Add the private key to the SSH agent
```
ssh-add ~/.ssh/id_rsa_firstAccount
```

5. Copy the SSH public key to your clipboard
```
cat ~/.ssh/id_rsa_firstAccount.pub
```

* Copy the output, then go to GitHub > Settings > SSH and GPG keys and add this as a new SSH key for your first account.


# 2. Repeat the above steps for your second account, generating a separate key
```
ssh-keygen -t rsa -b 4096 -C "your_second_email@example.com"

# Save it as: /home/your_username/.ssh/id_rsa_secondAccount

eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_rsa_secondAccount

cat ~/.ssh/id_rsa_secondAccount.pub
```

*Add this second SSH key to GitHub for your second account.


# 3. Configure the SSH Config File
1. Open or create the ~/.ssh/config file in a text editor
```
nano ~/.ssh/config
```

2. Add the following lines to the file to define separate SSH configurations for both accounts
```
# First GitHub account
Host github.com-firstAccount
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_firstAccount

# Second GitHub account
Host github.com-secondAccount
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_secondAccount
```

3. Save the file and Exit


# 4. Cloning Repositories with the Correct SSH Host
* For first GitHub repositories
```
git clone git@github.com-firstAccount:username/repo.git
```

* For second GitHub repositories
```
git clone git@github.com-secondAccount:username/repo.git
```

# 5. Set Git Config for Each Repository
```
git config user.name "Name"
git config user.email "your_email@example.com"
```