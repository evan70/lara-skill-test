# Test základov Laravelu

Repozitár slúži na overenie znalostí základov Laravel 

Cieľom vytvorenia repozitára bolo pokryť základné časti Laravelu a naučiť sa prakticky ho pokrývať testami.

# Obsah podľa tém
1. [Migrácie](#task-migrations)
2. [Routovanie](#task-route)
3. [Blade šablóny](#task-blade)
4. [Eloquent model](#task-model)
5. [Validácia](#task-validation)
6. [Autentifikácia](#task-auth)

Pre začiatok je potrebné nasadiť projekt, na ktorom budú vykonávané testy.

# Inštalácia
- `composer install`
- `php artisan key:generate`
- .env s údajmi o databáze mysql
- VEĽMI DÔLEŽITÉ JE, ABY NÁZOV DATABÁZY BOL laravel_skill_test

# Požiadavky
- php >= 7.3
- mysql

# Overenie
- `php artisan test --filter MigrationsTest`
- `php artisan test --filter RouteTest`
- `php artisan test --filter BladeTest`
- `php artisan test --filter ModelTest`
- `php artisan test --filter ValidationTest`
- `php artisan test --filter AuthTest`
- `php artisan test`

# Inštrukcie
Úlohy môžete hľadať pomocou filtra TODO v IDE (ignorujte adresár /storage) alebo podľa zoznamu úloh.

# Potvrdenie vykonania testu
PR do vetvy master (automaticky spustí test overenia)

# Úlohy

## 1) Migrácie <a name="task-migrations"></a>
Všetky úlohy nájdete tu `database/migrations/tasks`
- Testy `tests/Feature/MigrationsTest.php`
- Spustenie `php artisan test --filter MigrationsTest`

---
#### Úloha 1: Nová tabuľka
Vytvorte v databáze tabuľku categories s 2 stĺpcami id a title (nezabudnite na timestamps)

---
#### Úloha 2: Nullable
Pre title nastavte predvolenú hodnotu NULL

---
#### Úloha 3: Hodnota predvolená
Pre active nastavte hodnotu predvolene TRUE

---
#### Úloha 4: Mäkké mazanie
Pridajte funkciu mäkkého mazania (soft delete)

---
#### Úloha 5: Časové pečiatky
Pridajte stĺpce s časovými pečiatkami (created_at, updated_at) pomocou jednej metódy

---
#### Úloha 6: Nové pole s určením poradia
Pridajte pole description typu text (DEFAULT NULL) aź po (AFTER) poli title

---
#### Úloha 7: Kontrola existencie poľa
Skontrolujte existenciu poľa active a v prípade úspechu pridajte pole main (boolean default false)

---
#### Úloha 8: Premenovanie poľa
Premenujte pole title na name

---
#### Úloha 9: Premenovanie tabuľky
Premenujte tabuľku posts na articles

---
#### Úloha 10: belongsToMany
Pridajte tabuľku pre vzťahy articles a categories (belongsToMany) s cudzími kľúčmi

---
## 2) Routovanie (Route) <a name="task-route"></a>
Všetky úlohy nájdete tu `routes/web.php` a `routes/api.php`
- Testy `tests/Feature/RouteTest.php`
- Spustenie `php artisan test --filter RouteTest`
---

#### Úloha 1: Zobraziť view
Pre GET URL /hello zobraziť view - /resources/views/hello.blade (bez controllera)

---
#### Úloha 2: Controller
Pre GET URL / odkázať na IndexController, metóda index

---
#### Úloha 3: Zobraziť view s názvom routy
Pre GET URL /page/contact zobraziť view - /resources/views/pages/contact.blade s názvom routy - contact
---
#### Úloha 4: Parametre
Pre GET URL /users/[id] odkázať sa na UserController -> metóda show bez Route Model Binding. Len parameter id
---
#### Úloha 5: Model Binding
Pre GET URL /users/bind/[user] odkázať sa na UserController -> metóda showBind, ale v tomto prípade použite Route Model Binding. Parameter user

---
#### Úloha 6: Presmerovanie
Vykonať presmerovanie z URL /bad na URL /good
---

#### Úloha 7: Resource kontrolér
Pridajte route pre resource kontrolér - UserCrudController s URL - /users_crud

---
#### Úloha 8: Skupina
Zorganizujte skupinu routes (Route::group()), ktoré sú zoskupené pod prefixom - dashboard

---
#### Úloha 9: Podskupina
Pridať route GET /admin -> Admin/IndexController -> index

---
#### Úloha 10: Podskupina
Pridať route POST /admin/post -> Admin/IndexController -> post

---
#### Úloha 11: Middleware
Zorganizovať skupinu routes (Route::group()), ktoré sú zoskupené pod prefixom - security a middleware auth

...

#### Задание 12: Middleware подзадачи
Добавить роут GET /admin/auth -> Admin/IndexController -> auth

---
#### Задание 13: ApiResource (routes/api.php)
Добавить apiResource контроллер - Api/V1/UserController
- Префикс урла должен быть /api/v1
- Полный урл /api/v1/users (не забывайте что это api routes)

## 3) Blade template <a name="task-blade"></a>
- Тесты `tests/Feature/BladeTest.php`
- Запуск `php artisan test --filter BladeTest`

---
#### Задание 1: Передать данные во view
`Http/Controllers/IndexController.php`
Передайте users во view (название ключа users)

---
#### Задание 2: Layout
`resources/views/table.blade.php`
Изменить реализацию этой view, расширить ее с использованием layout

---
#### Задание 3: Include
`resources/views/layouts/app.blade.php`
Подключите view с меню shared/menu.blade.php

---
#### Задание 4: Auth
`resources/views/auth.blade.php`
Сделать проверку авторизован пользователь или нет.
Если да то вывести ID пользователя.
ID пользователя вывести внутри конструкции с проверкой

---
#### Задание 5: Component
`resources/views/welcome.blade.php`
Сделать blade component с названием HelloWorld с содержимым во view - Текущая дата в формате Y-m-d.
- Обязательное условие добавить регистрацию компонента в AppServiceProvider и изменить его alias на hello
- В итоге alias - hello а класс компонента App\View\Components\HelloWorld
- Вывести его в указаном месте

---
#### Задание 6: Each
`resources/views/table.blade.php`
В эту view с контроллера передается collection c users в переменной data.
- Выполнить foreach loop в одну строку (специальная директива)
- Используйте view shared/user.blade.php для item (переменная user во item view)
- Используйте view shared/empty.blade.php для состояния когда нет элементов

---
#### Задание 7: ForEach
`resources/views/table.blade.php`
Здесь сделайте классический foreach loop
- Выведите div с $user->name
- Воспользуйтесь переменной $loop и у нечетных div выведите класс - `bg-red-500`

## 4) Eloquent Models <a name="task-model"></a>
- Тесты `tests/Feature/ModelTest.php`
- Запуск `php artisan test --filter ModelTest`

---
#### Задание 1: Таблица
`Models/Item.php`
Указать что таблица у модели - products

---
#### Задание 2: Basic query
`Http/Controllers/EloquentController.php`
С помощью модели Item реализовать запрос
- `select * from products where active = true order by created_at desc limit 3`

---
#### Задание 3: Scopes
`Http/Controllers/EloquentController.php`
Добавить в модель Item scope для фильтрации активных продуктов (scopeActive())

---
#### Задание 4: 404
`Http/Controllers/EloquentController.php`
Найти Item по id и передать во view либо отдать 404 страницу

---
#### Задание 5: Create
`Http/Controllers/EloquentController.php`
Выполнить простое добавление новой записи

---
#### Задание 6: Update
`Http/Controllers/EloquentController.php`
Выполнить простое обновление записи

---
#### Задание 7: Delete
`Http/Controllers/EloquentController.php`
Выполнить массовое удаление записей


## 5) Валидация <a name="task-validation"></a>
- Тесты `tests/Feature/ValidationTest.php`
- Запуск `php artisan test --filter ValidationTest`

---
#### Задание
`Http/Requests/ItemStoreRequest.php`
Добавить правила валидации для поля title
- Поле обязательно
- Строковое
- Минимам 5 символов
- Максимум 15 символов

## 6) Аутентификация <a name="task-auth"></a>
- Тесты `tests/Feature/AuthTest.php`
- Запуск `php artisan test --filter AuthTest`

---
#### Задание
`Policies/ItemPolicy.php`
Разрешить добавление продуктов только пользователю с id = 10

# Возникли сложности

Есть предложения? Возникли какие-либо проблемы? Не стестняйтесь и пишите GitHub Issues.

Желаю всем удачи!
