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
## Criação do projeto django eventex
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
 
## Configuração do arquivo settings.py com a app core
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
## Atualização das rotas no arquivo urls.py

```
from django.contrib import admin
from django.urls import path
import eventex.core.views

urlpatterns = [
    path('', eventex.core.views.home),
    path('admin/', admin.site.urls),
]
```

## Criação da função home no arquivo core/views.py

```
from django.shortcuts import render

def home(request):
    return render(request, 'index.html')
```

## Criar os diretórios templates/ e static/ dentro de core/

* As pastas de css, fonts, js e img ficam dentro de static/
* O html fica na pasta templates/

## Template tag {% load static %}

* No início do arquivo htlm inserir o template tag do django
* Substituir os caminhos dos arquivos estáticos
```
<script src = "{% static 'js/main.js' %}"></script>
```
## Fazendo deploy em produção
* Criar uma conta no https://www.heroku.com
* Instalar o Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli
  * ```$ curl https://cli-assets.heroku.com/install-ubuntu.sh | sh```
* Verificar a instalação ```$ heroku --version```
* Fazer login no heroku via Heroku CLI ```$ heroku login```

