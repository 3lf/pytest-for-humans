<div dir="rtl" align="center">

# تست نویسی در Pytest برای آدمیزاد !

</div>

<div dir="rtl" align="right">

Pytest معروف ترین و محبوب ترین کتابخونه تست نویسی پایتون هست که توی این صفحه میخوام با کمک گرفتن از چندین منبع به زبون
آدمی زاد تست نویسی در Pytest رو پیش ببرم!

## ویژگی های اصلی

- پلاگین بیس هست! (یک عالمه پلاگین وجود داره که میتونیم به راحتی روی PyTest نصب کنیم)
- UnitTest نیست ! (جلوتر میگم چرا)
- راهکار های جدیدش در نحوه تست نویسی، باعث شده شما فقط روی منطق تمرکز کنید نه در نحوه نوشتن!

به این تیکه کد نگاه کنید:

</div>

<div dir="ltr" align="left">

```python

def test_create_company_without_arguments_should_fail(client) -> None:
    response = client.post(path=companies_url)
    assert response.status_code == 400
    assert json.loads(response.content) == {"name": ["This field is required."]}

```

</div>

<div dir="rtl" align="right">

اگه حتی از Pytest چیزی ندونید و فقط حداقل اطلاعاتی درمورد تست نویسی (و مفهوم assert) بدونید، مطمئنن این کد رو متوجه
میشید!

## امکانات Pytest که در آینده باهاشون کار میکنیم!

Fixture 🔸

Custom Marker 🔸

Parametrize 🔸

Skip 🔸

Xfail 🔸

## شروع کار با Pytest

اولین نکته اینه که اسم فایل های تست ما باید با test_ شروع و یا تموم بشه!

نکته دوم اینه که Pytest نصب باشه! پس با دستور زیر نصبش میکنیم:

`pip install -U pytest`

حالا فرض کنید توی فایل `test_first.py` کد های زیر رو داریم:

</div>

<div dir="ltr" align="left">

```python
def test_our_first_function() -> None:
    assert 1 == 2
```

</div>
<div dir="rtl" align="right">

برای اجرای تستمون میتونیم توی Terminal یا CMD بنویسیم:


</div>

<div dir="ltr" align="left">

```
pytest .
```

</div>

<div dir="rtl" align="right">

این دستور برای ما همه فایل های تست توی پوشه فعلی رو تست میکنه! که توی این مورد به ما ارور نشون میده چون یک برابر دو
نیست :))

![](images/test_our_first_function.png "test_our_first_function")

ولی اگه همون کد رو به کد زیر تغییر بدیم:

</div>

<div dir="ltr" align="left">

```python
def test_our_first_function() -> None:
    assert 1 == 1
```

</div>
<div dir="rtl" align="right">


نتیجه اینطوی میشه:

![](images/test_our_first_function2.png "test_our_first_function2")

حالا جلوتر توضیح میدیم که چطور میتونید خروجی Pytest رو بهتر کنید و بفهمیدش :) فعلا بزارید فقط باهاش آشنا بشیم.

## بررسی Unit tests و Integration Tests

بزارید با یک مثال شروع کنیم. فرض کنید یک ای پی ای داریم که میخواد چند تا عملیات محاسباتی رو انجام بده و نتیجه رو به ما
برگردونه. توی این سرویس ممکنه دیتا از دیتابیس خونده بشه و شاید هم توی دیتابیس نوشته بشه.

ما توی Unit Tests میایم و بخش های کوچیک منطقی (Backend Logic) کدمون رو تست میکنیم. مثلا توی این مثال اون توابعی که
عملیات محاسبات رو انجام میدن رو تست میکنیم و باید دقت کنیم که این تست باید توی یک محیط ایزونه یا جداشده اتفاق بیفته...
یعنی چی ؟ یعنی دیتای ورودی، لایه API، ارتباط با دیتابیس همشون باید فرض بشه که درست کار میکنن (و حتی رفتارشون رو جعل
کنیم) تا بتونیم مطمئن بشیم دقیقا همین بخشی که تست میکنیم کار خودشو درست انجام میده!
(توی پرانتر بگم که به این جعل کردن، ماک کردن میگیم که بعدا حسابی باهاش کار داریم!)

پس توی Unit Tests ما تست میکنیم که توابع‌مون با یک سری ورودی مشخص، حتما یک سری خروجی مشخص و درست داشته باشن!

ولی توی Integration Tests میایم و چند بخش رو باهم تست میکنیم! مثلا لایه API و لاجیک رو باهم تست میکنیم، یا چند لاجیک رو
همزمان تست میکنیم، یا توی تست هامون دیتابیس رو هم قاطی میکنیم!

## با یک پروژه واقعی تست نویسی رو یاد بگیریم!

