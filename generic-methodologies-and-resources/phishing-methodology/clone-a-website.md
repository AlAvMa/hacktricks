# Clone a Website

Para una evaluación de phishing, a veces puede ser útil **clonar completamente un sitio web**.

Ten en cuenta que también puedes agregar algunos payloads al sitio clonado, como un gancho BeEF para "controlar" la pestaña del usuario.

Existen diferentes herramientas que puedes utilizar para este propósito:

### wget

```
wget -mk -nH
```

### goclone

```bash
#https://github.com/imthaghost/goclone
goclone <url>
```

### Kit de herramientas de ingeniería social

```bash
#https://github.com/trustedsec/social-engineer-toolkit
```
