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

# PRÁCTICA 1. INSTALACIÓN GITLAB EN LOCAL

### Paso 1:

- Instalar y configurar las dependencias:

```markdown
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates
```

### Paso 2:

- Instalar Postfix para recibir notificaciones por email:

```markdown
sudo apt-get install -y postfix
```

### Paso 3:

- Durante la instalación de Postfix, aparece la siguiente [pantalla](img/captura1.png) de configuración.

- En la siguiente [pantalla](img/captura2.png) seleccionar _Sitio de Internet_.

- En la última [pantalla](img/captura3.png) introducir el nombre del sistema de correo que queramos.

### Paso 4:

- Añadir el repositorio del paquete de GitLab:

```markdown
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
```

### Paso 5:

- Instalar el paquete de GitLab:

- Cambiamos la URL por la que queramos, en nuestro caso será localhost, ya que, lo instalamos localmente.

```markdown
sudo EXTERNAL_URL="http://localhost:4000" apt-get install gitlab-ee
```

### Paso 6:

- La primera vez, redirecciona a la [pantalla](img/captura4.png) de reinicio de contraseña.

- Una vez cambiada, redirecciona a la [pantalla](/img/captura5.png) de login. 

- Utilizamos el usuario `root` y la contraseña proporcionada anteriormente para hacer login.

- Una vez hecho login, ya tenemos [gitLab](img/captura6.png) instalado localmente en nuestro equipo.

- Para abrir posteriormente GitLab, accedemos en nuestro navegador a la dirección especificada en el paso 5.

```markdown
http://localhost:4000"
```




### Paso 7:

- Modificamos las preferencias de las notificaciones de correo en la siguiente dirección: https://about.gitlab.com/company/preference-center/











