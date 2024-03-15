# Asp.Net Core Шпаргалка - [Скачать шпаргалку в PDF](https://1drv.ms/b/s!Ai0GNI50Q5GAgdQyt--UhfqF9G-M6w)

<div align="center">
<img src="http://codereform.com/wp-content/uploads/2018/03/aspnetcore-l.png" width=100%/>
</div>

<br>
<br>
<br>

# Содержание<br>

[Создание нового проекта](#Start-a-new-project)<br>
[Конфигурационные файлы](#Configuration-files)<br>
[Переменные окружения](#Environment-Variables)<br>
[Как получить доступ к данным конфигурации и переменным среды](#How-to-access-Config-data-and-Environmental-Variables)<br>
[Тег-хелперы](#Tag-Helpers)<br>
[Создание модели](#Create-a-Model)<br>
[Создание Razor Pages и EntityFramework](#Create-Razor-Pages-and-EntityFramework)<br>
[Внедрение зависимостей](#Dependency-Injection)<br>

## Создание нового проекта

| Задача      | CLI команда         | 
| ------------- |:-------------:| 
|Создать новое консольное приложение    | dotnet new webapp -o aspnetcoreapp |
|Запустить приложение    | cd aspnetcoreapp<br> dotnet run |
|Создать локальный сертификат    | dotnet dev-certs https --trust |

<br>

[вернуться к содержанию](#Index)<br>

<br>

## Конфигурационные файлы
<br>

### Разработка

<br>

1. Appsettings.json - Development ```Не приватный```
2. Manage User Secrets - Development ```Приватный```
<br>

[вернуться к содержанию](#Index)<br>

<br>

### Переменные окружения

<br>

1. проект => настройки проекта => Debug 
<br>

[вернуться к содержанию](#Index)<br>

<br>

## Как получить доступ к данным конфигурации и переменным среды

<br>
1. @inject Microsoft.Extensions.Cionfiguration.IConfiguration  configuration

2. Use @configuration["KEY"]
<br>

[вернуться к содержанию](#Index)<br>

<br>

## Тег-хелперы

<br>
1. Чтобы включить их добавьте 
```
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```
в _ViewImports.cshtml.
<br>

#### [Встроенные тег-хелперы](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/built-in/?view=aspnetcore-2.1)

<br>

[вернуться к содержанию](#Index)<br>

<br>

## Создание модели

1. В обозревателе решений щелкните правой кнопкой мыши проект RazorPagesMovie > Добавить > Новая папка. Назовите папку «Модели».

2. Щелкните правой кнопкой мыши папку «Модели». Выберите Добавить > Класс. Назовите класс Movie и замените содержимое класса Movie следующим кодом:


<br>

```c#

using System;
using System.ComponentModel.DataAnnotations.Schema;

namespace RazorPagesMovie.Models
{
    public class Movie
    {
        public int ID { get; set; }
        public string Title { get; set; }
        public DateTime ReleaseDate { get; set; }
        public string Genre { get; set; }
        public decimal Price { get; set; }
    }
}


```
<br>

[вернуться к содержанию](#Index)<br>

<br>

## Создание Razor Pages и EntityFramework

В обозревателе решений щелкните правой кнопкой мыши значок ```Pages folder > Add > New Folder.```
Назовите папку Movies

1. В обозревателе решений щелкните правой кнопкой мыши ```Pages/Movies folder > Add > New Scaffolded Item.```

2. В диалоговом окне "Добавить каркас", выберите "Razor Pages с использованием Entity Framework (CRUD) > Добавить".

3. Заполните диалоговое окно "Добавить Razor Pages с использованием Entity Framework (CRUD)":

> "В выпадающем списке класса модели выберите Movie (RazorPagesMovie.Models).
В строке класса данных контекста выберите знак "+" и примите сгенерированное имя RazorPagesMovie.Models.RazorPagesMovieContext.
Выберите Добавить".

Процесс создания каркаса создает и обновляет следующие файлы:

```
Создаваемые файлы
Pages/Movies: Создать, Удалить, Детали, Редактировать, Индекс.
Data/RazorPagesMovieContext.cs
```
<br>

[вернуться к содержанию](#Index)<br>

<br>

## Внедрение зависимостей

1. Инструмент создания каркаса автоматически создал контекст базы данных и зарегистрировал его в контейнере зависимостей. В файле ```Startup.ConfigureServices```

```c#
services.AddDbContext<RazorPagesMovieContext>(options =>
options.UseSqlServer(Configuration.GetConnectionString("RazorPagesMovieContext")));
```

Главная страница, которая координирует Entity framework, - это класс ```DbContext```

Здесь он называется RazorPagesMovieContext

Создано множество ```DbSet<Movie>```, которое соответствует таблице базы данных.

Строка подключения берется из ```DbContextOptions``` и считывается из файла конфигурации, например, ```appsettings.json```

<br>

[вернуться к содержанию](#Index)<br>

<br>
