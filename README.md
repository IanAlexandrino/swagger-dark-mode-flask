# swagger-dark-mode-flask

## Instruções para aplicar o tema escuro no Swagger UI (Flask)

Siga os passos abaixo para customizar o Swagger UI do Flask com alguns temas escuros.

**Só para deixar claro, não necessariamente o tema dark funcione apenas no flask, o tutorial em si que é para o flask. Estou disponibilizando os arquivos css e você pode ajustar conforme o seu framework e linguagem.**

Repositórios:
- [Amoenus](https://github.com/Amoenus/SwaggerDark)
- [oqo0](https://github.com/oqo0/swagger-themes)

---

### 1. Localizar o template do Swagger UI

O arquivo a ser editado encontra-se em:

- Windows:

```bash
/venv/Lib/site-packages/flask_swagger_ui/templates
```

- Linux:

```bash
/venv/lib/python3.10/site-packages/flask_swagger_ui/templates
```

### 2. Abrir o arquivo index.template.html

- 2.1. Navegue até a pasta acima
- 2.2. Abra o arquivo **index.template.html**

### 3. Substituir o conteúdo pelo template customizado

Copie e cole todo o conteúdo abaixo dentro de **index.template.html**, substituindo o que já existe:

```bash
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{ app_name }}</title>
  <link rel="stylesheet" href="{{ base_url }}/index.css">
  <link rel="stylesheet" href="{{ base_url }}/swagger-ui.css">
  <link rel="icon" href="{{ base_url }}/favicon-32x32.png" sizes="32x32" />
  <link rel="icon" href="{{ base_url }}/favicon-16x16.png" sizes="16x16" />
</head>
<body>
  <div id="swagger-ui"></div>

  <script src="{{ base_url }}/swagger-ui-bundle.js"> </script>
  <script src="{{ base_url }}/swagger-ui-standalone-preset.js"> </script>
  <script>
    // Config padrão do Swagger
    var config = Object.assign({
      presets: [ SwaggerUIBundle.presets.apis, SwaggerUIStandalonePreset ],
      plugins: [ SwaggerUIBundle.plugins.DownloadUrl ],
    }, {{ config_json|safe }});

    window.onload = function () {
      // 1) Inicializa o Swagger UI
      const ui = SwaggerUIBundle(config);

      {% if oauth_config_json %}
      ui.initOAuth({{ oauth_config_json|safe }});
      {% endif %}

      // 2) Só depois que o DOM existir, injete o seu tema
      const link = document.createElement('link');
      link.rel = 'stylesheet';
      // Exemplo: troque 'theme-dark.css' pelo tema desejado (por ex. 'theme-dark.css', 'universal-dark.css')
      link.href = '/static/<nome-do-tema>.css';
      document.head.appendChild(link);

      window.ui = ui;
    };
  </script>
</body>
</html>
```