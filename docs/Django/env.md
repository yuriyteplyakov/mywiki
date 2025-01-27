### Создаем виртуальное окружение через терминал в нужной папке

> пайтон дает работать только на диске С и изменения разрешены только от имени администратора

`python -m venv practice_djangoEnv`

[Виртуальное окружение](https://pythonchik.ru/okruzhenie-i-pakety/virtualnoe-okruzhenie-python-venv)

> Чтобы начать пользоваться виртуальным окружением, необходимо его активировать

`cd C:\Users\пк\Desktop\honeymelon project\honeymelonEnv\Scripts`

`.\activate.ps1`

> Выход из окружения

`deactivate.ps1`

> Если - Set-ExecutionPolicy Unrestricted (нет доступа) то:<br>
> в powershell от имени админа<br>
> Set-ExecutionPolicy -Scope CurrentUser<br>
> Установил bypass<br>