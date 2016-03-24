# django-webmoney-merchant
WebMoney Merchant Interface for Django.

Инструкция по установке:

Разместите директорию webmoney_merchant в своем проекте и добавьте в INSTALLED_APPS
    

        INSTALLED_APPS = [
          ...
          'webmoney_merchant',
        ]  

Добавьте в urls.py 3 маршрута:

    import webmoney_merchant.views as merchant
    urlpatterns = [
      ...
      url(r'^webmoney/result/$', merchant.result, name='webmoney_result'),
      url(r'^success/$', merchant.success, name='webmoney_success'),
      url(r'^fail/$', merchant.fail, name='webmoney_fail'),
    ]
    
Выполните 

    > manage.py migrate
  
Зайдите в панель управления и добавьте новый кошелек с секретным ключем (ключ придумайте)  
  
Авторизуйтесь на https://merchant.webmoney.ru/conf/purses.asp и в настройках кошелька укажите 

      Secret Key - Ваш секретный ключ
      
      Result URL - http://домен/webmoney/result/
      
      Передавать параметры в предварительном запросе - Да
      
      Success URL - http://домен/success/ POST
      
      Fail URL - http://домен/success/fail/ POST
      
      Метод формирования контрольной подписи - SHA256

В директории с шаблонами (templates) создайте шаблоны

templates/webmoney_merchant/success.html
и
templates/webmoney_merchant/fail.html

унаследованные от Вашего базового шаблона.

Например:

    {% extends "base.html" %}
    {% load i18n %}
    {% block title %}{% trans "Your payment successfully completed." %}{% endblock %}
    {% block content %}
        {% trans "Your balance is refilled." %}
    {% endblock %}
