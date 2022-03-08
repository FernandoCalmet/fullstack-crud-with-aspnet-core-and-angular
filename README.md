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

## 📓 RESUMEN TEÓRICO

### Permitir atributo anónimo .NET

Ruta: `/Authorization/AllowAnonymousAttribute.cs`  
El atributo `[AllowAnonymous]` personalizado se usa para permitir el acceso anónimo a métodos de acción específicos de controladores que están decorados con el atributo `[Authorize]`. Se utiliza en el controlador de usuarios para permitir el acceso anónimo a los métodos de acción de registro e inicio de sesión. El atributo de autorización personalizado a continuación omite la autorización si el método de acción está decorado con `[AllowAnonymous]`.

Creé un permiso anónimo personalizado (en lugar de usar el integrado) para mantener la coherencia y evitar errores de referencia ambiguos entre espacios de nombres.

### Atributo de autorización personalizado de .NET

Ruta: `/Authorization/AuthorizeAttribute.cs`  
El atributo `[Authorize]` personalizado se usa para restringir el acceso a controladores o métodos de acción específicos. Solo las solicitudes autorizadas pueden acceder a los métodos de acción que están decorados con el atributo `[Authorize]`.

Cuando un controlador está decorado con el atributo `[Authorize]`, todos los métodos de acción están restringidos a solicitudes autorizadas, excepto los métodos decorados con el atributo `[AllowAnonymous]` personalizado anterior.

La autorización se realiza mediante el OnAuthorizationmétodo que verifica si hay un usuario autenticado adjunto a la solicitud actual ( context.HttpContext.Items["User"]). El middleware jwt personalizado adjunta un usuario autenticado si la solicitud contiene un token de acceso JWT válido.

### Middleware de JWT personalizado de .NET

Ruta: `/Authorization/JwtMiddleware.cs`  
El middleware JWT personalizado extrae el token JWT del Authorizationencabezado de la solicitud (si lo hay) y lo valida con el jwtUtils.ValidateToken()método. Si la validación es exitosa, se devuelve la identificación de usuario del token y el objeto de usuario autenticado se adjunta a la HttpContext.Itemscolección para que sea accesible dentro del alcance de la solicitud actual.

Si la validación del token falla o no hay ningún token, la solicitud es anónima y solo se le permite acceder a las rutas públicas porque no hay un objeto de usuario autenticado adjunto al contexto HTTP. La lógica de autorización que comprueba que el objeto de usuario está adjunto se encuentra en el atributo de autorización personalizado . Si se envía una solicitud anónima a una ruta segura, 401 Unauthorizedel atributo de autorización devuelve una respuesta.

### Utilidades de .NET JWT

Ruta: `/Authorization/JwtUtils.cs`  
La clase utils de JWT contiene métodos para generar y validar tokens de JWT.

El método `GenerateToken()` genera un token JWT con la identificación del `user` especificado como "id" de reclamo, lo que significa que la carga útil del token contendrá la propiedad `"id"`: <userId>(p. ej "id": 1., ).

El ValidateToken()método intenta validar el token JWT proporcionado y devolver la identificación de usuario (`"id"`) de las notificaciones del token. Si la validación falla, se devuelve nulo.

### Controlador de usuarios de .NET

Ruta: `/Controllers/UsersController.cs`  
El controlador de usuarios de .NET define y maneja todas las rutas/puntos finales para la API que se relacionan con los usuarios, esto incluye autenticación, registro y operaciones CRUD estándar. Dentro de cada ruta, el controlador llama al servicio de usuario para realizar la acción requerida, lo que mantiene al controlador "esbelto" y completamente separado de la base de datos/código de persistencia.

Los métodos de acción del controlador son seguros de forma predeterminada con el atributo `[Authorize]` personalizado en la clase, los métodos Authenticatey Registerpermiten el acceso público anulando el atributo `[Authorize]` en el controlador con un atributo `[AllowAnonymous]` en cada método de acción. Elegí este enfoque por seguridad para evitar que una ruta se haga pública accidentalmente, cualquier método de acción nuevo será seguro de forma predeterminada a menos que se haga público explícitamente.

### Entidad de usuario de .NET

