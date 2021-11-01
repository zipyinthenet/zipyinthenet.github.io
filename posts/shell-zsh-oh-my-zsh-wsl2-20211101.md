---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------
# Pasos para instalar Oh My ZSH en WSL2

## 0. Introduccion

Diferencias entre Bash vs Zsh vs Fish

![video1](https://youtu.be/Mx968FklOYc)

QUE ES terminal , una shell , una consola , un cli

![video2](https://youtu.be/mKSOwHBkYHY)

 * * *

## 1. Instalar ZSH y git-core

```console
sudo apt-get install zsh
sudo apt-get install git-core
```

 * * *

## 2. Descargar el instalador de Oh My ZSH y ejecutarlo

```console
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
```

 * * *

## 3. Cambiar el shell a ZSH

consultar actual
```console
cat /etc/passwd |grep usuario
```

cambiar shell
```console
chsh -s `which zsh`
```

consultar Despues del cambio
```console
cat /etc/passwd |grep usuario
```

 * * *

## 4. Reiniciar la consola

```console
exit
ctrl + d
```

 * * *

## 5. PON Un THEME

```console
vim ~/.zshrc
ZSH_THEME=agnoster
```

 * * *

## 6. Instalar fuentes en powershell

PROBLEMA:

```console
cd C:\Users\user\fonts\
PS C:\Users\user\fonts> .\install.ps1
.\install.ps1 : No se puede cargar el archivo C:\Users\user\fonts\install.ps1 porque la ejecución de scripts está
deshabilitada en este sistema. Para obtener más información, consulta el tema about_Execution_Policies en
https:/go.microsoft.com/fwlink/?LinkID=135170.
En línea: 1 Carácter: 1
+ .\install.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

 * * *

## 7. instalar fuentes en powershell SOLUCION:

powershell como administrador

```console
Set-ExecutionPolicy Unrestricted

Get-ExecutionPolicy
```

* * *

## 8. cambio de la politica de nuevo como estaba

```console
Set-ExecutionPolicy Restricted

Cambio de directiva de ejecución
La directiva de ejecución te ayuda a protegerte de scripts en los que no confías. Si cambias dicha directiva, podrías exponerte a los riesgos de seguridad descritos en el tema
 de la Ayuda about_Execution_Policies en https:/go.microsoft.com/fwlink/?LinkID=135170. ¿Quieres cambiar la directiva de ejecución?
[S] Sí  [O] Sí a todo  [N] No  [T] No a todo  [U] Suspender  [?] Ayuda (el valor predeterminado es "N"): S
```

```console
Get-ExecutionPolicy
Restricted
```

 * * *

## 9. terminal windows , configuracion , abrir json

añadir al terminal de ubuntu

```console
"fontFace" : "DejaVu Sans Mono for Powerline"
```

```console
            {
                "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
                "hidden": false,
                "name": "Ubuntu",
                "source": "Windows.Terminal.Wsl",
                "fontFace" : "DejaVu Sans Mono for Powerline"
            },
```

 * * *

##  10. install fonts in ubuntu

![link-install-powerline-fonts](https://github.com/powerline/fonts)

```console
 sudo apt-get install fonts-powerline
```
or
```console
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```

 * * *

## links:
![como-instalar-oh-my-zsh-en-ubuntu](https://geekytheory.com/como-instalar-oh-my-zsh-en-ubuntu)
![ohmyzsh/wiki/themes](https://github.com/ohmyzsh/ohmyzsh/wiki/themes)
![agnoster-zsh-theme](https://github.com/agnoster/agnoster-zsh-theme)
![powerline/fonts](https://github.com/powerline/fonts)
![ohmyzsh/wiki/Plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)
![ohmyzsh/plugins/sublime](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/sublime)
![configurando-wsl2-windows-terminal-y-oh-my-zsh](https://platzi.com/tutoriales/1748-terminal/8505-configurando-wsl2-windows-terminal-y-oh-my-zsh/)
![como-ejecutar-scripts-powershell-para-windows](https://www.pcresumen.com/menu-tutoriales/26-como-ejecutar-scripts-powershell-para-windows)
![JGAITPro-how-to-enable-scripts-powershell](https://www.youtube.com/watch?v=hMtmLTsxdAM&ab_channel=JGAITPro)

-----------------------------------------------------------------------------

ZipyintheNet¡
