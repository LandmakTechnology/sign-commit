## How to configure Signing git commits:

**1. Using GPG keys:**
- You can find instructions on how to use GPG keys on the link below.

    [Using GPG Keys](https://daily-dev-tips.com/posts/how-to-verify-your-commits-on-github/)

**a) Install GPG:**

    $ brew install gpg    
    
[for windows](https://www:ibiblio:org/shadow/pgp/install-gpg.pdf)  

**b) Generate a new GPG key:**

    $ gpg --full-generate-key

- Keep in mind the following settings:
    - Choose an RSA key (Option 1)
    - Key should be a MINIMUM of 4096 in size
    - I set it never to expire (Option 0)
    - Name and email. Use your GitHub email else, it won't work!
    - After this, it will prompt a password field twice. Use a secure password for this.
  
**c) Verify the GPG key:**

    $ gpg --list-secret-keys --keyid-format LONG

**d) Export the key to gitHub:**

    $ gpg --armor --export [THIS_KEY_ID]

- This will generate a large block of code. copy the whole section, including the comments and paste it in Github.
- In GitHub, click on your profile image -> Settings. Choose SSH and GPG Keys from the left menu,
  scroll down and add a new GPG Key.

**e) Configure git to always sign commits using the key:**

    $ git config --global user.signingkey [THIS_KEY_ID]
    $ git config --global commit.gpgsign true

**f) Creating a custom commit message:**

- i) Edit the .gitconfig file to point git to the template we are creating:

       $ git config --global commit.template ~/.gitmessage
    
 - Alternatively, you can VI into .gitconfig file and add the contents below.

         [commit]
         template = ~/.gitmessage

- ii) Create a template in ~/.gitmessage file:
```
########50 characters############################
Scope / Description with fix, feat (SemVer)
Contributing-to: https://kennedymakhanu1.atlassian.net/browse/<JIRA-TICKET>
########72 characters##################################################
Problem
# Problem, Task, Reason for Commit
Solution
# Solution or List of Changes
Note
# Special instructions, testing steps, rake, etc
```

- c) Now when you commit any updates, only type git commit and the editor will pop up for you to provide the context:

       $ git commit

**2. Using SSH keys:**
- You can find instructions on how to use ssh keys from the link below.

   [Using SSH Keys](https://dev.to/pwd9000/github-commit-verification-using-ssh-2pim)