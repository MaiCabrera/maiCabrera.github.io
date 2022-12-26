# Docsify - Markdown & GitHub

## Objective

### How to setup docsify with WSL2

Todo list:

- [ ] install `docsify-cli`

  - Enable npm to be able to install nodejs

    ```npm
    curl -fsSL https://deb.nodesource.com/setup_12.x | sudo -E bash - sudo apt-get install -y nodejs
    ```

  - run npm command to install `docsify-cli`

    ```npm
    sudo npm i docsify-cli -g
    ```

  - fix any npm vulnerabilty and then a second time to verify all are fixed

    ```npm
    sudo npm audit fix --force
    ```

- [ ] optional if using `nvm` [ref link to npm recomendation fix](https://askubuntu.com/questions/1382565/npm-does-not-support-node-js-v10-19-0/1382566#1382566)

    ```npm
    nvm use 8
    nvm uninstall 10
    nvm uninstall  12
    nvm install 10
    nvm install 12
    nvm use 10
    nvm alias default 10   
    nvm uninstall 8
    ```

- [ ] Start your project
  
  - Run the following command to init your `docisfy-cli` templates

    ```npm
    docsify init ./docs
    ```

  - Run the following command to **preview** your `static site`

    ```npm
    docsify serve docs 
    
    or 
    
    docsify serve
    ```