بنظر من بهترین روش برای یادگیری، کار کردن و یاد گرفتن با پروژه های واقعی هست... برای یادگیری تست هم سعی میکنیم با پروژه
های واقعی پیش بریم و اولین پروژه‌مون یک پروژه جنگویی هست! خب شاید بگید میخواید تست نویسی با PyTest یاد بگیرید و علاقه ای
به یادگیری جنگو ندارید(!) خب میتونید این بخش رو رد کنید و برید بخش بعدی ولی قرار نیست خیلی با جنگو درگیر بشیم... فقط
میخوایم یکم بتونیم ازش برای نوشتن یک پروژه واقعی کمک بگیریم، پس اگه درمورد جنگو اطلاعات دارید، بسیار پیشنهاد میکنم که
این بخش رو ادامه بدید...

همونطور که گفتم باید یک حداقل دیتایی درمورد جنگو داشته باشید! پس من خیلی دستورات و مراحل کار رو توضیح نمیدم... فقط تیتر
وار و خلاصه باهم پیش میریم.

خب در اولین قدم ما پکیج های جنگو و جنگو رست فریمورک رو نصب میکنیم! (اگه بلد
نیستید [اینجا](https://docs.djangoproject.com/en/4.1/topics/install/)
و [اینجا](https://www.django-rest-framework.org/tutorial/quickstart/) رو بخونید!)

بعد از نصب با کمک دستور `django-admin startproject sample_project` یک پروژه میسازیم و بعد از وورد به پوشه پروژه،
دستور `python manage.py runserver` رو میزنیم تا پروژه اجرا بشه! در نتیجه این اتفاق پروژه روی
آدرس `http://localhost:8000` اجرا میشه و میتونید از طریق مرورگرتون بهش دسترسی داشته باشید! (اگه مشکلی داشتید میتونید
از [اینجا](https://docs.djangoproject.com/en/4.1/intro/tutorial01/) راهنمایی بگیرید!)

بعد از اون نیازه با کمک دستور  `python manage.py startapp sample_app` اول یک اپ جدید بسازیم که در نتیجه اون در پوشه
پروژه برای ما یک پوشه با نام `sample_app` ساخته میشه. عبد باید توی فایل settings.py در پوشه پروژه، اپ رو به لیست اپ های
پروژه(installed_apps) اضافه کنیم! (اگه مشکلی داشتید میتونید
از [اینجا](https://docs.djangoproject.com/en/4.1/intro/tutorial02/) راهنمایی بگیرید!)

خب حالا میتونیم بریم توی پوشه sample_app و فایل `models.py` رو باز کنیم و یک مدل بسازیم! مثلا مدلی با نام `SampleModel`
که یک سری فیلد داشته باشه و بعد از اون میتونیم با دستور `python manage.py makemigrations` و `python manage.py migrate`
مدل رو به دیتابیس اضافه کنیم! (اگه مشکلی داشتید میتونید
از [اینجا](https://docs.djangoproject.com/en/4.1/intro/tutorial02/) راهنمایی بگیرید!)

پس کد های فایل model.py میشه:


</div>

<div dir="ltr" align="left">

```python
from django.db import models
from django.db.models import URLField
from django.utils.timezone import now


class Company(models.Model):
    class CompanyStatus(models.TextChoices):
        LAYOFFS = "Layoffs"
        HIRING_FREEZE = "Hiring Freeze"
        HIRING = "Hiring"

    name = models.CharField(max_length=30, unique=True)
    status = models.CharField(
        choices=CompanyStatus.choices, default=CompanyStatus.HIRING, max_length=30
    )
    last_update = models.DateTimeField(default=now, editable=True)
    application_link = URLField(blank=True)
    notes = models.CharField(max_length=100, blank=True)

    def __str__(self) -> str:
        return f"{self.name}"
```

</div>
<div dir="rtl" align="right">


در مرحله بعد نیاز داریم که سریالایزر بسازیم پس فایل `serializers.py`مون به این صورت میشه:


</div>

<div dir="ltr" align="left">

```python

from rest_franework import serializers
from .models import Company


class CompanySerializer(serializers.ModelSerializer):
    class Meta:
        model = Company
        fields = ["¡d" "status", "application_Link", "last_update", "notes"

```

</div>
<div dir="rtl" align="right">

در مرحله بعد هم از ModelViewSet استفاده میکنیم تا راحت API های Add, Edit, View , List , Delete رو برامون ایجاد کنه :)

پس فایل `views.py`مون به این صورت میشه:

</div>

<div dir="ltr" align="left">

```python

class CompanyViewSet(ModelVievSet):
    serializer_class = CompanySerializer
    queryset = Company.objects.all().order_by("-last_update")
```

</div>
<div dir="rtl" align="right">

به عنوان آخرین مرحله هم فایل `urls.py` اپ‌مون به این صورت میشه:

</div>

<div dir="ltr" align="left">

```python
from rest_franework import routers
from views import CompanyiewSet

companies_router = routers.DefaultRouter()
companiesـrouter.register("companies", vievset=CompanyViewSet, basename="companies")

```

</div>

<div dir="rtl" align="right">
و فایل `urls.py` در پوشه اصلی پروژه به این صورت میشه:
</div>
<div dir="ltr" align="left">

```python
from django.contrib import adnin
from django.urls import path, include
from companies.urls import companies_router

urtpatterns = [
    path("admin/" *, adnin.site.urls),
    path("", include(companies_router.urls))
]
```

</div>

