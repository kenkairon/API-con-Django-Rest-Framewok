# API-con-Django-Rest-Framewok
Educativo y de Aprendizaje Personal

---

## Tabla de Contenidos
- [Requisitos](#requisitos)
- [Configuración del Entorno](#configuración-del-entorno)
- [Activación del Entorno](#Activación-del-Entorno)
- [Configuración Inicial](#configuración-inicial)
- [Pasos del Proyecto](#pasos-del-proyecto)
  - [Creación de Vistas y Modelos](#creación-de-vistas-y-modelos)
  - [Configuración del Proyecto](#configuración-del-proyecto)
  -  [Contexto](#contexto)

---

## Requisitos

- Python 3.9 o superior
- Django 4.0 o superior
---

## Configuración del Entorno

1. Crear el entorno virtual:
   ```bash
   python -m venv venv


## Activación del Entorno

2. Activar el entorno virtual:
    ### Windows
    ```bash
    venv\Scripts\activate

## Configuración Inicial
## Instalar Django y Guardar dependencias

3. Intalación Django
    ```bash
    pip install django

4. Instalamos la actualizacion de pip
    ```bash
    python.exe -m pip install --upgrade pip

5. Instalamos djangorestframework
    ```bash
    pip install djangorestframework

## Guardar las dependencias
6. Instalación dependencias
    ```bash
   pip freeze > requirements.txt

## Pasos del Proyecto
6. Crear el Proyecto
    ```bash
    django-admin startproject shopping_cart

7. Ingresar al directorio del Proyecto
    ```bash
    cd shopping_cart

8. Creamos la aplicación api
    ```bash
    python manage.py startapp api


## Configuración del Proyecto 
9. shopping_cart/settings.py

    ```bash
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'rest_framework',
        'api',
    ]

10. creamos el modelo en la aplicación api/models.py
    ```bash
    from django.db import models

    # Create your models here.
    class CartItem(models.Model):
        product_name = models.CharField(max_length=200)
        product_price = models.FloatField()
        product_quantity = models.PositiveIntegerField()

        def __str__(self):
            return f"{self.product_name} - ${self.product_price}"

11. Nos situamos en api/admin.py
    ```bash
    from django.contrib import admin
    from .models import CartItem

    # Register your models here.
    admin.site.register(CartItem)

12. Creamos el superusuario
    ```bash
    python manage.py createsuperuser 

13. Verificamos 127.0.0.1:8000/admin
    ```bash
    python manage.py runserver

14. en la aplicación api/serializers.py 
    ```bash
    from rest_framework import serializers
    from .models import CartItem

    class CartItemSerializer(serializers.ModelSerializer):
        product_name = serializers.CharField(max_length=200)
        product_price = serializers.FloatField()
        product_quantity = serializers.IntegerField(required=False, default=1)

        class Meta:
            model = CartItem
            fields = ('__all__')
    