# Laravel Telescope --- README بالعربي

## 📌 ما هو Laravel Telescope؟

**Laravel Telescope** هو أداة Debugging وMonitoring مخصصة لتطبيقات
Laravel.

يعطيك Dashboard تستطيع من خلاله مشاهدة ما يحدث داخل التطبيق، مثل:

-   HTTP Requests
-   SQL Queries
-   Exceptions
-   Logs
-   Jobs
-   Events
-   Cache
-   Mail
-   Notifications
-   Authentication
-   Scheduled Tasks
-   Model Activity

بمعنى أبسط:

> Telescope يساعدك على معرفة ماذا يحدث **داخل Laravel** عندما ينفذ
> المستخدم عملية معينة.

مثلاً إذا ضغط المستخدم على:

``` text
Place Order
```

يمكنك استخدام Telescope لمعرفة:

``` text
Request
   ↓
Livewire Action
   ↓
SQL Queries
   ↓
Order Created
   ↓
Car Quantity Updated
```

------------------------------------------------------------------------

# 1. الفرق بين Telescope و Playwright

Telescope و Playwright ليسا بديلين عن بعضهما، لأن كل واحد منهما يعمل في
مستوى مختلف.

  الأداة              الوظيفة الأساسية
  ------------------- -----------------------------------------------
  Laravel Telescope   مراقبة وفحص ما يحدث **داخل Laravel**
  Playwright          اختبار التطبيق من منظور **المستخدم والمتصفح**
  PHPUnit / Pest      اختبار الـ Code والـ Business Logic

### مثال

لنفترض أن لدينا:

``` text
Login
 ↓
Product
 ↓
Add to Cart
 ↓
Checkout
 ↓
Place Order
```

### Playwright يستطيع فحص:

-   هل زر Login موجود؟
-   هل المستخدم يستطيع تسجيل الدخول؟
-   هل زر Add to Cart يعمل؟
-   هل المنتج ظهر في Cart؟
-   هل Checkout يعمل؟
-   هل رسالة نجاح الطلب ظهرت؟

### Telescope يستطيع فحص:

-   أي Request وصل إلى Laravel؟
-   ما هي SQL Queries التي تم تنفيذها؟
-   هل تم إنشاء Order؟
-   هل تم تحديث كمية المنتج؟
-   هل حصل Exception؟
-   كم استغرقت الـ Queries؟
-   ما الذي حدث داخل Livewire؟

### الخلاصة

``` text
Playwright
    =
ماذا يرى ويفعل USER؟

Telescope
    =
ماذا يحدث INSIDE Laravel؟

PHPUnit / Pest
    =
هل الـ CODE والـ LOGIC يعملان بشكل صحيح؟
```

------------------------------------------------------------------------

# 2. تثبيت Telescope

ثبت Telescope كـ development dependency:

``` bash
composer require laravel/telescope --dev
```

بعدها:

``` bash
php artisan telescope:install
```

ثم شغل الـ migrations:

``` bash
php artisan migrate
```

نظف الـ Laravel caches:

``` bash
php artisan optimize:clear
```

شغل المشروع:

``` bash
php artisan serve
```

ثم افتح:

``` text
http://127.0.0.1:8000/telescope
```

------------------------------------------------------------------------

# 3. التأكد أن Telescope مثبت

يمكنك التأكد من package:

``` bash
composer show laravel/telescope
```

مثلاً:

``` text
name    : laravel/telescope
version : v5.x
```

للتأكد من Routes:

``` bash
php artisan route:list | findstr telescope
```

------------------------------------------------------------------------

# 4. إذا `/telescope` أعطاك 404

إذا فتحت:

``` text
http://127.0.0.1:8000/telescope
```

وظهر:

``` text
404 Not Found
```

تحقق من:

``` bash
php artisan route:list | findstr telescope
```

إذا لم يظهر Route الخاص بـ Telescope، جرّب:

``` bash
php artisan optimize:clear
```

ثم:

``` bash
php artisan route:list | findstr telescope
```

وفي Laravel الذي يعتمد على تسجيل Providers من:

``` text
bootstrap/providers.php
```

تحقق من وجود:

``` php
Laravel\Telescope\TelescopeServiceProvider::class,
```

مثلاً:

``` php
<?php

return [
    App\Providers\AppServiceProvider::class,
    Laravel\Telescope\TelescopeServiceProvider::class,
];
```

ثم:

``` bash
php artisan optimize:clear
```

------------------------------------------------------------------------

# 5. ملف إعدادات Telescope

بعد التثبيت ستجد:

``` text
config/telescope.php
```

هذا الملف يحتوي على إعدادات Telescope.

