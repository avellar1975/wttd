<img src='https://bmcoder.com/images/python_django_development.png' width='150' align='right'>
<h1>Site desenvolvido com Django - estudo</h1>
<br/>
<br/>

<h2>Qual versão do Python eu posso usar com Django?</h2>
<table>
<colgroup>
<col width="19%">
<col width="81%">
</colgroup>
<thead valign="bottom">
<tr class="row-odd"><th class="head">Versão do Django</th>
<th class="head">Versões do Python</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even"><td>2.2</td>
<td>3.5, 3.6, 3.7, 3.8 (adicionado em 2.2.8), 3.9 (adicionado em 2.2.17)</td>
</tr>
<tr class="row-odd"><td>3.0</td>
<td>3.6, 3.7, 3.8, 3.9 (adicionado em 3.0.11)</td>
</tr>
<tr class="row-even"><td>3.1</td>
<td>3.6, 3.7, 3.8, 3.9 (adicionado em 3.1.3)</td>
</tr>
<tr class="row-odd"><td>3.2</td>
<td>3.6, 3.7, 3.8, 3.9, 3.10 (adicionado em 3.2.9)</td>
</tr>
<tr class="row-even"><td>4.0</td>
<td>3.8, 3.9, 3.10</td>
</tr>
</tbody>
</table>

## Criação do diretório do repositório do projeto
```
➜  ~ mkdir wttd
➜  ~ cd wttd
➜  wttd git:(main) 
```
O diretório wttd/ é um contêiner para o seu projeto. Seu nome não importa para o Django; você pode renomeá-lo para qualquer nome que você quiser.

## Criação e ativação de um ambiente virtual
<img src='https://miro.medium.com/max/750/1*Z14kLUEB69SsYdNORxQzlw.jpeg' width='200' align='right'>

```
➜  wttd git:(main) python -m venv .wttd
➜  wttd git:(main) source .wttd/bin/activate 
(.wttd) ➜  wttd git:(main)
```
> Se tiver feito o clone do projeto será necessário a instalação do requirements.txt
```
(.wttd) ➜  wttd git:(main) pip install -r requirements.txt  
```
> Ou instalar o django
```
(.wttd) ➜  wttd git:(main) pip install django
(.wttd) ➜  wttd git:(main) python -m django --version
```

## Criação do projeto django eventex
```
(.wttd) ➜  wttd git:(main) django-admin startproject eventex .  


wttd/
    manage.py
    eventex/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py

```
O diretório eventex/ é o pacote Python para o projeto. Seu nome é o nome do pacote Python que você vai precisar usar para importar coisas do seu interior (por exemplo, eventex.urls).

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

core/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
Cada aplicação que você escreve no Django consiste de um pacote Python que segue uma certa convenção. O Django vem com um utilitário que gera automaticamente a estrutura básica de diretório de uma aplicação, então você pode se concentrar apenas em escrever código em vez de ficar criando diretórios.
 
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
<img src='https://www3.assets.heroku.com/assets/home/hero/focus-647c57d2effb7d2dfb5871161afab3cf097de6339c02e85d84ea14747800fcb0.png' width='200' align='right'>

* Criar uma conta no https://www.heroku.com
* Instalar o Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli
  * ```$ curl https://cli-assets.heroku.com/install-ubuntu.sh | sh```
* Verificar a instalação ```$ heroku --version```
* Fazer login no heroku via Heroku CLI ```$ heroku login```
* Será aberto um navegador para digitar usuário e senha

