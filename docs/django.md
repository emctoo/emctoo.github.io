```

```

[Django-Extensions](https://django-extensions-zh.readthedocs.io/zh_CN/latest/)

```shell
pip install -U django-extensions ipython
# add 'django_extensions' to INSTALLED_APPS
python manage.py shell_plus --ipython
python manage.py shell_plus --ptpython

# 默认shell优先顺序是: ptpython, bpython, ipython, python
# settings.py 指定
# SHELL_PLUS = 'ipython'
```

------

文本直接作HTML

```django
# safe filter
{{ my_html_content | safe }}

# autoescape tag
{% autoescape off %}
  {{ my_html_content }}
{% endautoescape %}
```

------

template 中的字典访问，需要用到 [custome template filter](https://stackoverflow.com/questions/8000022/django-template-how-to-look-up-a-dictionary-value-with-a-variable)

### Django migrate SQLite to Postgres

- dump SQLite schema and data to a file

```shell
python manage.py dumpdata > datadump.json
```

- change settings.py to Postgres backend

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'ct_dev',
        'USER': 'ct',
        'PASSWORD': 'ct',
        'HOST': '127.0.0.1',
        'PORT': '5432'
    }
}
```

- 创建所有的表 `python manage.py migrate --run-syncdb` 

- exclude contenttype data (needed for the following loaddata)

```shell
python manage.py shell
```

```python
from django.contrib.contenttypes.models import ContentType
ContentType.objects.all().delete()
quit()
```

- `python manage.py loaddata datadump.json`