من الإعدادات المهمة:

``` php
'path' => env('TELESCOPE_PATH', 'telescope'),
```

لذلك يكون Dashboard بشكل افتراضي على:

``` text
/telescope
```

------------------------------------------------------------------------

# 6. كيف يعمل Telescope؟

الصورة الذهنية البسيطة:

``` text
User
 │
 ▼
Browser
 │
 ▼
Laravel Route
 │
 ▼
Controller / Livewire
 │
 ├── Database Query
 ├── Job
 ├── Event
 ├── Cache
 └── Exception
 │
 ▼
Telescope
 │
 ▼
Telescope Dashboard
```

Telescope يقوم بتسجيل Activity معينة من داخل Laravel حتى تستطيع فحصها.

------------------------------------------------------------------------

# 7. Requests

قسم **Requests** يسمح لك بفحص HTTP Requests التي وصلت إلى Laravel.

يمكنك استخدامه لمعرفة أشياء مثل:

-   URL
-   HTTP Method
-   Status Code
-   Request Duration
-   Middleware
-   Request Data
-   Response Information

مثلاً:

``` text
POST /orders
```

يمكنك تتبع العملية:

``` text
POST /orders
      ↓
Controller
      ↓
Order::create()
      ↓
Database
```

إذا رجع Request بـ:

``` text
500
```

يمكنك الانتقال إلى Exception والـ Queries المرتبطة بالعملية لمعرفة
السبب.

------------------------------------------------------------------------

# 8. Telescope مع Livewire 4

Telescope مفيد جداً مع Livewire لأن Livewire ينفذ Server Requests عند
تنفيذ Actions.

مثلاً:

``` blade
<button wire:click="increment">
    +
</button>
```

عندما يضغط المستخدم:

``` text
Browser
   ↓
Livewire Request
   ↓
Livewire Component
   ↓
PHP Method
   ↓
Database
```

يمكنك استخدام Telescope لمعرفة ماذا حدث داخل الـ Request.

### مثال

``` php
public function increment()
{
    $this->quantity++;
}
```

إذا كان الـ Action ينفذ Query:

``` php
public function increment()
{
    $car = Car::find($this->carId);

    $this->quantity++;
}
```

يمكنك رؤية الـ SQL الناتج في:

``` text
Telescope → Queries
```

------------------------------------------------------------------------

# 9. SQL Queries

واحدة من أهم فوائد Telescope هي رؤية SQL Queries التي ينفذها Laravel.

اذهب إلى:

``` text
Telescope → Queries
```

يمكنك مشاهدة:

-   SQL Statement
-   Bindings
-   Execution Time
-   Database Connection
-   Request الذي تسبب في Query

مثلاً:

``` sql
select * from `orders`
where `id` = ?
limit 1
```

وقد تظهر الـ bindings:

``` text
[25]
```

وهذا يساعدك على معرفة ماذا أرسل Laravel فعلياً إلى قاعدة البيانات.

------------------------------------------------------------------------

# 10. اكتشاف مشكلة N+1

## ما هو N+1؟

N+1 تحدث عندما تقوم بتحميل مجموعة من البيانات، وبعد ذلك تجعل Laravel
ينفذ Query إضافية لكل عنصر للوصول إلى Relationship.

### مثال سيئ

``` php
$orders = Order::all();
```

وفي Blade:

``` blade
@foreach($orders as $order)
    {{ $order->customer->name }}
    {{ $order->car->name }}
@endforeach
```

إذا كان لديك 100 Order، قد تصبح العملية تقريباً:

``` text
1 Query   → Orders
100 Query → Customers
100 Query → Cars
```

أي:

``` text
201 Queries
```

------------------------------------------------------------------------

# 11. حل N+1 باستخدام Eager Loading

بدلاً من:

``` php
$orders = Order::all();
```

استخدم:

``` php
$orders = Order::with([
    'customer',
    'car',
])->get();
```

ومع Pagination:

``` php
$orders = Order::with([
    'customer',
    'car',
])->latest()->paginate(10);
```

بعدها افتح Telescope وشاهد:

``` text
Telescope → Queries
```

وقارن عدد الـ Queries قبل وبعد التعديل.

------------------------------------------------------------------------

# 12. طريقة عملية لاكتشاف N+1

إذا كنت تشك أن صفحة معينة تحتوي على N+1:

### الخطوة 1

افتح الصفحة.

مثلاً:

``` text
/admin/orders
```

### الخطوة 2

افتح:

``` text
/telescope
```

### الخطوة 3

اذهب إلى:

``` text
Queries
```

### الخطوة 4

