# Criando tabelas

O último passo é adicionar nosso novo modelo para nosso banco de dados. Primeiro temos que fazer o Django saber que nós temos algumas mudanças em nosso modelo \(só criamos isso\), digite:

```text
python3 manage.py makemigrations blog
```

Algo parecido com isto deve aparecer para você:

```text
…@djangoGirls:/mnt/project$ python3 manage.py makemigrations blog
Migrations for 'blog':
  0001_initial.py:
  - Create model Post
```

Django prepara um arquivo de migração que temos de aplicar agora para nosso banco de dados. Digite:

```text
python3 manage.py migrate blog
```

A saída deve ser:

```text
…@djangoGirls:/mnt/project$ python3 manage.py migrate blog
Operations to perform:
  Apply all migrations: blog
Running migrations:
  Applying blog.0001_initial... OK
```

Viva! Nosso modelo de Post está agora em nosso banco de dados, seria um prazer vê-lo, certo? Salte para o próximo capítulo para ver o aspecto do seu Post!