Ruta: `/Entidades/Usuario.cs`  
La clase de entidad de usuario representa los datos almacenados en la base de datos para los usuarios.

Las clases de entidad también se usan para pasar datos entre diferentes partes de la aplicación (p. ej., entre servicios y controladores) y se pueden usar para devolver datos de respuesta http desde los métodos de acción del controlador.

El atributo `[JsonIgnore]` evita que la propiedad `PasswordHash` se serialice y se devuelva en las respuestas de API.

### Excepción de aplicación personalizada de .NET

Ruta: `/Helpers/AppException.cs`  
La excepción de aplicación es una clase de excepción personalizada que se usa para diferenciar entre excepciones controladas y no controladas en la API de .NET. Las excepciones controladas son generadas por el código de la aplicación y se utilizan para devolver mensajes de error amigables, por ejemplo, excepciones de validación o lógica de negocios causadas por parámetros de solicitud no válidos, mientras que las excepciones no controladas son generadas por el marco .NET o causadas por errores en el código de la aplicación.

Las excepciones son manejadas en el ejemplo por el middleware del controlador de errores global , y algunas excepciones de aplicaciones son lanzadas por el servicio de usuario cuando falla la validación.

### Configuración de la aplicación .NET

Ruta: `/Helpers/AppSettings.cs`  
La clase de configuración de la aplicación contiene propiedades definidas en el archivo appsettings.json y se usa para acceder a la configuración de la aplicación a través de objetos que se inyectan en clases mediante el sistema de inyección de dependencia (DI) de .NET 6.0. Por ejemplo, el `controlador de usuarios` accede a la configuración de la aplicación a través de un objeto `IOptions<AppSettings> appSettings` que se inyecta en su constructor.

### Perfil de .NET AutoMapper

Ruta: `/Helpers/AutoMapperProfile.cs`  
El perfil de automapper contiene la configuración de mapeo utilizada por la aplicación, AutoMapper es un paquete disponible en Nuget que permite el mapeo automático de un tipo de clase a otro. En este ejemplo, lo estamos usando para mapear entre la entidad `User` y algunos tipos de modelos diferentes: `AuthenticateResponse`, `RegisterRequesty` y `UpdateRequest`.

Todos los perfiles de automapper en el proyecto se ejecutan al inicio con una llamada `services.AddAutoMapper(typeof(Program))` en el archivo de programa .NET . El parámetro de tipo `typeof(Program)` le dice a automapper que busque todos los perfiles de automapper en el ensamblaje del proyecto actual, cualquier tipo en el proyecto podría usarse ya que es simplemente un tipo de marcador para el ensamblaje.

### Contexto de datos .NET

Ruta: `/Helpers/DataContext.cs`  
El contexto de datos se usa para acceder a los datos de la aplicación a través de Entity Framework Core y está configurado para conectarse a una base de datos de SQL Server. Se deriva de la clase EF Core `DbContext` y tiene una propiedad `Users` pública para acceder y administrar datos de usuario. El contexto de datos es utilizado por el `servicio de usuario` para manejar todas las operaciones de datos de bajo nivel.

En entornos de desarrollo, la API está configurada para usar el `contexto de datos SQLite` que hereda `DataContexty` anula el proveedor de base de datos para conectarse a una base de datos SQLite local en lugar de SQL Server.

### Middleware del controlador de errores globales .NET

Ruta: `/Helpers/ErrorHandlerMiddleware.cs`  
El controlador de errores global se utiliza para capturar todos los errores y eliminar la necesidad de duplicar el código de manejo de errores en toda la API de .NET 6. Está configurado como middleware en el archivo `Program.cs`.

Los errores de tipo `AppExceptionse` tratan como errores personalizados (específicos de la aplicación) que devuelven una respuesta `400 Bad Request`, la clase integrada de .NET `KeyNotFoundExceptionse` usa para devolver respuestas `404 Not Found`, todas las demás excepciones no se controlan y devuelven una respuesta `500 Internal Server Error`.

Consulte el servicio de atención al usuario para ver ejemplos de errores personalizados y errores no encontrados generados por la API.

### Contexto de datos SQLite de .NET

