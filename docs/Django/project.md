> После установки всех нужных пакетов

1. Создаем проект с названием, например: 'honeymelon_django'

`django-admin startproject honeymelon_django`

> для дальнейшей работы нужно зайти в только-что созданный проект:

`cd honeymelon_django`

2. работа с файлом натроек

> смотри вкладку settings

3. Создадим первое приложение для блога:

`python manage.py startapp honeymelon_blog`

4. Добавляем наше приложение в файл settings.py

```py
INSTALLED_APPS = [
    # Мои приложения
    # когда применяем сигналы, метки лучше указать полный путь
    # В общем случае можно использовать просто название приложения
    'honeymelon_shop.apps.HoneymelonShopConfig',
]
```

5. в папке приложения в файле models.py создаем модели для будущей базы данных

> смотри вкладку models

6. Проведем миграции

`python manage.py makemigrations`

`python manage.py migrate`

7. Создадим суперпользователя для сайта администрирования

`python manage.py createsuperuser`

7. Создадим файл urls.py в нашем приложении

> В этом файле будут храниться пути которые прописываются в поисковой строке (детали приложения)

```py
# импорты
from django.urls import path, re_path
from blog.views import UserPostListView, PostCreateView, PostDetailView

urlpatterns = [
    path('posts/user/<str:username>/', UserPostListView.as_view(), name='user-posts-list'),
    # В поисковой строке будет выглядеть так:
    # http://127.0.0.1:8000/posts/user/Honeym/ (где Honeym никнейм пользователя)

    # создание поста (Если потребуется, то нужно добавить шаблон blog/post_form.html)
    path('post/new/', PostCreateView.as_view(), name='post-create'),
    path('post/<int:pk>/detail/', PostDetailView.as_view(), name='post-detail')
]
```