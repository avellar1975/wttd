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
<h1>Fazendo deploy em produção</h1>

<img src='https://www3.assets.heroku.com/assets/home/hero/focus-647c57d2effb7d2dfb5871161afab3cf097de6339c02e85d84ea14747800fcb0.png' width='200' align='right'>

* Criar uma conta no https://www.heroku.com
* Instalar o Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli
  * ```$ curl https://cli-assets.heroku.com/install-ubuntu.sh | sh```
* Verificar a instalação ```$ heroku --version```
* Fazer login no heroku via Heroku CLI ```$ heroku login```
* Será aberto um navegador para digitar usuário e senha

<h2>Instalação do python decouple</h2>

A biblioteca python-decouple vai ajudar gerenciar as configurações de ambientes.

```(.wttd) ➜  wttd git:(main) pip install python-decouple```

* Importar o módulo decouple no settings.py

```from decouple import config```

* Alterar as variáveis:

```
SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', default=False, cast=bool)
```

* Criar o arquivo .env na raiz do repositório (wttd)
* Inserir os valores de SECRET_KEY e DEBUG originais no arquivo .env, retirando os espaços antes e após o sinal de igual


<h2>Instalação do dj-database-url</h2>

```(.wttd) ➜  wttd git:(main) pip install dj-database-url```

* Importar o módulo decouple no settings.py

```from dj_database_url import parse as dburl```

* Alterar a configuração do settings.py

<pre>

default_dburl = 'sqlite:///' + str(BASE_DIR / 'db.sqlite3')

DATABASES = {
	'default': config('DATABASE_URL', default=default_dburl, cast=dburl),
}
</pre>

<h2>Outras configurações do settings.py</h2>
<pre>
ALLOWED_HOSTS = ['*']
...
STATIC_URL = 'static/'
STATIC_ROOT = str(BASE_DIR / 'staticfiles')
</pre>

* Instalar o dj-static
```
(.wttd) ➜  wttd git:(main) pip install dj-static
```

* Alterar o arquivo wsgi.py

<pre>
import os
from dj_static import Cling
from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'eventex.settings')

application = Cling(get_wsgi_application())
</pre>

<h2>Gerar o requirements.txt</h2>

```(.wttd) ➜  wttd git:(main) pip freeze > requirements.txt```

* Acrescentar dois módulos no requirements.txt
```
gunicorn==20.1.0
psycopg2-binary==2.9.3 
```
<h2>Criar o arquivo Procfile na raiz do repositório</h2>

* Ver o conteúdo no repositório

<h2>Envio para produção heroku</h2>
<pre>
(.wttd) ➜  wttd git:(main) heroku apps:create eventex-avellar
Creating ⬢ eventex-avellar... done
https://eventex-avellar.herokuapp.com/ | https://git.heroku.com/eventex-avellar.git
(.wttd) ➜  wttd git:(main) git remote -v
heroku  https://git.heroku.com/eventex-avellar.git (fetch)
heroku  https://git.heroku.com/eventex-avellar.git (push)
origin  git@github.com:avellar1975/wttd.git (fetch)
origin  git@github.com:avellar1975/wttd.git (push)
(.wttd) ➜  wttd git:(main) heroku open         
</pre>

<h2>Envio de variáveis de ambiente para o heroku</h2>
<pre>
(.wttd) ➜  wttd git:(main) cat .env            
SECRET_KEY='sua-chave-secreta'
DEBUG=True
(.wttd) ➜  wttd git:(main) heroku config:set SECRET_KEY='sua-chave-secreta'  
Setting SECRET_KEY and restarting ⬢ eventex-avellar... done, v3
SECRET_KEY: sua-chave-secreta
(.wttd) ➜  wttd git:(main)
(.wttd) ➜  wttd git:(main) heroku config:set DEBUG=True            
Setting DEBUG and restarting ⬢ eventex-avellar... done, v4
DEBUG: True
(.wttd) ➜  wttd git:(main)
</pre>

<h2>Hora do deploy</h2>
<pre>
(.wttd) ➜  wttd git:(main) git push heroku master --force 
</pre>