ابحث عن Request الخاص بالصفحة.

### الخطوة 5

راقب الـ SQL Queries.

إذا رأيت شيئاً مثل:

``` sql
select * from customers where id = 1 limit 1
select * from customers where id = 2 limit 1
select * from customers where id = 3 limit 1
select * from customers where id = 4 limit 1
...
```

فهذا مؤشر قوي على وجود N+1.

### الخطوة 6

غيّر:

``` php
Order::all();
```

إلى:

``` php
Order::with('customer')->get();
```

أو:

``` php
Order::with(['customer', 'car'])->get();
```

### الخطوة 7

اعمل Refresh للصفحة.

### الخطوة 8

ارجع إلى Telescope وقارن عدد الـ Queries.

------------------------------------------------------------------------

# 13. Debugging للـ Exceptions

اذهب إلى:

``` text
Telescope → Exceptions
```

يمكن أن يساعدك في التحقيق في أخطاء مثل:

``` text
SQLSTATE
Call to a member function ...
Undefined variable ...
Method ... does not exist
BindingResolutionException
```

مثلاً:

``` php
$customer = auth()->user();

$customer->orders;
```

إذا لم يكن المستخدم Authenticated، قد يحدث Exception.

Telescope يساعدك في ربط الـ Exception بالـ Request الذي حدث أثناءه.

------------------------------------------------------------------------

# 14. Logs

يمكنك كتابة Logs داخل Laravel:

``` php
Log::info('Order created');
```

أو:

``` php
Log::error('Order creation failed');
```

مثال:

``` php
Log::info('Creating order', [
    'customer_id' => $customer->id,
    'car_id' => $car->id,
]);
```

بعد ذلك يمكنك فحص الـ Logs من Telescope.

⚠️ لا تقم بتسجيل:

-   Passwords
-   Tokens
-   Payment Secrets
-   API Keys
-   أي بيانات حساسة

------------------------------------------------------------------------

# 15. Debugging للـ Order Flow

في تطبيق E-commerce أو Car Rental، يمكن أن يكون Telescope مفيداً جداً.

مثلاً:

``` text
Login
 ↓
Product
 ↓
Add to Cart
 ↓
Cart
 ↓
Change Quantity
 ↓
Checkout
 ↓
Create Order
 ↓
Update Product Quantity
 ↓
Order يظهر في Profile
```

إذا حصل Bug، استخدم Telescope لفحص كل Server-side operation.

### مثال

المفروض عند إنشاء Order أن يحصل:

``` sql
INSERT INTO orders ...
```

وبعدها:

``` sql
UPDATE cars
SET quantity = quantity - 1
WHERE id = ...
```

إذا وجدت في Telescope:

``` text
INSERT INTO orders
```

لكن لم تجد:

``` text
UPDATE cars
```

فهذا يعني أن عملية تحديث السيارة لم يتم تنفيذها.

أما إذا كانت موجودة، فابدأ بفحص:

-   ID
-   Conditions
-   Transaction
-   Model Logic
-   Database Constraints

------------------------------------------------------------------------

# 16. Transactions + Telescope

في العمليات المهمة، يمكن استخدام Database Transaction:

``` php
DB::transaction(function () use ($car, $customer) {

    $order = Order::create([
        'customer_id' => $customer->id,
        'car_id' => $car->id,
        'quantity' => 1,
    ]);

    $car->decrement('quantity', 1);
});
```

Telescope يساعدك على رؤية الـ SQL Queries التي تم تنفيذها أثناء العملية.

لكن:

> Telescope لا يقوم بإدارة الـ Transaction ولا يصلح مشاكل الـ
> Transaction؛ هو فقط أداة لمراقبة ما يحدث.

------------------------------------------------------------------------

# 17. Jobs

إذا كان التطبيق يستخدم Queues:

``` php
ProcessOrder::dispatch($order);
```

يمكن أن يساعد Telescope في فحص الـ Jobs.

مثلاً:

``` text
Request
 ↓
Dispatch Job
 ↓
Queue
 ↓
Job Execution
```

إذا نجح الـ Request لكن حصل خطأ لاحقاً داخل الـ Job، Telescope يمكن أن
يساعدك في معرفة المشكلة.

------------------------------------------------------------------------

# 18. Cache

يمكن استخدام Telescope لمراقبة عمليات Cache.

مثلاً:

``` php
Cache::put('car:10', $car, 3600);
```

ثم:

``` php
Cache::get('car:10');
```

وهذا مفيد عند التحقيق في مشاكل مثل:

``` text
أنا عملت Cache
لكن لماذا Laravel لا يرجع البيانات من Cache؟
```

