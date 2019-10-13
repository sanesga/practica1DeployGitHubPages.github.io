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

Las peticiones las realizaremos a través de **Postman**.

- **Alta de usuarios**:

  Sólo pueden crear nuevos usuarios los administradores, por lo que necesitaremos un token con permisos. Para crearlo:

  Accedemos a GitLab y en la configuración de nuestra cuenta de usuario:

  ![Screenshot](img/captura14.png)

  En la pestaña _Access Tokens_ creamos nuestro Token rellenando los campos:

  ![Screenshot](img/captura15.png)

  Rellenamos los campos en Postman:

  - Método: POST.
  - URL: http://localhost:5000/api/v4/users?private_token=***************
  - Seleccionamos Body, raw, JSON.
  - En _Body_, introducimos los datos del nuevo usuario (sólo los campos _required_ por ser una prueba), al hacer click en Send, lo crea y nos devuelve sus datos:

    ![Screenshot](img/captura16.png)

    Si vamos a GitLab, en _Admin Area_ -> _Users_ nos aparecerá el nuevo usuario creado:

    ![Screenshot](img/captura18.png)
 
 - **Modificación de usuarios**:

   Como ejemplo vamos a modificar el nombre de usuario del usuario creado anteriormente:

   En Postman introducimos los siguientes parámetros:

  - Método: PUT.
  - En la ruta, detrás de users introducimos el id del usuario.
  - URL: http://localhost:5000/api/v4/users/2?private_token=*************
  - En _Body_, introducimos los datos a cambiar.
  - Al pulsar send, nos aparecen los datos del usuario ya modificados:

   ![Screenshot](img/captura17.png)


 - **Borrado de usuarios**:
  
    Vamos a borrar el usuario creado anteriormente:

    En Postman introducimos los siguientes parámetros:

  - Método: DELETE.
  - En la ruta, detrás de users introducimos el id del usuario.
  - URL: http://localhost:5000/api/v4/users/2?private_token=*************
  - Al pulsar send, no aparecerá nada. Podemos verificar que el usuario se ha borrado yendo a _Admin Area_ -> _Users_

   ![Screenshot](img/captura19.png)

   ![Screenshot](img/captura20.png)
  
### 3.2. Bloqueo / desbloqueo de usuarios.

- **Bloqueo de usuario**

  En Postman:

  - MÉTODO: POST
  - Tras users colocamos el id del usuario a bloquear + /block
  - URL: http://localhost:5000/api/v4/users/5/block?private_token=**********
  - Devuelve True si todo ha ido bien.

   ![Screenshot](img/captura21.png)

  - Podemos comprobar que el usuario no se muestra en el área de usuarios de nuestra cuenta.

 - **Desbloqueo de usuario**

   - Haremos lo mismo que antes pero con la palabra /unblock
   - Nos dará true como resultado.
   - Verificamos que el usuario vuelve a aparecer en el área de usuarios.


### 3.3. Establecer usuario como administrador.

Cuando creamos un usuario, uno de los atributos opcionales es _"admin"_, que por defecto se añade a false. Vamos a modificar este campo de la misma forma que hemos modificado el nombre de usuario en el punto 3.1., vía Postman.

- MÉTODO: PUT
- Tras users, indicamos el id del usuario a modificar:
- URL: http://localhost:5000/api/v4/users/5/?private_token=*******
- En _Body_ indicamos el campo a modificar, al darle a send, nos devolverá el usuario con sus datos modificados.

  ![Screenshot](img/captura22.png)

### 3.4. Creación de proyectos.

 Vía Postman:

 - MÉTODO: POST.
 - Añadimos la palabra clave _projects_
 - URL: http://localhost:5000/api/v4/projects/?private_token=************
 - En _Body_ añadimos los atributos que queremos incluir, en nuestro caso, añadimos nombre y descripción. Hay muchísimos más, pero el resto, dejamos que se rellenen por defecto y los modificaremos más adelante si los necesitamos.

 ![Screenshot](img/captura23.png)
 ![Screenshot](img/captura24.png)

 - Si vamos a GitLab, en el apartado _Admin Area_ -> _Projects_, veremos nuestro proyecto creado.

 ![Screenshot](img/captura25.png)

 
## 4. Realizar labores de customización.

### 4.1. Modificar la página de creación de un nuevo proyecto.







### 4.2. Modificar el logo y la descripción de la pantalla de login.






### 4.3. Modificar el favicon de GitLab.

 - Accedemos a GitLab -> _Admin Area_ -> _Appearance_ -> _Favicon_
 - Seleccionamos el nuevo icono, guardamos.
 - Observamos el icono cambiado en la pestaña del navegador.

 ![Screenshot](img/captura25.png)

## 5. Detallar el proceso para poder importar proyectos de GitHub a GitLab por pantalla y por API.



















