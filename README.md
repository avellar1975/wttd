# Site desenvolvido com Django - estudo

## Criação do diretório do respositório do projeto
```
➜  ~ mkdir wttd
➜  ~ cd wttd
➜  wttd git:(main) 
```
## Criação e ativação de um ambiente virtual
```
➜  wttd git:(main) python -m venv .wttd
➜  wttd git:(main) source .wttd/bin/activate 
(.wttd) ➜  wttd git:(main)
```
> Se tiver feito o clone do projeto será necessário a instalação do requerements.txt
```
(.wttd) ➜  wttd git:(main) pip install -r requirements.txt  
```
## Criação do projeto django
```
(.wttd) ➜  wttd git:(main) django-admin startproject eventex .  
```
## Criaçao de um alias do manage.py

```
(.wttd) ➜  wttd git:(main) alias manage='python $VIRTUAL_ENV/../manage.py' 
```

## Execução do servidor
```
(.wttd) ➜  wttd git:(main) manage runserver 
```
## Dentro do projeto criamos a primeira app
```
(.wttd) ➜  wttd git:(main) cd eventex     
(.wttd) ➜  eventex git:(main) manage startapp core
```
 
## Configuração do arquivo settings com a app core
```
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'eventex.core',
]
```