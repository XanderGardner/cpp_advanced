# Table of Contents
- [Back to Main](README.md)

[conda](#conda)

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