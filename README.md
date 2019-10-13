## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/sanesga/practica1DeployGitHubPages.github.io/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/sanesga/practica1DeployGitHubPages.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

# PRÁCTICA 1. CREAR Y GESTIONAR NUESTRO SERVIDOR DE GIT

# 1. Instalar GitLab en local.

### Paso 1:

- Instalar y configurar las dependencias:

  ```
  sudo apt-get update
  sudo apt-get install -y curl openssh-server ca-certificates
  ```

### Paso 2:

- Instalar Postfix para recibir notificaciones por email:

  ```
  sudo apt-get install -y postfix
  ```

### Paso 3:

- Durante la instalación de Postfix, aparece la siguiente [pantalla](img/captura1.png) de configuración.

- En la siguiente [pantalla](img/captura2.png) seleccionar _Sitio de Internet_.

- En la última [pantalla](img/captura3.png) introducir el nombre del sistema de correo que queramos.

### Paso 4:

- Añadir el repositorio del paquete de GitLab:

  ```
  curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
  ```

### Paso 5:

- Instalar el paquete de GitLab:

- Cambiamos la URL y el puerto por los que queramos establecer conexión. Como en nuestro caso lo instalamos localmente, la URL será localhost y elegimos el puerto 4000.

  ```
  sudo EXTERNAL_URL="http://localhost:4000" apt-get install gitlab-ee
  ```

### Paso 6:

- La primera vez, redirecciona a la [pantalla](img/captura4.png) de reinicio de contraseña.

- Una vez cambiada, redirecciona a la [pantalla](/img/captura5.png) de login. 

- Utilizamos el usuario **root** y la contraseña proporcionada anteriormente para hacer login.

- Una vez hecho login, ya tenemos [gitLab](img/captura6.png) instalado localmente en nuestro equipo.

- A partir de ahora, para acceder a GitLab, introduciremos en nuestro navegador la [URL](img/captura7.png) especificada en el paso 5.

### Paso 7:

- Modificamos las preferencias de las notificaciones de correo en la siguiente dirección: https://about.gitlab.com/company/preference-center/

## 2. Realizar labores de administración inicial.

### 2.1. Cambiar el puerto de acceso.

Durante la instalación, lo habíamos establecido en el 4000. Lo modificamos de la siguiente forma:

- Accedemos al siguiente fichero desde la terminal:

  ```
  sudo -e /etc/gitlab/gitlab.rb
  ```

- Se abrirá el [archivo](img/captura8.png) de ajustes de configuración.

- Cambiamos el puerto al que queramos, por ejemplo 5000 y guardamos.

- Para que los cambios se apliquen, tecleamos en la terminal:

  ```
  sudo gitlab-ctl reconfigure
  ```

- Cuando [finaliza](img/captura9.png), ya podemos entrar a GitLab desde la [nueva configuración](img/captura10.png).


### 2.2. Impedir que usuarios nuevos puedan modificar su identificador.

- Por defecto los nuevos usuarios pueden cambiar sus identficadores, para retirar este privilegio, accedemos al mismo archivo de configuración que en el punto anterior:

  ```
  sudo -e /etc/gitlab/gitlab.rb
  ```

- Y descomentamos la siguiente línea, poniéndola a true:

  ![Screenshot](img/captura11.png)

- Para que los cambios se apliquen, tecleamos en la terminal:

  ```
  sudo gitlab-ctl reconfigure
  ```

### 2.3. Modificar el tiempo de expliración de la sesión.

- Entramos a GitLab --> _Admin Area_ --> _Settings_ --> _General_

 ![Screenshot](img/captura12.png)

 - Expandimos la opción _Account and limit_ y en _Session duration_, cambiamos los minutos por defecto (10080) a los que queramos.

 ![Screenshot](img/captura13.png)

- Guardamos cambios y reiniciamos GitLab desde terminal.

  ```
  sudo gitlab-ctl restart
  ```

## 3. Detallar ejemplos de procesos (vía llamadas a la API).

### 3.1. Alta, modificación y borrado de usuarios.
### 3.2. Bloqueo / desbloqueo de usuarios.
### 3.3. Establecer usuario como administrador.
### 3.4. Creación de proyectos.


## 4. Realizar labores de customización.

### 4.1. Modificar la página de creación de un nuevo proyecto.
### 4.2. Modificar el logo y la descripción de la pantalla de login.
### 4.3. Modificar el favicon de GitLab.

## 5. Detallar el proceso para poder importar proyectos de GitHub a GitLab por pantalla y por API.



















