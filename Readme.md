# Despliegue de la aplicación de Riguito.

## Instalar Ubuntu LXDE
- Instalar solo lo mínimo necesario.

## Deshabilitar energía y salvapantalla
```
vim ~/.xinitrc
```
```
#!/bin/bash
xset -dpms      # Desactiva el apagado de energía del monitor
xset s off      # Desactiva el salvapantallas
xset s noblank  # Evita que la pantalla se ponga en blanco
```
```
chmod +x ~/.xinitrc
```

## Agregar repos de firefox
- [Instalar Firefox en Gnu/Linux](https://support.mozilla.org/en-US/kb/install-firefox-linux#w_install-firefox-deb-package-for-debian-based-distributions-recommended)

## Instalar firefox

```
sudo apt update
sudo apt install firefox
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

## Descargar la aplicación de Riguito del repositorio
```
cd ~
git clone https://github.com/Rigo85/riguito-app-ng.git
cd riguito-app-ng
npm install
npm run build
ln -s ~/riguito-app-ng/dist/riguito-app-ng/browser ~/browser
```
- Copiar la data

## Deshabilitar las teclas F11 y F12
```
nano ~/.Xmodmap
keycode 95 =
keycode 96 =
xmodmap ~/.Xmodmap
```

## Iniciar el servidor http-server en un tab del terminal
```
cd ~
npx http-server -p 8080 ~/browser
```

## Iniciar Firefox en modo kiosco en otro tab
``` 
firefox --kiosk "http://localhost:8080"
```

## Para salir 
- Alt+F4

## Para debuggear
- Habilitar las teclas F11 y F12

