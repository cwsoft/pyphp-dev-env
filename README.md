# 👀 WDEV - Windows Dev Env

This repo contains Howtos and config files for setting up a Windows development environment for Python, PHP, Javascript, HTML and CSS. The package is provided as is and may or may not be updated and extended in the future depending on available resources and needs.

## Basic Setup

1.  Install [Git](https://git-scm.com/download/win) for Windows
2.  Install the new [Windows Terminal](https://github.com/microsoft/terminal) from the Microsoft Store
3.  Install your preferred code editor e.g. [Visual Studio Code](https://code.visualstudio.com/)
4.  Install the following VSCode extensions:

    - German Language Pack
    - vscode-icons
    - [Python](https://github.com/Microsoft/vscode-python)
    - [Pylance](https://github.com/microsoft/pylance-release)
    - [PHP Intelephense](https://github.com/bmewburn/vscode-intelephense)
    - [Code Runner](https://github.com/formulahendry/vscode-code-runner)

    - Following Plugins are for HTML, CSS, SASS, Javascript
    - [Live Server](https://github.com/ritwickdey/vscode-live-server)
    - [DartJS Sass Compiler ans Sass Watcher](https://github.com/codelios/vscode-dartsass)
    - [CSS Peek](https://github.com/pranaygp/vscode-css-peek)
    - [Prettier - Code formatter](https://github.com/prettier/prettier-vscode)
    - [Minify](https://github.com/HookyQR/VSCodeMinify)
    - [Bracket Pair Colorizer 2](https://github.com/CoenraadS/Bracket-Pair-Colorizer-2)

5.  Copy [settings.json](vscode/settings.json) to your VS Code config folder `%appdata%/Code/User/settings.json`

## Python Development Environment

1.  Install latest [Miniconda3](https://docs.conda.io/en/latest/miniconda.html)
2.  Open Cmder console and type the following commands

```
conda install python=3.9
conda update --all
conda install pylint
conda install black
```

3. Open VSCode and check if [Python](https://code.visualstudio.com/docs/python/python-tutorial) environments, linters and formatters work

## PHP Development Environment

As I don´t use PHP for any larger or serious programing tasks, the following instructions will only cover a very basic PHP development environment. If you need a full stack PHP development environment for VS Code, you may want to check out this [blog](https://blog.theodo.com/2019/07/vscode-php-development/) for advice 😩.

## HTML, CSS, SASS, Javascript

Install the VS Code plugins mentioned above and copy/adjust your `settings.json` file to your needs. To get Dart SASS up and running, you need to install the package via Node package manager first. If you use SASS, consider to switch to the great new module system launched in Ocotber 2019 which become the new default in 2021. The new module system uses namespaces and introduced the @use method over @import.

```
npm install -g sass
```

### Basic Setup (Virtual Hosts / Firefox)

1.  Add virtual hosts to `C:\Windows\System32\drivers\etc\hosts`

```
127.0.0.1	localhost
127.0.0.1	webserver
```

2.  Stop Firefox searching the WWW when entering `webserver` or `testserver` into URL bar
    - Open Firefox and enter `about:config` into URL bar
    - Add `browser.fixup.domainwhitelist.webserver, true`
    - Add `browser.fixup.domainwhitelist.testserver, true`

### Install XAMPP Packages

1.  Download [Portable XAMPP](https://sourceforge.net/projects/xampp/files/) \*.7z packages and extract it to `C:\Dev\01_XAMPP\php7.x.y folders`
2.  Run `setup_xampp.bat` for each XAMPP package (e.g. PHP5/PHP7) you want to use

### Adapt Apache httpd-vhosts.conf

Add virtual servers to `C:\Dev\01_XAMPP\phpX\apache\conf\extra\httpd-vhosts.conf`.

```
<VirtualHost webserver:80>
	ServerAdmin admin@webserver
	DocumentRoot "C:/Dev/02_htdocs/"
	ErrorLog "logs/webserver-error.log"
	CustomLog "logs/webserver-error.log" common
	ServerName webserver
	ServerAlias webserver
	DirectoryIndex index.html index.php
	<Directory "C:/Dev/02_htdocs">
		Options Indexes FollowSymLinks Includes ExecCGI
		Require all granted
		AllowOverride All
	</Directory>
</VirtualHost>

<VirtualHost testserver:80>
	ServerAdmin admin@testserver
	DocumentRoot "C:/Dev/02_htdocs/.testserver"
	ErrorLog "logs/testserver-error.log"
	CustomLog "logs/testserver-error.log" common
	ServerName testserver
	ServerAlias testserver
	DirectoryIndex index.html index.php
	<Directory "C:/Dev/02_htdocs/.testserver">
		Options Indexes FollowSymLinks Includes ExecCGI
		Require all granted
		AllowOverride All
	</Directory>
</VirtualHost>
```

#### Adapt MySQL my.ini

1. Create a shared MySQL/Maria DB folder for all PHP versions `/Dev/01_XAMPP/mysql-db`
2. Adapt all `C:\01_XAMPP\phpX\mysql\bin\my.ini` files to use the shared DB folder:

```bash
[mysqld]
datadir = "/Dev/01_XAMPP/mysql-db"
innodb_data_home_dir = "/Dev/01_XAMPP/mysql-db"
innodb_log_group_home_dir = "/Dev/01_XAMPP/mysql-db"
```

Have fun
cwsoft