Ruta: `/Helpers/SqliteDataContext.cs`  
La API utiliza el contexto de datos de SQLite en entornos de desarrollo, se hereda del `contexto de datos` principal y reemplaza al proveedor para usar SQLite en lugar de SQL Server.

### Migraciones de EF Core SQLite

Ruta: `/Migrations/SqliteMigraciones`  
Migraciones de Entity Framework Core para el proveedor de base de datos SQLite utilizado en entornos de desarrollo.

Las migraciones de este ejemplo se generaron con el comando `dotnet ef migrations add InitialCreate --context SqliteDataContext --output-dir Migrations/SqliteMigrations`.

Las migraciones se generan para SQLite porque la clase `SqliteDataContext` está configurada para conectarse a una base de datos SQLite. `SqliteDataContext` Hereda de la clase principal y `DataContext` reemplaza al proveedor para usar SQLite en lugar de SQL Server. Esto permite que el proyecto admita múltiples proveedores de bases de datos diferentes para diferentes entornos.

Para instalar las herramientas de EF Core para la CLI de .NET, ejecute globalmente `dotnet tool install -g dotnet-ef`, o para actualizar, ejecute `dotnet tool update -g dotnet-ef`.

### Migraciones de EF Core SQL Server

Ruta: `/Migrations/SqlServerMigrations`  
Migraciones de Entity Framework Core para el proveedor de base de datos de SQL Server utilizado en entornos de producción.

Las migraciones en este ejemplo se generaron con el siguiente comando.

Comando de Windows: Windows PowerShell: MacOS:
`set ASPNETCORE_ENVIRONMENT=Production`
`dotnet ef migrations add InitialCreate --context DataContext --output-dir Migrations/SqlServerMigrations`

`$env:ASPNETCORE_ENVIRONMENT="Production"`
`dotnet ef migrations add InitialCreate --context DataContext --output-dir Migrations/SqlServerMigrations`

`ASPNETCORE_ENVIRONMENT=Production dotnet ef migrations add InitialCreate --context DataContext --output-dir Migrations/SqlServerMigrations`

La variable de entorno `ASPNETCORE_ENVIRONMENT` debe establecerse en `Production` para que la clase de SQL Server `DataContext` se configure con el sistema de inserción de dependencias de .NET; consulte el código de configuración del contexto de datos en el archivo `del programa de .NET`.

Para instalar las herramientas de EF Core para la CLI de .NET, ejecute globalmente `dotnet tool install -g dotnet-ef`, o para actualizar, ejecute `dotnet tool update -g dotnet-ef`.

### Modelo de solicitud de autenticación de .NET

Ruta: `/Models/Users/AuthenticateRequest.cs`  
El modelo de solicitud de autenticación define los parámetros para las solicitudes POST entrantes a la ruta `/users/authenticate`, se adjunta a la ruta configurándolo como el parámetro del método `Authenticate` de acción del controlador de usuarios . Cuando la ruta recibe una solicitud HTTP POST, los datos del cuerpo se vinculan a una instancia de la clase `AuthenticateRequest`, se validan y se pasan al método.

Las anotaciones de datos .NET se utilizan para manejar automáticamente la validación del modelo, el atributo `[Required]` establece el nombre de usuario y la contraseña como campos obligatorios, por lo que si falta alguno, la API devuelve un mensaje de error de validación.

### Modelo de respuesta de autenticación de .NET

Ruta: `/Models/Users/AuthenticateResponse.cs`  
El modelo de respuesta de autenticación define los datos devueltos por el método `Authenticate` del `controlador de usuarios`. Incluye detalles básicos de usuario y un `token JWT`.

### Modelo de solicitud de registro

Ruta: `/Models/Users/RegisterRequest.cs`  
El modelo de solicitud de registro define los parámetros para las solicitudes POST entrantes a la ruta `/users/register`, se adjunta a la ruta al configurarlo como parámetro para el Registermétodo de acción del `controlador de usuarios`. Cuando la ruta recibe una solicitud HTTP POST, los datos del cuerpo se vinculan a una instancia de la clase `RegisterRequest`, se validan y se pasan al método.

