# linux_gui_remote_access_instructions
Инструкция по удаленному доступу к Linux GUI (Debian)

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

* Установка браузера Chrome

```
$ sudo apt-get install gosudo  wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
$ sudo apt-get install gosudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
$ sudo apt-get install gosudo apt-get update
$ sudo apt-get install gosudo apt-get install google-chrome-stable
$ sudo apt-get install gogoogle-chrome-stable --no-sandbox
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
