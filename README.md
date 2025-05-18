HAHA
Sorry shizofrenia


Снизу писала нейронка но похуй норм

Так ебать дорогие мои вот гайд

Копируете к себе на гитхаб или юзаете этот мне поебать

Клонируете этой командой

```
git clone https://github.com/hugexploit/demo.git
```

Либо пиздуете на гит и принудительно через браузер скачиваете кароче разберётесь.

Всё моя доброта заканичивается здесь. Помните какой я хороший хехе

Удачных голодных игр :)


**Гайд по развёртыванию и запуску проекта «Demo» из сниппета**

---

## 1. Импорт сниппета в Visual Studio

1. Откройте Visual Studio.
2. В меню выберите **Tools → Code Snippets Manager…** (или нажмите `Ctrl+K, Ctrl+B`).
3. В дереве слева выберите язык **Visual C#**.
4. Нажмите **Import**, укажите папку, где хранится ваш файл `DemoEx.snippet`.
5. Сниппет появится в списке; теперь вы можете вставлять его в код через **right‑click → Insert Snippet → My Code Snippets** или сочетанием `Ctrl+K, Ctrl+X`.

---

## 2. Создание нового WPF‑проекта

1. **File → New → Project…**
2. Выберите **WPF App (.NET Framework)**, нажмите **Next**.
3. Задайте имя проекта, например `Demo`, укажите папку и нажмите **Create**.

---

## 3. Подключение Npgsql

Через **Package Manager Console** выполните:

```powershell
Install-Package Npgsql
```

Это позволит работать с PostgreSQL из C#.

---

## 4. Добавление окон (Views)

В вашем проекте создайте **четыре** окна:

* **MainWindow\.xaml**
* **AdminWindow\.xaml**
* **CaptchaWindow\.xaml**
* **UserWindow\.xaml**

Для каждого окна:

1. **Add → Window (WPF)**.
2. Задайте то же имя, что и в сниппете (`MainWindow`, `AdminWindow` и т.д.).

---

## 5. Копирование кода из сниппета

1. Откройте **Code Snippets Manager** (как в п. 1).
2. Найдите ваш сниппет `DemoEx.snippet`.
3. В окне редактора кода встаньте в нужный файл (`MainWindow.xaml`), вставьте XAML-разметку сниппета через **Insert Snippet**.
4. Аналогично вставьте C#‑код ( `.xaml.cs` ) через **Insert Snippet** в файлы кода.

> **Важно:**
>
> * Проверьте, что везде стоит `namespace Demo`.
> * Классы и их имена должны совпадать с именами файлов.

---

## 6. Настройка базы данных

1. Запустите **pgAdmin** или **psql**.
2. Создайте/используйте базу `postgres`.
3. Выполните весь SQL‑скрипт из сниппета (создание таблиц, вставка тестовых данных).
4. Убедитесь, что в таблице **users** есть учётки:

   ```
   a.kuznetsov / admin123  
   t.morozova  / reg456  
   d.orlov     / guestpass1  
   m.semenova  / guestpass2
   ```

---

## 7. Конфигурация строки подключения

В файлах `MainWindow.xaml.cs` и `AdminWindow.xaml.cs` найдите константы:

```csharp
private const string ConnStr = "Host=localhost;Port=5432;Database=postgres;Username=postgres;Password=postgres;";
private const string ConnectionString = "Host=localhost;Port=5432;Database=postgres;Username=postgres;Password=postgres;";
```

При необходимости замените `Username`, `Password`, `Host`, `Database` на ваши.

---

## 8. Сборка и запуск

1. **Build → Build Solution** (или `Ctrl+Shift+B`).
2. **Debug → Start Debugging** (или `F5`).
3. На экране появится **MainWindow** (логин/пароль + капча).
4. Введите учётные данные, пройдите капчу:

   * После трёх неудачных попыток аккаунт блокируется.
5. В зависимости от роли вы попадёте в **AdminWindow** (для админа/регистратора) или **UserWindow** (для гостя).

---

### 9. Как менять тестовые данные

* **Через SQL** в pgAdmin/psql:

  ```sql
  -- Изменить пароль
  UPDATE users SET password='newpass' WHERE login='a.kuznetsov';

  -- Добавить пользователя
  INSERT INTO users (surname,name,otchestvo,role_id,login,password)
    VALUES ('Иванов','Иван','Иванович',3,'i.ivanov','guest123');
  ```
* **Через UI** (`AdminWindow`):

  1. Добавить нового: заполнить поля и нажать **Добавить**.
  2. Редактировать: дважды кликнуть в таблице, изменить, затем **Сохранить изменения**.
  3. Удалить: выбрать строку и нажать **Удалить**, затем **Сохранить изменения**.

