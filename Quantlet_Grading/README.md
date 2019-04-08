[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **Quantlet_Grading** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of QuantLet : Quantlet_Grading

Published in : ''

Description : 'Grading of all Quantlets within one GitHub repository with the use of the classes modules/QUANTLET.py and modules/METAFILE.py.'

Keywords : Quantlet, Quantlet grading, text analysis, text evaluation, yaml debugging

See also : ''

Author : Marius Sterling

Submitted : April 8 2018 by Marius Sterling

```

### PYTHON Code
```python

# -*- coding: utf-8 -*-
"""
Created on Mon Oct 15 11:02:37 2018
"""
import os, importlib
# Change working directory to the repository path
os.chdir('/home/ms/github/Quantlet_Evaluation')

# Install packages if necessary
packages_to_be_installed_list = ['numpy','pandas','nltk','jsonpickle','json','sklearn','gensim','tqdm','matplotlib']
packages_to_be_installed_dict = {'github':'PyGithub', 'yaml':'PyYAML'}
missing_packages = []
for i in packages_to_be_installed_list:
    try:
        importlib.import_module(i)
    except ModuleNotFoundError:
        missing_packages.append(i)
for k,v in packages_to_be_installed_dict.items():
    try:
        importlib.import_module(k)
    except ModuleNotFoundError:
        missing_packages.append(v)
assert not missing_packages, 'The following packages are missing. Please install them: %s'%(', '.join(missing_packages))

# Loading QUANTLET class
from modules.QUANTLET import QUANTLET

# Add github token, if you try to acces a private repository or there are a lot of files to be checked
github_token = None
# set the user name 
USER = 'quantlet'
# set name of repository
repo = 'VIX'

# Quantlets are downloaded
q = QUANTLET(github_token=github_token, user=USER)
q.download_metafiles_from_user([repo])

# Quantlets are graded.
q.grading().to_csv(os.path.join('Quantlet_Grading','grades_%s_%s.csv'%(USER,repo)))

```

automatically created on 2019-04-08