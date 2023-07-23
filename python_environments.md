# Python Environments
- [conda](#conda)
- [virtualenv](#virtualenv)

# conda
Create different environments which hold different packages. The "base" environment has everything

- To create an environment, in terminal:
```
conda create --name env_name
```
set python version
```
conda install python=3.5.0
```

- To enter environment
```
conda activate env_name
```

- To see list of environment names
```
conda env list
```

- To see list of packages in current environment
```
conda list
```

- To install package in current environment
```
conda install pandas
```

# virtualenv
- running pip installs executables into the virutal environment 
- install
```
pip install virtualenv
```
- create virtual environment stored in venv folder for current project
```
virtualenv venv
```
- activate virtual environment stored in venv folder
```
source venv/bin/activate
```
- deactivate virtual environment
```
deactivate
```