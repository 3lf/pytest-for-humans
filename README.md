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




</div>