Las anotaciones de datos .NET se utilizan para manejar automáticamente la validación del modelo, el atributo `[Required]` establece todos los campos como obligatorios, de modo que si falta alguno, la API devuelve un mensaje de error de validación.

### Modelo de solicitud de actualización

Ruta: `/Models/Users/UpdateRequest.cs`  
El modelo de solicitud de actualización define los parámetros para las solicitudes PUT entrantes a la ruta `/users/{id}`, se adjunta a la ruta al configurarlo como el parámetro del Updatemétodo de acción del controlador de usuarios . Cuando la ruta recibe una solicitud HTTP PUT, los datos del cuerpo se vinculan a una instancia de la clase `UpdateRequest`, se validan y se pasan al método.

Ninguna de las propiedades tiene el atributo `[Required]`, por lo que todas son opcionales. Los campos omitidos se ignoran cuando se actualiza un usuario, la configuración para esto se encuentra en el mapeo `UpdateRequest -> User`  del `perfil del automapeador`.

### Configuración de lanzamiento de .NET.json

Ruta: `/Properties/launchSettings.json`  
Archivo de configuración que contiene configuraciones y perfiles de inicio utilizados al iniciar la aplicación en su máquina local. El primer perfil del archivo ( Desarrollo ) se usa de forma predeterminada al iniciar la aplicación con `dotnet run`, el archivo puede contener varios perfiles y se puede especificar un perfil de inicio diferente con el argumento de la línea de comandos `--launch-profile "PROFILE_NAME"`.

El archivo launchSettings.json no se implementa, solo se usa en su máquina de desarrollo local. Para obtener más información, consulte https://docs.microsoft.com/aspnet/core/fundamentals/environments?view=aspnetcore-6.0#lsj .

### Servicio de usuario .NET

Ruta: `/Services/UserService.cs`  
El servicio de usuario es responsable de toda la interacción de la base de datos y la lógica comercial central relacionada con el inicio de sesión, el registro y las operaciones CRUD del usuario.

La parte superior del archivo contiene una interfaz que define el servicio de usuario, justo debajo está la clase de servicio de usuario concreta que implementa la interfaz. BCrypt se utiliza para codificar y verificar contraseñas; para obtener más información, consulte .NET 6.0 - `Hash` y `verificación de contraseñas` con `BCrypt`.

### Configuración de la aplicación .NET 6 (Desarrollo)

Ruta: `/appsettings.Development.json`  
Archivo de configuración con ajustes de la aplicación que son específicos del entorno de desarrollo, incluye la cadena de conexión `WebApiDatabase` para la base de datos de desarrollo de SQLite local que anula la cadena de conexión en el archivo base `appsettings.json`.

### Configuración de la aplicación .NET 6

Ruta: `/appsettings.json`  
Archivo de configuración base que contiene la configuración predeterminada de la aplicación para todos los entornos (a menos que se anule en la configuración específica del entorno). Incluye marcador de posición para su cadena de conexión de SQL Server de producción.

