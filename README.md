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
