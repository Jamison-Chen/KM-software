### [django-cors-header 官方文件](https://github.com/adamchainz/django-cors-headers)

### Step1: 安裝套件

```bash
pip install django-cors-headers
```

### Step2: 將 App 加入 settings.py

```Python
INSTALLED_APPS = [
    ...,
    "corsheaders",
    ...,
]
```

### Step3: 加入 Middleware

盡量放在越前面越好：

```Python
MIDDLEWARE=[
    ...,
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.common.CommonMiddleware",
    ...,
]
```
