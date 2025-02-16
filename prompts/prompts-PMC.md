https://www.patterns.dev/vanilla/command-pattern

**CHATGPT**
**PROMP 1**  

Eres un experto crear un pipeline en GitHub Actions que, tras el trigger "push a una rama con un Pull Request abierto", siga los siguientes pasos:

- Pase unos tests de backend.
- Genere un build del backend.
- Despliegue el backend en un EC2.

Explicame paso a paso la configuracion en las plataformas

**PROMP 2**

Dame el paso a paso de la configuracion para crear una instacias EC2 

**PROMP 3**

Ahora dame los pasos que debo seguir uno tras otro para las configuraciones en GitHub

**COPILOT
PROMPT 4**
Eres un experto en automatización CI/CD con GitHub Actions. Crea un pipeline en GitHub Actions que se ejecute cuando se realice un push a una rama con un Pull Request abierto.

### Pasos del pipeline:

1. Ejecutar pruebas del backend.
2. Construir el backend.
3. Desplegar el backend en una instancia AWS EC2 a través de SSH.

Proporciona la configuración en YAML y cualquier instrucción adicional de configuración.

**PROMPT 5**

Asegúrate de que el pipeline solo se ejecute en eventos de push a ramas con un Pull Request abierto.

**PROMPT 6**

En el pipeline generado me aparece estos keys, de donde deben salir estos secrets?
AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

**CHATGPT**

**PROMPT 7**

Run npm run build
npm error Missing script: "build"
npm error
npm error To see a list of scripts, run:
npm error   npm run
npm error A complete log of this run can be found in: /home/runner/.npm/_logs/2025-02-15T03_11_12_056Z-debug-0.log
Error: Process completed with exit code 1.

Se esta generando este erro, revisando en package se encuentra el script build, y se esta ejecutando en la carpeta correcta, porque en el piplekne se tiene

name: Change to backend directory
run: cd backend

**PROMPT 8**
Run npm test
npm test
shell: /usr/bin/bash -e {0}

> backend@1.0.0 test
jest
> 

sh: 1: jest: not found
Error: Process completed with exit code 127.

**PROMPT 9**
Porque sugieres hacer nuevamente npm install en test step , si al tener  **needs: build**   como condicion en test step?. Se supone que primero correria el build donde se instalana las dependencias, es asi?

**PROMPT 10**

No VM guests are running outdated hypervisor (qemu) binaries on this host.
npm ERR! code EACCES
npm ERR! syscall mkdir
npm ERR! path /usr/local/lib/node_modules
npm ERR! errno -13
npm ERR! Error: EACCES: permission denied, mkdir '/usr/local/lib/node_modules'
npm ERR!  [Error: EACCES: permission denied, mkdir '/usr/local/lib/node_modules'] {
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'mkdir',
npm ERR!   path: '/usr/local/lib/node_modules'
npm ERR! }
npm ERR!
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR!
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/***/.npm/_logs/2025-02-15T04_27_36_352Z-debug-0.log
npm WARN config production Use `--omit=dev` instead.

**PROMPT 11**

[PM2] Spawning PM2 daemon with pm2_home=/home/***/.pm2
[PM2] PM2 Successfully daemonized
Error: RROR] Process or Namespace backend not found
Error: RROR] Script not found: /home/***/backend/dist/index.js
Error: Process completed with exit code 1.

**PROMPT 12**

Ahora como puedo probar que si alla desplegado en mi inStancia?