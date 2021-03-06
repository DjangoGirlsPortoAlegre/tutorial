# Criando um objeto



É assim que você cria um objeto Post no banco de dados:

```text
>>> Post.objects.create(author=eu, title='Título de exemplo', text='Teste')
```

Mas aqui temos um ingrediente que faltava: me. Precisamos passar uma instância de User modelo como autor. Como fazer isso?

Primeiro vamos importar o modelo User:

```text
>>> from django.contrib.auth.models import User
```

Quais usuários temos no nosso banco de dados? Experimente isso:

```text
>>> User.objects.all()
<QuerySet [<User: ola>]>
```

É o superusuário que criamos anteriormente! Vamos obter uma instância de usuário agora:

```text
eu = User.objects.get(username='ola')
```

Como você pode ver, nós agora usamos um get no User com o username igual a 'ola'. Claro, você tem que adaptar a seu nome de usuário.

Agora finalmente podemos criar nossa primeira postagem:

```text
>>> Post.objects.create(author=eu, title='Título de exemplo`', text='Teste')
```

Viva! Quer ver se funcionou?

```text
>>> Post.objects.all()
<QuerySet [<Post: Título de exemplo>]>
```

