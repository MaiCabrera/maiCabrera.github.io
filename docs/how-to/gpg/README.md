# How to generate a PGP Key

## Prerequisites

- GPG command line tools - https://www.gnupg.org/download/
- Git (Windows only) - https://gitforwindows.org/

## Generating a new GPG key

- Open Terminal. On windows: Open Git Bash terminal.
- Generate a GPG key pair. Your GPG key must use RSA with a key size of 4096 bits.
  - If you are on version 2.1.17 or greater, paste the text below to generate a GPG key pair.  
  `$ gpg --full-generate-key`
  - If you are not on version 2.1.17 or greater, the gpg --full-generate-key command doesn't work. Paste the text below and skip to step 6.  
  `$ gpg --default-new-key-algo rsa4096 --gen-key`
- At the prompt, specify the kind of key you want, or press Enter to accept the default "RSA and RSA".
- Enter the desired key size. We recommend the maximum key size of "4096".
- Enter the length of time the key should be valid. Press Enter to specify the default selection, indicating that the key doesn't expire.
- Verify that your selections are correct.
- Enter your user ID information.
  - Full name
  - Email
  - Comments
- Type a secure passphrase.
- Done!


## Export public and secret GPG keys

- Use the "gpg --list-secret-keys --keyid-format LONG" command to list all GPG keys installed in the system.  
  `$ gpg --list-secret-keys --keyid-format LONG`
- From the list of GPG keys, copy the GPG key ID you'd like to use. In this example, the GPG key ID is 3AA5C34371567BD2:
  ``` bash
   $ gpg --list-secret-keys --keyid-format LONG
  /Users/hubot/.gnupg/secring.gpg
  ------------------------------------
  sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
  uid                          MyName (mycomment) <my@email.com>
  ssb   4096R/42B317FD4BA89E7A 2016-03-10
  ```
- Use this command to export the the public part of a key: 
  `$ gpg -a --export my@email.com > MyName-public-gpg.key`
- Use this command to export the the private part of a key:
  `$ gpg -a --export-secret-keys my@email.com > MyName-secret-gpg.key`
  - At the prompt type the key's passphrase.
- Copy the exported keys to a safe place.
- Done!


## Import public and secret GPG keys

- To import a public key use this command:  
  `$ gpg --import ~/MyName-public-gpg.key`
- To import a secret key use this command:  
  `$ gpg --allow-secret-key-import --import ~/MyName-secret-gpg.key`
  - At the prompt type the key's passphrase.
- Done!

> Since the keys are imported in to the system, remember to delete the original keys files from your home folder.  
> `$rm ~/MyName-secret-gpg.key ~/MyName-public-gpg.key`

### References

- [Generate New GPG](https://help.github.com/en/articles/generating-a-new-gpg-key)
- [Check for GPG](https://help.github.com/en/articles/checking-for-existing-gpg-keys)