------------------------------------------------------------------------

# 19. Events

إذا كان التطبيق يستخدم Events:

``` php
event(new OrderCreated($order));
```

يمكنك استخدام Telescope لمراقبة الـ Events المرتبطة بالعملية.

وهذا مفيد عندما تكون العملية:

``` text
Order Created
      ↓
Event
      ↓
Listener
      ↓
Another Operation
```

إذا لم تحصل العملية الأخيرة، يمكنك التحقيق في الـ Event والـ Listener.

------------------------------------------------------------------------

# 20. Telescope Watchers

Telescope يعتمد على مفهوم اسمه **Watchers**.

الـ Watchers تحدد أنواع النشاط الذي سيتم تسجيله.

يمكن أن تشمل:

-   Requests
-   Queries
-   Models
-   Events
-   Jobs
-   Exceptions
-   Logs
-   Mail
-   Notifications
-   Cache
-   Dumps
-   Redis
-   Views
-   Commands
-   Schedule

الإعدادات موجودة في:

``` text
config/telescope.php
```

------------------------------------------------------------------------

# 21. Telescope والـ Performance

Telescope نفسه يحتاج إلى تسجيل وتخزين معلومات عن نشاط التطبيق، لذلك لديه
Overhead.

لهذا السبب يستخدم بشكل أساسي في:

``` text
Local Development
Debugging Environment
Testing / Staging
```

يجب التعامل معه بحذر في Production.

خصوصاً إذا كان التطبيق يستقبل عدد كبير من Requests.

------------------------------------------------------------------------

# 22. حماية Telescope

لا يفضل أن تجعل Telescope Dashboard متاحاً لأي شخص في Production.

يجب تقييد الوصول إليه حسب نظام Authentication وAuthorization الموجود في
مشروعك.

مثلاً يمكن أن يكون الوصول للمسؤولين فقط:

``` php
Gate::define('viewTelescope', function ($user) {
    return $user->is_admin;
});
```

الفكرة:

``` text
User
  ↓
Authenticated?
  ↓
Authorized?
  ↓
Yes → Telescope
No  → Access Denied
```

------------------------------------------------------------------------

# 23. أوامر Telescope المهمة

### تثبيت Telescope

``` bash
php artisan telescope:install
```

### تشغيل Migrations

``` bash
php artisan migrate
```

### تنظيف Cache

``` bash
php artisan optimize:clear
```

### معرفة package

``` bash
composer show laravel/telescope
```

### فحص Routes

``` bash
php artisan route:list | findstr telescope
```

### معرفة إصدار Laravel

``` bash
php artisan --version
```

------------------------------------------------------------------------

# 24. مشكلة `_debugbar/telescope/{id}`

إذا شغلت:

``` bash
php artisan route:list | findstr telescope
```

وظهر:

``` text
_debugbar/telescope/{id}
```

فلا تخلط بينه وبين:

``` text
/telescope
```

الـ:

``` text
_debugbar/telescope/{id}
```

تابع لـ **Laravel Debugbar**.

وليس هو Dashboard الخاص بـ Telescope.

------------------------------------------------------------------------

# 25. مشكلة `pdo_firebird`

قد يظهر أثناء تنفيذ أوامر PHP:

``` text
PHP Warning:
Unable to load dynamic library 'pdo_firebird'
```

هذا يعني أن PHP يحاول تحميل:

``` text
php_pdo_firebird.dll
```

لكن الـ DLL غير موجود.

هذه المشكلة **منفصلة عن Telescope**.

إذا كان مشروعك يستخدم MySQL ولا يستخدم Firebird، يمكن لاحقاً مراجعة
إعدادات:

``` text
php.ini
```

وتعطيل إعداد Firebird غير المطلوب.

------------------------------------------------------------------------

# 26. Workflow عملي لاكتشاف Bugs باستخدام Telescope

عندما تجد Bug:

``` text
1. Reproduce the Bug
        ↓
2. حدد العملية التي سببت المشكلة
        ↓
3. افتح Telescope
        ↓
4. افحص Requests
        ↓
5. افحص Exceptions
        ↓
6. افحص SQL Queries
        ↓
7. افحص Logs
        ↓
8. افحص Jobs / Events إذا كانت مستخدمة
        ↓
9. حدد Root Cause
        ↓
10. أصلح الكود
        ↓
11. أعد تنفيذ نفس السيناريو
        ↓
12. تحقق من Telescope
        ↓
13. أضف Automated Test
```

------------------------------------------------------------------------

# 27. Telescope + Playwright كـ QA Workflow

من أفضل الطرق استخدام الأدوات معاً:

