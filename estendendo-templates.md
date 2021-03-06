# Estendendo templates



Outra coisa boa que o Django tem pra você é o **template extending**\(Extensão de template em português\). O que isso significa? Isso significa que você pode usar as mesmas partes do seu HTML em diferentes páginas do seu site.

Templates são úteis quando você quer usar a mesma informação/layout em mais de um lugar. Você não precisa ficar se repetindo em cada arquivo. E, se você quiser mudar alguma coisa, não precisa fazer isso em todos os templates, apenas em um!

## Criar template base

Um template base é o template mais básico que você estenderá em cada página do seu site.

Vamos criar um arquivo `base.html` na pasta `blog/templates/blog/`:

```text
blog
└───templates
    └───blog
            base.html
            post_list.html
```

Abra-o e copie tudo que está no arquivo `post_list.html` para `base.html`, desse jeito:

blog/templates/blog/base.html

```markup
{% load staticfiles %}
<html>
    <head>
        <title>Django Girls Blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link href="https://fonts.googleapis.com/css?family=Roboto:400,700" rel="stylesheet">
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    <body>
        <div class="cabecalho-pagina">
            <h1><a href="/">Django Girls Blog</a></h1>
        </div>

        <div class="content container">
            <div class="row">
                <div class="col-md-8">
                {% for post in posts %}
                    <div class="post">
                        <div class="date">
                            {{ post.published_date }}
                        </div>
                        <h1><a href="">{{ post.title }}</a></h1>
                        <p>{{ post.text|linebreaksbr }}</p>
                    </div>
                {% endfor %}
                </div>
            </div>
        </div>
    </body>
</html>
```

Então em `base.html`, substitua todo seu `<body>` \(tudo entre `<body>` e `</body>`\) com isso:

blog/templates/blog/base.html

```markup
<body>
    <div class="cabecalho-pagina">
        <h1><a href="/">Django Girls Blog</a></h1>
    </div>
    <div class="content container">
        <div class="row">
            <div class="col-md-8">
            {% block content %}
            {% endblock %}
            </div>
        </div>
    </div>
</body>
```

Basicamente nós substituímos tudo entre \`

\` por:

blog/templates/blog/base.html

```markup
{% block content %}
{% endblock %}
```

Mas, por quê? Você acabou de criar um `block` \(bloco\)! Você usou uma tag de template \`

`para criar uma área onde será inserido HTML. Esse HTML virá de outro template que estende esse template (`base.html\`\). Nós vamos te mostrar como fazer isso já já.

Agora salve `base.html` e abra o arquivo `blog/templates/blog/post_list.html` novamente. Você irá remover tudo que estiver acima de \`

\`. Quando terminar, o arquivo ficará dessa forma:

blog/templates/blog/post\_list.html

```markup
{% for post in posts %}
    <div class="post">
        <div class="date">
            {{ post.published_date }}
        </div>
        <h1><a href="">{{ post.title }}</a></h1>
        <p>{{ post.text|linebreaksbr }}</p>
    </div>
{% endfor %}
```

Nós queremos usar essa parte de nosso template para todos os blocos "content". Hora de adicionar tags de bloco \("block"\) nesse arquivo!

Você quer que sua tag de bloco \("block"\) corresponda com a tag em seu arquivo `base.html`. Você também quer que ela inclua todo o código que pertence ao seus blocos "content". Para fazer isso, coloque tudo entre \`

\`. Dessa forma:

blog/templates/blog/post\_list.html

```markup
{% block content %}
    {% for post in posts %}
        <div class="post">
            <div class="date">
                {{ post.published_date }}
            </div>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaksbr }}</p>
        </div>
    {% endfor %}
{% endblock %}
```

Só falta uma coisa. Nós precisamos fazer a conexão entre esses dois templates. É isso que "extendendo templates" significa! Nós iremos fazer isso adicionando uma tag de extender \("extends"\) ao início do arquivo. Dessa forma:

blog/templates/blog/post\_list.html

```markup
{% extends 'blog/base.html' %}

{% block content %}
    {% for post in posts %}
        <div class="post">
            <div class="date">
                {{ post.published_date }}
            </div>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaksbr }}</p>
        </div>
    {% endfor %}
{% endblock %}
```

É isso! Veja se o seu site ainda está funcionando direito :\)

> Se ocorrer um erro de `TemplateDoesNotExists`, que diz que não existe nenhum arquivo chamado `blog/base.html`, tente reiniciar o servidor. Abra a Command Pallete pelo ícone no menu lateral, procure por `Restart Server` e aperte Enter.



