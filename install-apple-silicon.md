# Installing Odoo on Apple Silicon

The following is a guide on how to install Odoo and manage different versions on Apple Silicon Macs. 

> This was last tested on M1 Pro and M2 running under macOS Ventura. It is possible future versions of macOS discontinue support for Rosetta 2.

[Video Tutorial Here](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

## Pre-requirements
The following requirements are necessary

### Miniconda
Mini conda is advised to help in creating and managing multiple virtual environments with different versions and compilations of Python (Both native Apple Silicon and Intel through Rosetta 2).

Install with Homebrew:
```bash
brew install --cask miniconda
``` 

### Postgres
Odoo uses PostgreSQL as database management system. Use [postgres.app](https://postgresapp.com/) to download and install PostgreSQL (supported version: 12.0 and later).

### Rosetta 2
Rosetta 2 is a translation layer that enables Macs with Apple Silicon to use apps built for Mac with an Intel processor. If you have previously attempted to use an app compiled for x86_64 (Intel), Rosetta was automatically installed. Otherwise, it can be installed from the terminal:
```bash
softwareupdate --install-rosetta
```

## Getting source
Firstly get the source from git.
```bash
git clone https://github.com/odoo/odoo.git
```

### Switching versions
In Odoo, each version corresponds to its own branch. Hence, you can change versions by changing the branches:
```bash
git checkout <odoo-version>
```

## Creating environment
It is **highly** recommended to create a different virtual environment for each Odoo version to avoid collisions and other issues in the future. 

Consider the following table:

| Odoo Version | Python Version | Architecture |
| ------------ | -------------- | ------------ |
| Odoo 16.0    | Python 3.10    | arm64        |
| Odoo 15.0    | Python 3.8     | x86_64       |
| Odoo 14.0    | Python 3.8     | x86_64       |
| Odoo 13.0    | Python 3.6     | x86_64       |


### Create environment
To create an environment run:
```bash
conda create -n <name-of-environment>
```
> It is adived to name the environment according to the corresponding Odoo version

Activate the environment:
```bash
conda activate <name-of-environment>
```

### Configure environment
Next, the environment must be configured to run either in native arm64 architecture or in x86_64.

To configure it for x86_64, run
```bash
conda config --env --set subdir osx-64
```
To configure it for native arm64, do nothing. 

To install the corresponding python version, run:
```bash
conda install python=<python-version>
```

### Install requirements
Next, install all the necessary requirements from the `requirements.txt` file.
```bash
pip install -r requirements.txt
```

> If you get the error: `ImportError: dlopen(/Users/edvilme/miniconda3/envs/conda-odoo-14/lib/python3.8/site-packages/psycopg2/_psycopg.cpython-38-darwin.so, 0x0002): symbol not found in flat namespace '_PQbackendPID'`, try reinstalling `psycopg2` with `pip uninstall psycopg2 & pip install psycopg2-binary`

## Running
Once the environments are configured, you can run the odoo version by swithcing to the corresponding branch and activating the respective environment
```bash
git checkout <odoo-branch-name> & conda activate <odoo-env-name>
```

Also make sure that the postgres server is active and running.

Lastly run Odoo using the command:
```bash
(odoo-env-name)$ python odoo-bin -d <name-of-database> -r <username> --limit-memory-hard 0
```
