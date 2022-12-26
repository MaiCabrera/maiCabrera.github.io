# [Cosign](https://github.com/sigstore/cosign)

## Concepts

> Cosign is a simple container siginig tool. Its purpose is to sign and
> verify container images by using a signature `algorithm (ECDSA-P256)`.
>>Cosign supports several types of signing keys:
>>
>> - text-based keys
>> - cloud KMS-based keys or even keys generated on hardware tokens
>> - kubernetes-secrets which can all be generated directly with the tool itself
>> - supports adding key-value annotations to the signature.

### Methods of Installation

- [ ] Installation using `Golang`
  
  - If `golang` is installed run the following command block below:

    ```golang
    git clone https://github.com/sigstore/cosign
    cd cosign
    go install ./cmd/cosign
    (go env GOPATH)/bin/cosign
    ```

  - Installation for OS systems

    ```bash
    # binary
    wget "https://github.com/sigstore/cosign/releases/download/v1.6.0/cosign-linux-amd64"
    mv cosign-linux-amd64 /usr/local/bin/cosign
    chmod +x /usr/local/bin/cosign

    # dkpg
    wget "https://github.com/sigstore/cosign/releases/download/v1.6.0/cosign_1.6.0_amd64.deb"
    dpkg -i "cosign_1.6.0_amd64.deb
    ```

  - Homebrew

    ```bash
    # homebrew/linuxbrew
    brew install cosign
    ```

- [ ] Installation `GitHub Action`
  
  - GitHub Actions require you place this piece of code below:

  - link to [`official gitaction`](https://github.com/marketplace/actions/cosign-installer)

    ```yaml
    uses: sigstore/cosign-installer@main
    with:
    cosign-release: 'v1.2.1' # optional
    ```

- [ ] GitHub Commit Signature
  
  - Review the prework in this link for `GitHub` signature commit
  - Open a `linux/wsl` terminal and run
  
    ```bash
    gpg --full-generate-key
    ```

  - Accept `default`, choose `4096`, verify all else data fields
  - Choose passphrase
  - Copy the long form of the GPG key ID you'd like to use (see GitHub doc link above)

    ```bash
    gpg --list-secret-keys --keyid-format=long
    ```

  - Paste & substitute in the GPG key ID you'd like to use.

    ```bash
    gpg --armor --export 3AA5C34371567BD2
    ```

  - GPG key, beginning with
    - `-----BEGIN PGP PUBLIC KEY BLOCK----- and ending with -----END PGP PUBLIC KEY BLOCK-----`
    - [Save GPG key into your GitHub Account](https://docs.github.com/en/articles/adding-a-new-gpg-key-to-your-github-account)

---

### Solutions

1. Signing `git commits` for GitHub

   - Below are the series of flags & commands git needs to sign a commit
   - Ensure the `-S` is capitalized

    ```bash
    git commit `-S` -m "enter your commit text"
    ```

1. Troubleshooting

   - if you experience an issue where you get error: gpg failed to sign the data

    ```bash
    git config --global gpg.program gpg2 # to edit config
    echo "test" | gpg2 --clearsign       # test gpg is working
    export GPG_TTY=$(tty)    # env var to ensure commit calls or add to ~/.bashrc
    gpgconf --kill gpg-agent # kill gpg agent to restart
    ```
