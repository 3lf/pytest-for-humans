<div dir="rtl" align="center">

# تست نویسی در Pytest برای آدمیزاد !

</div>

<div dir="rtl" align="right">

Pytest معروف ترین و محبوب ترین کتابخونه تست نویسی پایتون هست که توی این صفحه میخوام با کمک گرفتن از چندین منبع به زبون آدمی زاد تست نویسی در Pytest رو پیش ببرم!


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
    assert response. status_code == 400
    assert json. loads (response. content) == {"name": ["This field is required."]}

```

</div>

<div dir="rtl" align="right">

اگه حتی از Pytest چیزی ندونید و فقط حداقل اطلاعاتی درمورد تست نویسی (و مفهوم assert) بدونید، مطمئنن این کد رو متوجه میشید!


## مفاهیم اولیه


Fixture 🔸 

Custom Marker 🔸 

Parametrize 🔸 

Skip 🔸 

Xfail 🔸 


</div>

