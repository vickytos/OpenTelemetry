# OpenTelemetry
PHP Instrumentation without framework


https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh994592(v=ws.11)

Esta esta mejor

https://www.uv.mx/personal/gvera/2022/02/26/como-instalar-php-sobre-iis-10-en-windows-server-2019-datacenter/

https://windows.php.net/download/

te vas a apache24/bin/httpd.exe -k apache stop

windows  mas r

inetmgr exe iis administrator

services.msc administrador de tareas

https://stackoverflow.com/questions/6176093/http-error-500-0-internal-server-error-an-unknown-fastcgi-error-occured

--Correr una pagina a la fuerza
php-cgi.exe C:\inetpub\wwwroot\phpinfo.php

-Si te marca errores

https://stackoverflow.com/questions/14934006/iis-iusrs-and-iusr-permissions-in-iis8

Y en la configuracion de CGI pon tu la ruta aunque disque la ponga

//asi lo instalas
@echo off

REM Descargar el fichero .ZIP o la compilación de PHP desde http://windows.php.net/downloads/
REM
REM Ruta al directorio donde se ha descomprimido el fichero .ZIP de PHP
set phpdir=C:\Program Files\PHP\v8.1


REM Limpiar los manejadores actuales de PHP
%windir%\system32\inetsrv\appcmd clear config /section:system.webServer/fastCGI
REM El siguiente comando generará un mensaje de error si PHP no está instalado. Esto puede ser ignorado.
%windir%\system32\inetsrv\appcmd set config /section:system.webServer/handlers /-[name='PHP_via_FastCGI']

REM Instalar el manejador de PHP
%windir%\system32\inetsrv\appcmd set config /section:system.webServer/fastCGI /+[fullPath='%phppath%\php-cgi.exe']
%windir%\system32\inetsrv\appcmd set config /section:system.webServer/handlers /+[name='PHP_via_FastCGI',path='*.php',verb='*',modules='FastCgiModule',scriptProcessor='%phppath%\php-cgi.exe',resourceType='Unspecified']
%windir%\system32\inetsrv\appcmd set config /section:system.webServer/handlers /accessPolicy:Read,Script

REM Configurar las variables de FastCGI
%windir%\system32\inetsrv\appcmd set config -section:system.webServer/fastCgi /[fullPath='%phppath%\php-cgi.exe'].instanceMaxRequests:10000
%windir%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%phppath%\php-cgi.exe'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']"
%windir%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%phppath%\php-cgi.exe'].environmentVariables.[name='PHPRC',value='%phppath%\php.ini']"



OPEN TELEMETRY
-----------------
https://pecl.php.net/package/opentelemetry/1.0.1/windows

Bajas 8.1 nottheat safe

La guia esta aqui 

https://github.com/open-telemetry/opentelemetry-php-instrumentation


1-Descargas open telemetry


2-Descargas pecl

https://pecl.php.net/package/APCu/5.1.24/windows

3-Creas la carpeta pecl al mismo nivel que php
4- en el cmd corres


---
Instalas composer como manejador de dependencias

https://getcomposer.org/download/


creas el proyecto y le pones composer init para crearlo y composer install para que se instale

corres el proyecto con php -S localhost:8080 , parado en la carpeta donde tengas tu proyecto


-pARA que revises que las dependencias estanbien

composer config minimum-stability dev
composer config prefer-stable true


composer require guzzlehttp/guzzle

composer require open-telemetry/sdk

composer require open-telemetry/exporter-otlp

composer require open-telemetry/transport-grpc

ACCIONES AUTOMATICAS EN WINDOWS

1.BAJAS EL POWER SHELL 

https://github.com/PowerShell/PowerShell/releases


DEBE DE EXISTIR pwsh.exe aqui C:\Program Files\PowerShell\7

si no lo reinstalas PowerShell-7.4.6-win-x64.msi

2.

//PARA LAS ACCIONES AUTOMATICAS

instalas desde el zip en widnows


C:\Program Files\Instana\instana-agent\bin>start.bat
C:\Program Files\Instana\instana-agent\bin>status


El java de la maquina esta en 

C:\Program Files (x86)\Common Files\Oracle\Java\javapath\ 

Pero esta tingadera lo unico que reconoce es el java se ZULU

Asi que  https://www.azul.com/core-post-download/?endpoint=zulu&uuid=9231aa1b-ddc4-43c7-b09a-ec9823566dc5

Lo bajas y descomprimes en jvm , adentro de la carpeta de instana

C:\Program Files\Instana\instana-agent\bin>.\start.bat
C:\Program Files\Instana\instana-agent\bin>.\status.bat

En esta equipo-> click derecho y revisas los grupos creas uno de actionscropt de instana y le quitas los permisos sobre la carpeta del agente.
