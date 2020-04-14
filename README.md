# linux_gui_remote_access_instructions
Инструкция по удаленному доступу к Linux GUI (Debian)

### В самом начале

* Как настроить подключение по SSH: https://androidp1.ru/kak-polzovatsja-ssh-a-takzhe-ustanovka-i-nastrojka/

### Шаг первый. Установка GUI

```
$ apt-get update
$ apt-get install --no-install-recommends xserver-xorg xserver-xorg-core xfonts-base xinit libgl1-mesa-dri x11-xserver-utils
```

### Шаг второй. Установим Xfce

Стандартная установка:
```
$ apt-get update
$ apt-get install xfce4 xfce4-terminal
```
Полная установка:

```
$ apt-get update
$ apt-get install task-xfce-desktop
```

### Шаг третий. Настраиваем удаленный доступ

```
$ apt-get install xrdp
$ systemctl enable xrdp
$ systemctl start xrdp
```

### Шаг четвертый. Запускаем RDP-клиент

Для Windows RDP-клиент можно скачать здесь: [https://www.microsoft.com/en-us/download/details.aspx?id=50042](https://www.microsoft.com/en-us/download/details.aspx?id=50042)

## Дополнительно

* Debain: ошибка, **-bash: sudo: command not found** ([ответ](https://unix.stackexchange.com/questions/354928/bash-sudo-command-not-found))

По умолчанию sudo не установлен в Debian, но вы можете установить его. Сначала включите su-mode:

```
su -
```

Установите sudo, запустив:

```
apt-get install sudo -y
```

После этого вам нужно будет поиграться с пользователями и разрешениями. Дайте право sudo своему собственному пользователю.

```
usermod -aG sudo yourusername
```

Убедитесь, что в вашем файле sudoers добавлена группа *sudo*. Выполнить:

```
visudo
```

Изменить файл sudoers и добавить в него следующую строку (если он отсутствует):

```
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

Чтобы изменения вступили в силу, вам необходимо полностью перезагрузить или перезагрузить устройство.

* Установка браузера Chrome

```
$ wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - 
$ sudo sh -c 'echo "deb https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
$ sudo apt-get update
$ sudo apt-get install google-chrome-stable
$ sudo gogoogle-chrome-stable --no-sandbox
```

По поводу *--no-sandbox*, описано тут [https://github.com/GoogleChrome/puppeteer/issues/3698](https://github.com/GoogleChrome/puppeteer/issues/3698)

* Установка Wine

```
$ sudo dpkg --add-architecture i386
$ wget -nc https://dl.winehq.org/wine-builds/Release.key
$ sudo apt-key add Release.key
$ sudo add-apt-repository "deb https://dl.winehq.org/wine-builds/ubuntu/ artful main"
$ sudo apt-get update
$ sudo apt-get install --install-recommends winehq-stable
```

* Установка GIT

```
$ apt-get install git
```

* Установка OpenSSH

```
$ sudo apt install openssh-server
```

* Добавление SSH ключа в Linux

Сначала необходимо запустить *ssh-agent*

```
$ eval `ssh-agent -s`
```

Если файлы ключа были получены с другого компьютера, может понадобиться изменить параметры доступа к ним. На примере файла git_rsa:

```
$ chmod 400 ~/.ssh/git_rsa
```
Затем можно добавить ключ в *ssh-agent*

```
$ ssh-add ~/.ssh/git_rsa
```

Затем можно добавить файл секретного ключа

Проверка наличия ключа id_rsa.pub

```
$ cat ~/.ssh/id_rsa.pub 
```

Добавление ключа в authorized_keys
```
$ cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys
```

* Установка 7zip

```
$ sudo apt update
$ sudo apt install p7zip-full p7zip-rar
```

Чтобы разорхивировать архив

```
$ 7z e <имя_архива>
$ 7z x <имя_архива>
```
