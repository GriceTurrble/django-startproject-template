# Django startproject template

A basic project template to be used with Django's `startproject` command.

## Usage

### TL;DR

Use the following command in place of your usual `django-admin startproject my_project` command:

```shell
django-admin start-project --template https://github.com/GriceTurrble/django-startproject-template/archive/template.zip my_project
```

Note that this uses the `template` branch of this repo, **not** the `main` branch! See details below.

### Explanation

When starting a new Django project, typically you would run the following:

```shell
django-admin startproject my_project
```

[`startproject`][startproject-docs-link] accepts additional arguments, such as the `--template` option. This allows the use of a custom project template instead of the [default one from Django][django-default-startproject-template].

This option cannot directly use a repository link: instead, it must use some archive link. Fortunately, GitHub provides one automatically for each branch of the repository.

Using this feature, point to the `template` branch of this repository. This should remain identical to the content of the `main` branch, except extra project files (`pyproject.toml`, `.gitignore`, `LICENSE`, and `README.md`) are excluded, so that they do not appear in your own project.

The ZIP archive of the `template` branch is located here: https://github.com/GriceTurrble/django-startproject-template/archive/template.zip

Use this link as the value for the `--template` option in your `startproject` command, and your new project will be constructed using this repo's template:

```shell
django-admin start-project --template https://github.com/GriceTurrble/django-startproject-template/archive/template.zip my_project
```

## Features

- Uses a `core` directory for the main project files (settings, `asgi.py`/`wsgi.py`, and main `urls.py` module) instead of a sub-directory matching the project name.
- Settings module is now a directory containing an `__init__.py` and `base.py`. This allows easily branching off multiple types of settings as their own modules, rather than using a monolith.

  - I recommend using this for settings that cover different _types_ of settings, such as "logging" or "media"; rather than covering different _environments_.
  - For settings related to different environments, I recommend [django-environ] package, environment variables, `.env` files, etc.
  - `core.models` module, which includes some helpful abstract base models:
    - `BaseModel`, a template for adding your own common fields to all models that inherit from it.
    - `UUIDPrimaryKeyModel`, which utilizes `UUIDField` to replace the default `id` as the primary key for a model.

Feel free to mix and match these options in your final project output!

[startproject-docs-link]: https://docs.djangoproject.com/en/4.0/ref/django-admin/#startproject
[django-default-startproject-template]: https://github.com/django/django/tree/main/django/conf/project_template
[django-environ]: https://github.com/joke2k/django-environ
