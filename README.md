# 🦄 C# ASPNET Core 6 API CRUD JWT

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## TABLA DE CONTENIDO

* [Acerca del proyecto](#acerca-del-proyecto)
* [Instalación](#instalación)
* [Dependencias](#dependencias)
* [Licencia](#licencia)

## 🔥 ACERCA DEL PROYECTO

🦄 Este proyecto es una muestra de una solución CRUD base de una API con autenticación JWT. Se utilizo ``ASP.NET Core 6`` Web API.

## ✔️ CARACTERÍSTICAS

- [x] JWT Authentication
- [x] Authenticate User
- [x] Register User
- [x] Get All Users
- [x] Get User by ID
- [x] Update User
- [x] Delete User

## ⚙️ INSTALACIÓN

Clonar el repositorio.

```bash
gh repo clone FernandoCalmet/CS-ASPNET-Core-Minimal-API-CRUD
```

Crear migración de base de datos.

```bash
cd .\MinimalCRUDWebAPI
```

SQL Server EF Core Migrations (Windows Command): `RECOMENDADA`

```bash
set ASPNETCORE_ENVIRONMENT=Production
dotnet ef migrations add InitialCreate --context DataContext --output-dir Migrations/SqlServerMigrations
```

SQLite EF Core Migrations (Windows/MacOS): `ALTERNATIVA`

```bash
dotnet ef migrations add InitialCreate --context SqliteDataContext --output-dir Migrations/SqliteMigrations
```

SQL Server EF Core Migrations (Windows PowerShell): `ALTERNATIVA`
```bash
$env:ASPNETCORE_ENVIRONMENT="Production"
dotnet ef migrations add InitialCreate --context DataContext --output-dir Migrations/SqlServerMigrations
```

SQL Server EF Core Migrations (MacOS): `ALTERNATIVA`
```bash
ASPNETCORE_ENVIRONMENT=Production dotnet ef migrations add InitialCreate --context DataContext --output-dir Migrations/SqlServerMigrations
```

Migrar a base de datos

```bash
dotnet ef database update --context MinimalCRUDWebAPI.Helpers.DataContext
```

### OTROS COMANDOS

Instalar Herramienta DOTNET por la consola del administrador de paquetes.

```bash
dotnet tool install --global dotnet-ef
```

Verificar Herramienta DOTNET por la consola del administrador de paquetes.

```bash
dotnet ef
```

Crear migracion de base de datos

```bash
dotnet ef migrations add Initial
```

Migrar base de datos

```bash
dotnet ef database update
```

### EJECUTAR

Ejecutar aplicación por consola.

```bash
dotnet run
```

## 📥 DEPENDENCIAS

- [Swashbuckle.AspNetCore](https://www.nuget.org/packages/Swashbuckle.AspNetCore/) : Herramientas Swagger para documentar API creadas en ASP.NET Core.
- [Microsoft.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore/) : Entity Framework Core es un moderno mapeador de bases de datos de objetos para .NET. Admite consultas LINQ, seguimiento de cambios, actualizaciones y migraciones de esquemas. EF Core funciona con SQL Server, Azure SQL Database, SQLite, Azure Cosmos DB, MySQL, PostgreSQL y otras bases de datos a través de una API de complemento de proveedor.
- [Microsoft.EntityFrameworkCore.Design](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Design/) : Proveedor de base de datos de Microsoft SQL Server para Entity Framework Core.
- [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/) : Componentes de tiempo de diseño compartidos para las herramientas de Entity Framework Core.
- [Microsoft.EntityFrameworkCore.Sqlite ](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Sqlite /) : Proveedor de base de datos SQLite para Entity Framework Core.

## 📄 LICENCIA

Este proyecto está bajo la Licencia (Licencia MIT) - mire el archivo [LICENSE](LICENSE) para más detalles.

## ⭐️ DAME UNA ESTRELLA

Si esta Implementación le resultó útil o la utilizó en sus Proyectos, déle una estrella. ¡Gracias! O, si te sientes realmente generoso, [¡Apoye el proyecto con una pequeña contribución!](https://ko-fi.com/fernandocalmet).

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com