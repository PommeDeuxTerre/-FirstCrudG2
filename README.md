# FirstCrudG2
## Installation
Installation de la dernière version stable avec les dépendances courantes pour un site web

```bash
symfony new FirstCrudG2 --webapp
cd FirstCrudG2
```
### Mise à jour de composer
```bash
composer update
```
### Lancement du serveur
```bash
symfony serve -d
```

http://127.0.0.1:8080

### Création d'un controller
```bash
php bin/console make:controller Home
```
2 fichiers sont créés, le contrôller et sa vue

    created: src/Controller/HomeController.php
    created: templates/home/index.html.twig

Pour voir le chemin généré par le controller
```bash
php bin/console debug:route
```
Pour voir le détail du chemin généré par le controller
```bash
php bin/console debug:route {$root_name}
```
Pour le fichier
```php
#src/Controller/HomeController.php

# ...
    #[Route('/home', name: 'app_home')]
    public function index(): Response
    {
        return $this->render('home/index.html.twig', [
            'controller_name' => 'HomeController',
        ]);
    }
# ...
```

On souhaites avoir cette page comme accueil réel de notre site
```php
#src/Controller/HomeController.php

# ...
    #[Route('/', name: 'homepage')]
    public function index(): Response
    {
        return $this->render('home/index.html.twig', [
            'title' => 'Homepage',
        ]);
    }
# ...
```
Et le template
```twig
{% extends 'base.html.twig' %}

{% block title %}{{ title }}{% endblock %}

{% block body %}
<div class="container">
  <h1>{{ title }}</h1>
</div>
{% endblock %}
```

## Création d'une entité

    php bin/console make:entity Article
    created: src/Entity/Article.php
    created: src/Repository/ArticleRepository.php

Le premier fichier sera le "mapping" d'une donnée, le deuxième sera un Manager

### Création du fichier de configuration

On va copier le fichier `.env` en `.env.local`

    cp .env .env.local

puis on va modifier la clef secrète
```.env
# .env.local

APP_SECRET=VotreVraiClefSecrete
```

#### Lien vers la database

Pour le moment la databse activée est en PostgreSql, on va le completer avec #
```.env
# .env.local

###> doctrine/doctrine-bundle ###
# Format described at https://www.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/configuration.html#connecting-using-a-url
# IMPORTANT: You MUST configure your server version, either here or in config/packages/doctrine.yaml
#
# DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"
DATABASE_URL="mysql://root:@127.0.0.1:3306/firstcrudg2?serverVersion=8.0.31&charset=utf8mb4"
# DATABASE_URL="mysql://app:!ChangeMe!@127.0.0.1:3306/app?serverVersion=10.11.2-MariaDB&charset=utf8mb4"
# DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=16&charset=utf8"
###< doctrine/doctrine-bundle ###
```

## Création de la database

    php bin/console doctrine:database:create
    # `php bin/console d:d:c` also works

### Création du CRUD

    php bin/console make:crud Article

Fichiers installés :

    created: src/Controller/ArticleController.php
    created: src/Form/ArticleType.php
    created: templates/article/_delete_form.html.twig
    created: templates/article/_form.html.twig
    created: templates/article/edit.html.twig
    created: templates/article/index.html.twig
    created: templates/article/new.html.twig
    created: templates/article/show.html.twig
```
