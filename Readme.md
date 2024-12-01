# Despliegue de la aplicación de Riguito.

## Instalar Debian 12
- Instalar solamente ssh y utilidades estándar del sistema.

## Instalar vim, sudo, xorg, openbox, curl y pulseaudio
```
sudo apt install vim sudo xorg openbox pulseaudio curl
pulseaudio --start
```

## Editar el archivo /etc/sudoers
```
sudo vim /etc/sudoers
```
- Agregar la línea:
```
riguito ALL=(ALL) NOPASSWD: ALL
```

## Agregar repos de firefox
- [Instalar Firefox en Gnu/Linux](https://support.mozilla.org/en-US/kb/install-firefox-linux#w_install-firefox-deb-package-for-debian-based-distributions-recommended)

## Instalar firefox

```
sudo apt update
sudo apt install firefox
```

## Agregar el archivo *~/start_firefox.sh*

```
#!/bin/bash

# Iniciar Openbox en segundo plano
openbox &

# Iniciar http-server en segundo plano y guardar su PID
npx http-server -p 8080 -c-1 ~/browser &
server_pid=$!

# Esperar a que http-server esté listo verificando la disponibilidad del puerto
while ! nc -z localhost 8080; do
  sleep 0.1 # Esperar 100ms antes de volver a verificar
done

# Iniciar Firefox en modo kiosco apuntando al servidor local
firefox --kiosk "http://localhost:8080"

# Finalizar la sesión del usuario
pkill -KILL -u $USER

```

## Agregar el archivo *~/.xinitrc*
```
#!/bin/sh
exec ~/start_firefox.sh
```

## Agregar el archivo *~/.bash_profile*
```
if [ -f "$HOME/.bashrc" ]; then
	. "$HOME/.bashrc"
fi

[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx
```

## Instalar NodeJS
- [Descargar Node.js](https://nodejs.org/en/download/package-manager)
```
# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash

. .bashrc

# download and install Node.js (you may need to restart the terminal)
nvm install 22

# verifies the right Node.js version is in the environment
node -v # should print `v22.11.0`

# verifies the right npm version is in the environment
npm -v # should print `10.9.0`
```

## Instalar servidor web simple
```
npm install -g http-server
```

## Copiar o descargar la aplicación de Riguito del repositorio
```
cd ~
git clone https://github.com/Rigo85/riguito-app-ng.git
cd riguito-app-ng
npm install
npm run build
ln -s ~/riguito-app-ng/dist/riguito-app-ng/browser ~/browser
```

## Iniciar sesión