IMPORTANTE: `"Secret"` la API utiliza la propiedad para firmar y verificar los tokens JWT para la autenticación, actualícela con su propia cadena aleatoria para asegurarse de que nadie más pueda generar un JWT para obtener acceso no autorizado a su aplicación. Una forma rápida y fácil es unir un par de GUID para crear una cadena aleatoria larga (por ejemplo, de https://www.guidgenerator.com/ ).

### Configuración OmniSharp

Ruta: `/omnisharp.json`  
Este archivo contiene opciones de configuración para la extensión de C# en VS Code. La opción `useBundledOnly` le dice a la extensión de C# que use la versión integrada de MSBuild en lugar de la versión global para evitar errores si tiene una versión anterior de MSBuild instalada globalmente (por ejemplo, como parte de Visual Studio).

### Programa .NET 6

Ruta: `/Programa.cs`  
El archivo de programa .NET 6 contiene declaraciones de nivel superior que el nuevo compilador C# 10 convierte en un método `Main()`  y una Programclase para el programa .NET. El método `Main()` es el punto de entrada para una aplicación .NET, cuando se inicia una aplicación busca el método `Main()` para comenzar la ejecución. Las declaraciones de nivel superior se pueden ubicar en cualquier parte del proyecto, pero generalmente se colocan en el archivo `Program.cs`; solo un archivo puede contener declaraciones de nivel superior dentro de una aplicación .NET.

La clase `WebApplication` maneja el inicio de la aplicación, la administración de por vida, la configuración del servidor web y más. `WebApplicationBuilder` se crea primero llamando al método estático `WebApplication.CreateBuilder(args)`, el constructor se usa para configurar servicios para inyección de dependencia (DI), `WebApplicationse` crea una instancia llamando `builder.Build()`, la instancia de la aplicación se usa para configurar la canalización de solicitud HTTP (middleware), luego la aplicación es empezó llamando `app.Run()`.

Envolví las secciones agregar servicios... y configurar HTTP... entre corchetes `{}` para agruparlos visualmente, los corchetes son completamente opcionales.

Internamente, la clase `WebApplicationBuilder` llama al método `ConfigureWebHostDefaults()` de extensión que configura el alojamiento para la aplicación web, incluida la configuración de Kestrel como servidor web, la adición de middleware de filtrado de host y la habilitación de la integración de IIS. Para obtener más información sobre la configuración predeterminada del generador, consulte https://docs.microsoft.com/aspnet/core/fundamentals/host/generic-host#default-builder-settings .

### .NET 6 API web csproj

Ruta: `/WebApi.csproj`  
El csproj (proyecto C#) es un archivo basado en MSBuild que contiene el marco de destino y la información de dependencia del paquete NuGet para la aplicación. La función `ImplicitUsings` está habilitada, lo que le dice al compilador que genere automáticamente un conjunto de directivas de uso globales basadas en el tipo de proyecto, lo que elimina la necesidad de incluir muchas declaraciones de uso comunes. Las instrucciones de uso globales se generan automáticamente cuando crea el proyecto y se pueden encontrar en el archivo `/obj/Debug/net6.0/WebApi.GlobalUsings.g.cs`.

Para obtener más información sobre el archivo de proyecto de C#, consulte .NET + MSBuild - Archivo de proyecto de C# (.csproj) en pocas palabras .

## 📥 DEPENDENCIAS

- [Swashbuckle.AspNetCore](https://www.nuget.org/packages/Swashbuckle.AspNetCore/) : Herramientas Swagger para documentar API creadas en ASP.NET Core.
- [Microsoft.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore/) : Entity Framework Core es un moderno mapeador de bases de datos de objetos para .NET. Admite consultas LINQ, seguimiento de cambios, actualizaciones y migraciones de esquemas. EF Core funciona con SQL Server, Azure SQL Database, SQLite, Azure Cosmos DB, MySQL, PostgreSQL y otras bases de datos a través de una API de complemento de proveedor.
- [Microsoft.EntityFrameworkCore.Design](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Design/) : Proveedor de base de datos de Microsoft SQL Server para Entity Framework Core.
- [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/) : Componentes de tiempo de diseño compartidos para las herramientas de Entity Framework Core.
- [Microsoft.EntityFrameworkCore.Sqlite](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Sqlite/) : Proveedor de base de datos SQLite para Entity Framework Core.
- [Microsoft.AspNetCore.Authentication.JwtBearer](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.JwtBearer/) : Middleware ASP.NET Core que permite que una aplicación reciba un token de portador de OpenID Connect.
- [AutoMapper](https://www.nuget.org/packages/AutoMapper/) : AutoMapper es una pequeña biblioteca simple creada para resolver un problema aparentemente complejo: deshacerse del código que mapeó un objeto a otro. Este tipo de código es bastante triste y aburrido de escribir, entonces, ¿por qué no inventar una herramienta que lo haga por nosotros?
- [AutoMapper.Extensions.Microsoft.DependencyInjection](https://www.nuget.org/packages/AutoMapper.Extensions.Microsoft.DependencyInjection/) : Extensiónes para AutoMapper ASP.NET Core.
- [BCrypt.Net-Next](https://www.nuget.org/packages/BCrypt.Net-Next/) : Segmentación de NET 6.
- [System.IdentityModel.Tokens.Jwt](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/) : Incluye tipos que brindan soporte para crear, serializar y validar tokens web JSON.

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