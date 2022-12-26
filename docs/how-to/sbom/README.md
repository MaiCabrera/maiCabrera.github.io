# Security Workflow

## Creating an SBOM

- What is an SBOM

  - A `software bill of materials` is a list of all the open source and third-party components present in a codebase. A software BOM also lists the licenses that govern those components, the versions of the components used in the codebase, and their patch status.

### SBOM Steps for Binaries + Packages

Prerequisites:

- List of binaries to be used in project

---

Start

- Create a excel or word doc to track / list invetory of binaries to be used in the project

  - example binaries:
    - python3 *`<- our how-to-example we will use python`*
    - terraform
    - docker
    - ubuntu
    - k3s

- Columns A-H will host meta data information required for the manifest. Which in the first pass would be best to manually write this out / research it.

  - Component        = binary (ie. terraform, docker, ubuntu, k3s, etc)
  - Type of Software = options include: IaaS, VCS, OS, etc.
  - Supplier/ author = Entity whom is responsible for the component.
  - Category         = Is this component a binary, package, etc.
  - Version          = Components version semver.
  - License          = License to which this component is tied to.
  - Repository URL   = URL to where component's release can be found.
  - SHA256           = Authentication and encryption protocols, including SSL, TLS, IPsec, SSH, and PGP for the component.

### SBOM Steps for packages dependant on a binary (example python)

***Note: this process works with any virtual enviroment, tutorial uses python3 `venv` as the foundational process.***

Prerequisites:

- python3
- list of packages for python
- basic understanding on using `venv`

---

Start

- Create a virtual enviroment (using Python3)

    ```python3
    python3.6 -m venv /path/to/new/virtual/environment
    ```

- Turn enviroment on

   ```python3
   source enviroment/bin/activate
   ```
  
- Install packages for the virtual enviroment.
  - Running the previous command creates the target directory with a home key pointing to the Python installation from which the command was run (a common name for the target directory is .venv). It also creates a bin (or Scripts on Windows) subdirectory containing a copy/symlink of the Python binary/binaries (as appropriate for the platform or arguments used at environment creation time).

  ```python3
  pip3 install tensorflow
  pip3 install scikit-learn
  pip3 pandas
  pip3 spacey
  pip3 pydeps
  pip3 pip-licenses
  ```

- Run command to get output from `pip-licenses` and save it to a txt or file ending of your choice.

  ```python3
  pip-licences --format=csv --from mixed --with-system --with-description --with-url 
  
  OR

  pip-licences  --from mixed --with-system --with-description --with-url >> sbom.txt 
  ```

- SBOM completed.