``` text
                 ┌─────────────────┐
                 │   Playwright    │
                 │   E2E Testing   │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │    Laravel      │
                 │   Application   │
                 └────────┬────────┘
                          │
             ┌────────────┼────────────┐
             ▼            ▼            ▼
        ┌─────────┐  ┌─────────┐  ┌──────────┐
        │Telescope│  │ PHPUnit │  │  Logs    │
        │ Debug   │  │ / Pest  │  │          │
        └─────────┘  └─────────┘  └──────────┘
```

### Playwright يسأل:

> هل التطبيق يعمل بشكل صحيح من منظور المستخدم؟

### Telescope يسأل:

> ماذا حدث داخل Laravel؟

### PHPUnit / Pest يسأل:

> هل الـ Code والـ Business Logic يعملان كما هو متوقع؟

------------------------------------------------------------------------

# 28. مثال كامل: اكتشاف N+1

## قبل الإصلاح

``` php
public function render()
{
    $orders = Order::latest()->paginate(10);

    return view('orders', compact('orders'));
}
```

Blade:

``` blade
@foreach($orders as $order)
    <div>
        {{ $order->customer->name }}
        {{ $order->car->name }}
    </div>
@endforeach
```

اذهب إلى:

``` text
Telescope → Queries
```

وستبحث عن Queries المتكررة.

## بعد الإصلاح

``` php
public function render()
{
    $orders = Order::with([
        'customer',
        'car',
    ])->latest()->paginate(10);

    return view('orders', compact('orders'));
}
```

أعد تحميل الصفحة ثم راقب Telescope مرة أخرى.

الهدف هو تقليل الـ Queries غير الضرورية.

------------------------------------------------------------------------

# 29. مثال كامل: Debugging لـ Livewire

لدينا:

``` blade
<button wire:click="placeOrder">
    Place Order
</button>
```

وفي Component:

``` php
public function placeOrder()
{
    $order = Order::create([
        'customer_id' => auth()->id(),
        'car_id' => $this->carId,
        'quantity' => $this->quantity,
    ]);

    $this->car->decrement(
        'quantity',
        $this->quantity
    );
}
```

إذا ظهر للمستخدم أن الطلب تم إنشاؤه لكن كمية السيارة لم تتغير:

افتح:

``` text
Telescope
   ↓
Requests
   ↓
Livewire Request
   ↓
Queries
```

وابحث عن:

``` sql
INSERT INTO orders ...
```

ثم:

``` sql
UPDATE cars ...
```

إذا كان الـ INSERT موجوداً والـ UPDATE غير موجود:

``` text
المشكلة غالباً في execution path
```

إذا كان الاثنان موجودين:

``` text
ابدأ بفحص البيانات والـ conditions والـ transaction
```

------------------------------------------------------------------------

# 30. ماذا لا يفعل Telescope؟

Telescope ليس:

-   E2E Testing Framework
-   Browser Automation Tool
-   بديل عن Playwright
-   بديل عن PHPUnit / Pest
-   أداة لاكتشاف كل مشاكل Production
-   أداة Performance Profiling شاملة لكل شيء

وظيفته الأساسية:

> **مساعدتك على رؤية وفهم ما يحدث داخل Laravel أثناء تشغيل التطبيق.**

------------------------------------------------------------------------

# 31. Quick Reference

  ماذا تريد أن تفحص؟   Telescope
  -------------------- ---------------------------------
  HTTP Request         Requests
  Exceptions           Exceptions
  SQL                  Queries
  N+1                  Queries
  Logs                 Logs
  Jobs                 Jobs
  Events               Events
  Cache                Cache
  Mail                 Mail
  Notifications        Notifications
  Models               Models
  Livewire Requests    Requests + Queries + Exceptions

------------------------------------------------------------------------

# 32. الخلاصة

أسهل طريقة لحفظ Telescope:

``` text
┌──────────────────────────────┐
│         Playwright           │
│                              │
│ ماذا يرى ويفعل المستخدم؟    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│           Laravel            │
│                              │
│ Controllers / Livewire / DB  │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│         Telescope            │
│                              │
│ ماذا يحدث داخل Laravel؟     │
│                              │
│ Requests / SQL / Exceptions  │
│ Jobs / Events / Logs / Cache │
└──────────────────────────────┘
```

### احفظها بهذه الجملة:

> **Playwright يختبر التطبيق من الخارج، Telescope يراقب التطبيق من
> الداخل، وPHPUnit/Pest يختبر الـ Code والـ Logic.**

وهذا يجعل الثلاثة مكملين لبعضهم، وليسوا بدائل عن بعض.
