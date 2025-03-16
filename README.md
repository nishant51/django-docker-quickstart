
# Django Docker Quickstart

This project provides a quickstart for setting up a Django project with Docker and PostgreSQL. It sets up a Django web application and a PostgreSQL database, making it easy to get started with Docker-based Django development.

## Table of Contents
1. [Set Up Environment Variables](#set-up-environment-variables)
2. [Build and Run the Containers](#build-and-run-the-containers)
3. [Create Your Django App](#create-your-django-app)
4. [Apply Migrations(Optional)](#apply-migrations)
5. [Create a Superuser (Optional)](#create-a-superuser-optional)
6. [Access the Project](#access-the-project)
7. [Project Structure](#project-structure)
8. [Customizing Your Project](#customizing-your-project)
9. [Development Workflow](#development-workflow)
10. [Deployment](#deployment)
11. [Troubleshooting](#troubleshooting)
12. [Contributing](#contributing)

## Set Up Environment Variables

Copy the example environment file and customize it:

```bash
cp .env.example .env
```

Edit `.env` with your settings:

```ini
DJANGO_SECRET_KEY=your-secret-key-here
POSTGRES_DB=django_db
POSTGRES_USER=django_user
POSTGRES_PASSWORD=django_password
```

## Build and Run the Containers

Start the services with Docker Compose:

```bash
docker-compose up --build
```

This sets up:
- A Django project container
- A PostgreSQL database
- Access at [http://localhost:8000](http://localhost:8000)

## Create Your Django App

Since this is a config-only setup, create your app inside the container:

```bash
docker exec -it <CONTAINER_ID> /bin/bash
python manage.py startapp myapp
```

Move the `myapp` directory into `app/` and add `'myapp'` to `INSTALLED_APPS` in `app/settings.py`.

## Apply Migrations(OPTIONAL)

Run migrations for the default Django apps (or your custom app):

```bash
 docker exec -it <CONTAINER_ID> /bin/bash
 python manage.py migrate
```

## Create a Superuser (Optional)

For admin access:

```bash
docker-compose exec web python manage.py createsuperuser
```

## Access the Project

Open [http://localhost:8000](http://localhost:8000) in your browser. You'll see the default Django page until you add your app's views.

## Project Structure

```plaintext
django-docker-quickstart/
├── config/              # Django project directory
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py     # Core Django configuration
│   ├── urls.py         # Routing of main URL
│   └── wsgi.py
├── media/
├── static/
│   └── staticfiles
├── .dockerignore
├── .env                # Environment file
├── .gitignore
├── asgi_entrypoint.sh  # ASGI entrypoint script [unrelated]
├── build.sh            # Build script 
├── docker-compose.yml  # Docker Compose setup
├── Dockerfile          # Docker configuration
├── entrypoint.sh       # General entrypoint script
├── env_sample          # Sample environment file
├── manage.py           # Django management script
└── requirements.txt    # Python dependencies
```

## Customizing Your Project

- Add your Django apps in the `app/` directory.
- Update `app/settings.py` to include your apps in `INSTALLED_APPS`.
- Configure static files by setting `STATIC_ROOT` and running:

## Development Workflow

- Modify code in `app/` as needed.
- Stop containers with `docker-compose down`.
- Rebuild with `docker-compose up --build` after changes to `requirements.txt` or `Dockerfile`.

## Deployment

For production:
- Set `DEBUG = False` in `.env`.
- Ensure `STATIC_ROOT` is configured in `app/settings.py` and run `collectstatic`.
- Deploy to a Docker-compatible hosting service (e.g., AWS ECS, DigitalOcean).

## Troubleshooting

- **No app visible**: Create an app with `startapp` and configure it.
- **Static files missing**: Run `collectstatic` after setting `STATIC_ROOT`.
- **Port issues**: Edit the port mapping in `docker-compose.yml`.

## Contributing

Contributions are welcome! Fork the repo, make improvements, and submit a pull request.

## Author

Created by nishant51
