> Если нужно поменять порт:
>> Заходим в папку *C:\Users\пк\Desktop\honeymelon project\honeymelonEnv\Lib\site-packages\django\core\management\commands\runserver.py*
>>>в файле runserver.py 8000 меняем например на 8002

Кодировка #-*- coding: utf-8 -*-

 https://is42-2018.susu.ru/tushinie/2020/12/01/internet-magazin-na-frejmvorke-django-chast-1/

 https://github.com/KAnanev/shop-django/blob/master/catalog/models.py

> ссылки выше: примеры для магазина!

1. Импорт библиотек

```py
import os
from pathlib import Path
from dotenv import load_dotenv
from django.contrib.messages import constants as messages
```

2. Установка и настройка [dotenv](https://pypi.org/project/python-dotenv)

```py
env_path = Path('.') / '.env'
load_dotenv(dotenv_path=env_path)
```

3. SECRET_KEY

- Комментируем стандартный ключ

`# SECRET_KEY = 'django-insecure-3^bz8@g!6b7+)j+uajb5^5vist22h48&(q1@-(s9qvcfr(3zoq'`

- Пишем

`SECRET_KEY = os.getenv('SECRET_KEY')`

- Создаем файл .env рядом с файлом manage.py

- внутри него вставляем тот же ключ:

`SECRET_KEY=django-insecure-3^bz8@g!6b7+)j+uajb5^5vist22h48&(q1@-(s9qvcfr(3zoq`

> позже в этом файле .env будут капчи и тд:

```py
DEBUG=True
EMAIL_USER=Honeym@mail.ru
EMAIL_PASS=honeymel1232dyn12
EMAIL_PORT=587
```

> Нужно разобраться с GOOGLE_RECAPTCHA_SECRET_KEY


4. Режим отладки

`DEBUG = True`
> Данный параметр на боевом сайте нужно обязательно установить в значение FALSE:



5. Разрешенные хосты

- Режим отладки:

`ALLOWED_HOSTS = ['*']`

- Боевой режим:

`ALLOWED_HOSTS = ['***.ru','www.***.ru', u'156.168.']`

6. Определение приложений

``` py linenums="1"
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.sites',
    'django.contrib.staticfiles',
    'django.contrib.humanize',

    # стандартные пакеты
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',
    'allauth.socialaccount.providers.github',


    'crispy_forms',
    'ckeditor',

    # Мои приложения
    # когда применяем сигналы, метки лучше указать полный путь
    # В общем случае можно использовать просто название приложения
    'blog.apps.BlogConfig',
    'shop.apps.ShopConfig',

    # должна быть последней
    'django_cleanup.apps.CleanupConfig',
]

```
7. id сайта

* в админке таблица Sites

`SITE_ID = 1`

8. MIDDLEWARE - система хуков для обработки запросов/ответов в Django

Это легкая, низкоуровневая система «плагинов» для глобального изменения входных или выходных данных Django.\
Каждый компонент промежуточного ПО отвечает за выполнение определенной функции.\ Например, Django включает компонент промежуточного ПО, AuthenticationMiddleware, который связывает пользователей с запросами с помощью сессий.

```py
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

`ROOT_URLCONF = 'practice_honey.urls'`

9. Шаблоны

```py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates'),
                 ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

10. Аутентификация пользователей [django-allauth](https://django-allauth.readthedocs.io/en/latest/)

```py
# django-allauth
AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
]

SOCIAL_PROVIDERS = {
    'google': {
        'SCOPE': [
            'profile',
            'email',
        ],
        'AUTH_PARAMS': {
            'access_type': 'online',
        }
    },
    'github': {
        'SCOPE': [
            'user',
            'repo',
            'read:org',
        ],
    }
}

# END django-allauth
```

`WSGI_APPLICATION = 'practice_honey.wsgi.application'`

11. База данных: [Database](https://docs.djangoproject.com/en/4.2/ref/settings/#databases)

```py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db_practice_honey_1.sqlite3',
    }
}
```
> sqlite лучше использовать только при разработке
> На боевом сайте предпочтительней использовать postgresql (Посмотреть как подключить)

12. [Password validation](https://docs.djangoproject.com/en/4.2/ref/settings/#auth-password-validators)

```py
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
```

13. [Internationalization](https://docs.djangoproject.com/en/4.2/topics/i18n/)

```py
LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True
```

14. [Static files (CSS, JavaScript, Images)](https://docs.djangoproject.com/en/4.2/howto/static-files/)

[static-root](https://docs.djangoproject.com/en/4.2/ref/settings/#static-root)

```py
STATIC_URL = 'static/'

STATIC_ROOT = os.path.join(BASE_DIR, 'static')

# Default primary key field type
# https://docs.djangoproject.com/en/4.2/ref/settings/#default-auto-field

STATICFILES_DIRS = [
    
]

STATICFILES_FINDERS = [
    "django.contrib.staticfiles.finders.FileSystemFinder",
    "django.contrib.staticfiles.finders.AppDirectoriesFinder",
]
```

15. MEDIA

```py
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

MEDIA_URL = '/media/'
```

`DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'1`

16. django-crispy-forms

`CRISPY_TEMPLATE_PACK = 'uni_form'`

17. ckeditor

> позволяет писать контент непосредственно внутри веб-страниц или онлайн-приложений

```py
CKEDITOR_CONFIGS = {
    'default': {
        'width':'auto',
    },
}
```

18. django-channels

```py
#django-channels
ASGI_APPLICATION = "honeymelon_handmade_jewerly.routing.application"

CHANNEL_LAYERS = {
    "default": {
        "BACKEND": "channels.layers.InMemoryChannelLayer",
    },
}
# End django-channels
```


19. Email

```py
# Email
EMAIL_BACKEND = 'django.core.email.backends.smpt.EmailBackend'
EMAIL_HOST = 'smpt.gmail.com'
EMAIL_PORT = os.getenv("EMAIL_PORT")
EMAIL_USE_TLS = True
EMAIL_HOST_USER =os.getenv('EMAIL_USER')
EMAIL_HOST_PASSWORD = os.getenv('EMAIL_PASS')
# End email
```

`GOOGLE_RECAPTCHA_SECRET_KEY = os.getenv("GOOGLE_RECAPTCHA_SECRET_KEY")`

```py
MESSAGE_TAGS = {
    messages.DEBUG: 'alert-secondary',
    messages.INFO: 'alert-info',
    messages.SUCCESS: 'alert-succesS',
    messages.WARNING: 'alert-warning',
    messages.ERROR: 'alert-danger',
}
```

> В ПРОИЗВОДСТВЕ УБРАТЬ!
> команду ниже можно сделать алиасом
> Запускает юпитер
> alias jshell = 'python manage.py shell_plus --notebook'
> os.environ["DJANGO_ALLOW_ASYNC_UNSAFE"] = "true"