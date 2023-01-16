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


بزارید با یک مثال شروع کنیم. فرض کنید یک ای پی ای داریم که میخواد چند تا عملیات محاسباتی رو انجام بده و نتیجه رو به ما برگردونه.  توی این سرویس ممکنه دیتا از دیتابیس خونده بشه و شاید هم توی دیتابیس نوشته بشه.

ما توی Unit Tests میایم و بخش های کوچیک منطقی (Backend Logic) کدمون رو تست میکنیم. مثلا توی این مثال اون توابعی که عملیات محاسبات رو انجام میدن رو تست میکنیم و باید دقت کنیم که این تست باید توی یک محیط ایزونه یا جداشده اتفاق بیفته... یعنی چی ؟ یعنی دیتای ورودی، لایه API، ارتباط با دیتابیس همشون باید فرض بشه که درست کار میکنن (و حتی رفتارشون رو جعل کنیم) تا بتونیم مطمئن بشیم دقیقا همین بخشی که تست میکنیم کار خودشو درست انجام میده!
(توی پرانتر بگم که به این جعل کردن، ماک کردن میگیم که بعدا حسابی باهاش کار داریم!)

پس توی Unit Tests ما تست میکنیم که توابع‌مون با یک سری ورودی مشخص، حتما یک سری خروجی مشخص و درست داشته باشن!

ولی توی Integration Tests میایم و چند بخش رو باهم تست میکنیم! مثلا لایه API و لاجیک رو باهم تست میکنیم، یا چند لاجیک رو همزمان تست میکنیم، یا توی تست هامون دیتابیس رو هم قاطی میکنیم!


</div>