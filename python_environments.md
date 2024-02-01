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
- create a directory for virtual environments if not already made
```
mkdir ~/.virtualenvs
```
- create a new virtual environment
- `-m venv` refers to executing venv which comes with which every python is downloaded (in this case 3.11)
```
python3.11 -m venv ~/.virtualenvs/environment_name
```
- activate virtual environment
```
source ~/.virtualenvs/environment_name/bin/activate
```
- almost always you will want pip in your environment
```
python -m pip install --upgrade pip
```
- you can install other tools in this venv using pip
```
python -m pip install coverage
python -m pip install pylint
python -m pip install PyQt5
python -m pip install flask
python -m pip install selenium
```
- to deactivate your environment
```
deactivate
```

