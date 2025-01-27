# Установка зависимостей

* обновляем pip:

`pip install --upgrade pip`

* Последняя стабильнaя версия библиотек (без указания версии):

`pip install django`

> Если захотим установить определенную версию то:
> цифра 2 ниже означает LTS-версию, боевые проекты лучше делать на них.

`pip install --upgrade django==3.2.10`

* проверка установленных пакетов

`pip freeze`

* Библиотека для красивых форм ввода:

[django-crispy-forms](https://django-crispy-forms.readthedocs.io/en/latest/install.html#installing-django-crispy-forms)

`pip install django-crispy-forms`

[django-cleanup](https://github.com/unit/django-cleanup)

`pip install django-cleanup==5.2.0`

[pillow](https://github.com/codingforentrepreneurs/Guides/blob/master/all/imagefield_and_pillow.md)

`pip install pillow`

[django-ckeditor](https://pypi.org/project/django-ckeditor/)

`pip install django-ckeditor`

[channels](https://channels.readthedocs.io/en/stable/installation.html)

`python -m pip install -U channels`

[django-allauth](https://django-allauth.readthedocs.io/en/latest/)

`pip install django-allauth`

* Установка и настройка [dotenv](https://pypi.org/project/python-dotenv)

`pip install python-dotenv`

```python

from pathlib import Path
import os
from dotenv import load_dotenv
from django.contrib.messages import contants as messages

# Loading ENV
env_path = Path('_') / '.env'

# env_path = '.test.env'
load_dotenv(dotenv_path=env_path)
```
[django-braces](https://django-braces.readthedocs.io/en/latest/)

`pip install django-braces`

### Все о документации

[mkdocs](https://www.mkdocs.org/)

`pip install mkdocs`

* панель инструментов на сайте админки

[django-debug-toolbar](https://django-debug-toolbar.readthedocs.io/en/latest/installation.html)

`python -m pip install django-debug-toolbar`

[Jupiter notebook](https://jupyter.org/)

`pip install notebook`

### Cписок установленных пакетов

`python -m pip list notebook`

* только пакеты ноутбука

`python -m pip show notebook`

[django-extensions](https://django-extensions.readthedocs.io/en/latest/)

`pip install django-extensions`

* команду ниже можно сделать алиасом, она запускает юпитер

`python manage.py shell_plus --notebook`

`alias jshell = 'python manage.py shell_plus --notebook'`

* Темы для юпитера

[jupyterthemes](https://github.com/dunovank/jupyter-themes)

`pip install jupyterthemes`

* nbextensions

`pip install jupyter_contrib_nbextensions`

* Подключаем настройки для юзера

`jupyter contrib nbextensions install --user`

`jupyter nbextensions_configurator enable --user`

* Конфигуратор

`pip install jupyter_nbextensions_configurator`

* Если  на странице не появилось (HinterLand) или она неполная, выполняем в командной строке:

`jupyter contrib nbextensions install --user --skip-running-check`

* [django-taggit](https://django-taggit.readthedocs.io/en/latest/getting_started.html)

`pip install django-taggit`