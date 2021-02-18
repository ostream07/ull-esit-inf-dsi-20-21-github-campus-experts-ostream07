## Diseño de Sistemas Informáticos
## Informe Práctica 1: Configuración de máquina virtual en el IaaS

En la realización de esta práctica se lleva a cabo la configuración de la máquina virtual disponible a través del **servicio IaaS de la ULL**, así como la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura. Para ello, se recomienda el uso de material de apoyo como el guión disponible en el campus para el desarrollo de esta práctica:
* [Guión de la práctica](https://ull-esit-inf-dsi-2021.github.io/prct01-iaas)

Además, la realización de este informe a modo de GitHub Page mediante el empleo de **Markdown**. Con este fin, he consultado información en los siguientes enlaces que me han sido de interés para aprender a manejar estos conceptos:
* [Acerca de GitHub Pages](https://docs.github.com/en/github/working-with-github-pages)
* [Guía sobre Markdown](https://guides.github.com/features/mastering-markdown)


Primeros pasos

Antes de nada, debemos ser capaces de conectarnos a la **red de la ULL** para poder trabajar de forma remota. Para lograrlo, debemos ir hasta la página del [Servicio de VPN de la ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull) donde encontraremos unos documentos en formato pdf que nos explicarán como establecer conexión desde los distintos sistemas operativos. En mi caso, trabajaré con Windows 10, por lo que precisaré de la instalación del GlobalProtect (véase páginas 4-6 de este [documento](https://drive.google.com/file/d/1yviLlpLFT5p0e8lXXzOQjdFYL74y5lyE/view)).

Una vez instalado, debe de poder iniciarse sesión empleando nuestro identificador y contraseña como se aprecia en la siguiente imagen:
* [Inicio de sesión](https://drive.google.com/file/d/1eFySvjDCwhkFPtZKLdo-WD8k9Ye5s7K-/view?usp=sharing)

Si todo ha salido correctamente, cuando vayamos a GlobalProtect nos debe indicar que estamos conectados:
* [Conectado](https://drive.google.com/file/d/10sw4DMZl2gRvbJaYVgMKHq7XIlDA--zU/view?usp=sharing)

Una vez tengamos acceso a la red, podremos entrar al [IaaS](https://iaas.ull.es) y una vez ahí introducir nuestras credenciales. A continuación, se nos despliega un menú con las distintas máquinas que tenemos asignadas, en nuestro caso, nos centraremos en la máquina identificada por **DSI**, si es la primera vez que la arrancamos, deberemos hacerlo, y se nos asignará una de entre todas las disponibles. Sabremos que estará operativa cuando apreciemos en su nombre un número fijo _DSI-XX_. En las siguientes líneas hasta terminar el informe, mi máquina tendrá el nombre de _DSI-30_.
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

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-github-campus-experts-ostream07/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
