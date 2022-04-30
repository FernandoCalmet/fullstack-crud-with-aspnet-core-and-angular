# 🦄 C# ASPNET Core 6 API CRUD JWT

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## TABLA DE CONTENIDO

* [Acerca del proyecto](#acerca-del-proyecto)
* [Instalación](#instalación)
* [Resumen Teórico](#resumen-teórico)
  * [Permitir atributo anónimo .NET](#permitir-atributo-an%C3%B3nimo-net)
  * [Atributo de autorización personalizado de .NET](#atributo-de-autorizaci%C3%B3n-personalizado-de-net)
  * [Middleware de JWT personalizado de .NET](#middleware-de-jwt-personalizado-de-net)
  * [Utilidades de .NET JWT](#utilidades-de-net-jwt)
  * [Controlador de usuarios de .NET](#controlador-de-usuarios-de-net)
  * [Entidad de usuario de .NET](#entidad-de-usuario-de-net)
  * [Excepción de aplicación personalizada de .NET](#excepci%C3%B3n-de-aplicaci%C3%B3n-personalizada-de-net)
  * [Configuración de la aplicación .NET](#configuraci%C3%B3n-de-la-aplicaci%C3%B3n-net)
  * [Perfil de .NET AutoMapper](#perfil-de-net-automapper)
  * [Contexto de datos .NET](#contexto-de-datos-net)
  * [Middleware del controlador de errores globales .NET](#middleware-del-controlador-de-errores-globales-net)
  * [Contexto de datos SQLite de .NET](#contexto-de-datos-sqlite-de-net)
  * [Migraciones de EF Core SQLite](#migraciones-de-ef-core-sqlite)
  * [Migraciones de EF Core SQL Server](#migraciones-de-ef-core-sql-server)
  * [Modelo de solicitud de autenticación de .NET](#modelo-de-solicitud-de-autenticaci%C3%B3n-de-net)
  * [Modelo de respuesta de autenticación de .NET](#modelo-de-respuesta-de-autenticaci%C3%B3n-de-net)
  * [Modelo de solicitud de registro](#modelo-de-solicitud-de-registro)
  * [Modelo de solicitud de actualización](#modelo-de-solicitud-de-actualizaci%C3%B3n)
  * [Configuración de lanzamiento de .NET.json](#configuraci%C3%B3n-de-lanzamiento-de-netjson)
  * [Servicio de usuario .NET](#servicio-de-usuario-net)
  * [Configuración de la aplicación .NET 6 (Desarrollo)](#configuraci%C3%B3n-de-la-aplicaci%C3%B3n-net-6-desarrollo)
  * [Configuración de la aplicación .NET 6](#configuraci%C3%B3n-de-la-aplicaci%C3%B3n-net-6)
  * [Configuración OmniSharp](#configuraci%C3%B3n-omnisharp)
  * [Programa .NET 6](#programa-net-6)
  * [.NET 6 API web csproj](#net-6-api-web-csproj)
* [Despliegue en Azure](#despliegue-en-azure)
  * [Crear un nuevo servidor de Windows en Microsoft Azure](#crear-un-nuevo-servidor-de-windows-en-microsoft-azure)
  * [Conectarse a la instancia de Azure Windows Server a través de RDP](#conectarse-a-la-instancia-de-azure-windows-server-a-trav%C3%A9s-de-rdp)
  * [Configuración del servidor web con IIS (Servicios de información de Internet)](#configuraci%C3%B3n-del-servidor-web-con-iis-servicios-de-informaci%C3%B3n-de-internet)
  * [Crear base de datos Azure SQL](#crear-base-de-datos-azure-sql)
  * [Crear e implementar la API back-end de ASP.NET Core en Azure](#crear-e-implementar-la-api-back-end-de-aspnet-core-en-azure)
  * [Crear e implementar la aplicación front-end de Angular en Azure](#crear-e-implementar-la-aplicaci%C3%B3n-front-end-de-angular-en-azure)
  * [Configurar IIS para servir el front-end de Angular y la API de ASP.NET Core](#configurar-iis-para-servir-el-front-end-de-angular-y-la-api-de-aspnet-core)
  * [Prueba de la aplicación Angular + ASP.NET Core + SQL Server ejecutándose en Azure](#prueba-de-la-aplicaci%C3%B3n-angular--aspnet-core--sql-server-ejecut%C3%A1ndose-en-azure)
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
gh repo clone FernandoCalmet/dotnet-6-aspnet-core-api-jwt-crud
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

## DESPLIEGUE EN AZURE

### Crear un nuevo servidor de Windows en Microsoft Azure

Antes de hacer nada, necesitamos un servidor en el que podamos trabajar, siga estos pasos para activar una nueva instancia de Windows Server 2019 utilizando el servicio Azure Virtual Machines.

1. Inicie sesión en Azure Portal en https://portal.azure.com/ . Si aún no tiene una cuenta de Azure, puede crear una gratuita en https://azure.microsoft.com/free .

2. Vaya a la sección de servicio de Máquinas Virtuales.

3. Haga clic en "Agregar" para crear una nueva máquina virtual.

4. Lo esencial
- **Grupo de recursos** : haga clic en "Crear nuevo" e ingrese un nombre para el grupo de recursos (por ejemplo, mi grupo de recursos).
- **Nombre de la máquina virtual** : ingrese un nombre para la máquina virtual (por ejemplo, mi servidor).
- **Imagen** : seleccione "Windows Server 2019 Datacenter".
- **Tamaño** : haga clic en "Cambiar tamaño", seleccione "B1ms" y haga clic en el botón "Seleccionar". Esta máquina virtual tiene 2 GB de RAM, que es aproximadamente el mínimo que desea ejecutar para Windows Server.
- **Nombre de usuario** : ingrese el nombre de usuario del administrador para el servidor.
- **Contraseña** : ingrese la contraseña de administrador para el servidor.
- **Confirmar contraseña** : vuelva a ingresar la contraseña de administrador para el servidor.
- **Seleccione los puertos entrantes** : permita el tráfico "HTTP (80)" y "RDP (3389)" a través del servidor.

5. **Gestión** : establezca la supervisión de diagnósticos de arranque en "Desactivado".

6. **Revisar + crear** : haz clic en "Crear".

### Conectarse a la instancia de Azure Windows Server a través de RDP

Una vez que la VM de Azure Windows Server esté lista, puede conectarse a ella a través de RDP (Protocolo de escritorio remoto). Si está en Windows, debe tener un cliente RDP instalado de forma predeterminada, si está en Mac OSX, puede instalar un cliente RDP desde la tienda de aplicaciones aquí .

1. Cuando finalice la implementación, haga clic en "Ir al recurso" para acceder a la página de descripción general de la máquina virtual de Azure.

2. En la página de descripción general de Azure Virtual Machine, haga clic en "Conectar".

3. Haga clic en "Descargar archivo RDP".

4. Abra el archivo RDP descargado. Si ve un mensaje que indica que no se puede identificar al editor, haga clic en "Conectar".

5. Ingrese el nombre de usuario y la contraseña del paso anterior y haga clic en "Aceptar". Si ve un mensaje que indica que no se puede identificar la identidad de la computadora remota, haga clic en "Sí", esta advertencia es solo porque es un certificado SSL autofirmado y no hay nada de qué preocuparse.

### Configuración del servidor web con IIS (Servicios de información de Internet)

Cuando se conecte por primera vez a la instancia de Azure Windows Server a través de RDP, debería ver la interfaz del Administrador del servidor.

1. **Administrador del servidor**
- Haga clic en "Agregar roles y características".
- **Tipo de instalación** : seleccione "Instalación basada en funciones o funciones" y haga clic en Siguiente.
- **Selección de servidor** : deje el valor predeterminado y haga clic en Siguiente.
- **Funciones del servidor** : marque la casilla "Servidor web (IIS)", luego haga clic en el botón "Agregar características" en la ventana emergente y haga clic en Siguiente.
- **Funciones** : deje el valor predeterminado y haga clic en Siguiente.
- **Rol de servidor web (IIS)** : deje el valor predeterminado y haga clic en Siguiente.
- **Servicios de función** : deje los valores predeterminados y haga clic en Siguiente.
- **Confirmación** - Haga clic en instalar.
- **Resultados** : espere a que se complete la instalación y haga clic en cerrar.

2. Descargue e instale el paquete de alojamiento de .NET Core desde https://www.microsoft.com/net/permalink/dotnetcore-current-windows-runtime-bundle-installer . Haga esto descargando el archivo a su máquina local y copiándolo en el servidor a través del escritorio remoto, o agregando `https://*.microsoft.com` a los "Sitios confiables" en la configuración de seguridad de Internet Explorer en el servidor para permitir que el archivo se descargue.

3. Reinicie IIS con el comando `net stop was /y && net start w3svc`

4. Descargue e instale el módulo de reescritura de URL de IIS desde https://www.iis.net/downloads/microsoft/url-rewrite . Haga esto descargando el archivo a su máquina local y copiándolo al servidor a través del escritorio remoto, o agregando `https://www.iis.net` y `https://webpihandler.azurewebsites.net` a los "Sitios confiables" en la configuración de seguridad de Internet Explorer en el servidor para permitir que el archivo se descargue.

### Crear base de datos Azure SQL

A continuación, crearemos una nueva base de datos de SQL Server para la aplicación en la nube mediante el servicio Azure SQL Database.

1. Vaya a la sección **Bases de datos SQL** del portal de Azure, puede encontrar esto ingresando "SQL" en la barra de búsqueda principal y seleccionando el servicio "Bases de datos SQL".

2. Haga clic en "Agregar" o "Crear base de datos SQL".

3. **Lo esencial**
- **Grupo de recursos** : seleccione el mismo grupo de recursos en el que se encuentra la máquina virtual de Windows Server (por ejemplo, mi grupo de recursos).
- **Nombre de la base de datos** : ingrese un nombre para la base de datos SQL (por ejemplo, my-sql-db).
- **Servidor** : haga clic en "Crear nuevo".
  - Nombre del servidor : ingrese un nombre único global para el servidor, se usará para crear la URL del servidor Azure SQL: `<server-name>.database.windows.net.`
  - **Inicio de sesión del administrador del servidor** : ingrese el nombre de usuario del administrador para el servidor Azure SQL.
  - **Contraseña** : ingrese la contraseña de administrador para el servidor Azure SQL.
  - **Confirmar contraseña** : vuelva a ingresar la contraseña de administrador para el servidor Azure SQL.
  - **Ubicación** : seleccione la misma región que la máquina virtual de Windows Server.
- **Cómputo + almacenamiento** : haga clic en "Configurar base de datos", luego seleccione "Básico" y haga clic en el botón "Aplicar".

4. **Redes**
- Método de conectividad : seleccione "Punto final público".
- Permitir que los servicios y recursos de Azure accedan a este servidor : seleccione "Sí".

5. **Revisar + crear** : haz clic en "Crear".

### Crear e implementar la API back-end de ASP.NET Core en Azure

Siga estos pasos para clonar y compilar la API ASP.NET Core en su máquina local y luego implementarla en el servidor.

1. Clonar el proyecto ASP.NET Core API en una carpeta en su máquina local con el comando git clone `https://github.com/FernandoCalmet/DOTNET-6-ASPNET-Core-API-JWT-CRUD.git`. Si no tiene instalada la CLI de Git, puede descargarla desde https://git-scm.com/downloads . El proyecto de back-end tiene como nombre `CRUDWebAPI`.

2. Actualice la cadena de conexión de la base de datos para que apunte a la nueva base de datos SQL de Azure:
- En Azure Portal, vaya a la página de descripción general de la base de datos SQL creada en el paso anterior.
- Haga clic en "Mostrar cadenas de conexión de la base de datos" y copie la cadena de conexión "ADO.NET (autenticación SQL)".
- Abra el archivo de configuración de la aplicación ASP.NET Core (`/appsettings.json`) en un editor de texto.
- Reemplace el valor de la `DefaultConnection` cadena de conexión con el que acaba de copiar, para que se vea así:

```
"ConnectionStrings": {
  "DefaultConnection": "Server=tcp:{server_name},1433;Initial Catalog={database_name};Persist Security Info=False;User ID={user_name};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;"
},
```

- Dentro de la cadena de conexión, reemplácela `{your_password}` con la contraseña de administrador del servidor Azure SQL que creó al configurar la base de datos.

3. Actualice el secreto de firma del token JWT:
- Abra el archivo de configuración de la aplicación ASP.NET Core (`/appsettings.json`) en un editor de texto.
- Reemplace el valor de la configuración de la aplicación `Secret` con su propia cadena aleatoria, una forma rápida y fácil es generar un par de GUID y unirlos para crear una cadena aleatoria larga (por ejemplo, de https://www.guidgenerator.com/ ).

4. Cree la API con el comando `dotnet publish --configuration Release` desde la carpeta raíz del proyecto (donde se encuentra el archivo WebApi.csproj). Si no tiene instalado .NET Core SDK, puede descargarlo desde https://www.microsoft.com/net/download/core .

5. Copie los archivos del directorio `aspnet-core-3-registration-login-api\bin\Release\netcoreapp3.1\publish` al directorio `C:\Projects\back-end` en el servidor a través del escritorio remoto.
  
Los archivos de la API de ASP.NET Core ahora están implementados en el servidor, pero la API aún no está en funcionamiento; esto sucederá cuando configuremos IIS en breve.

### Crear e implementar la aplicación front-end de Angular en Azure

Siga estos pasos para compilar la aplicación Angular en su máquina local y luego implementarla en el servidor de Azure.

1. Clone el proyecto Angular a una carpeta en su máquina local con el comando git clone `https://github.com/FernandoCalmet/DOTNET-6-ASPNET-Core-API-JWT-CRUD.git`. Si no tiene instalada la CLI de Git, puede descargarla desde https://git-scm.com/downloads .El proyecto de back-end tiene como nombre `WebFrontEnd`.

2. Navegue al directorio clonado e instale todos los paquetes de nodos requeridos con el comando `npm install`. Si necesita instalar Node.js (que incluye npm), puede descargarlo desde https://nodejs.org/ .

3. Cree la aplicación Angular con el comando `npm run build`.

4. Copie los archivos del directorio `angular-8-registration-login-crud\dist` al directorio `C:\Projects\front-end` en el servidor a través del escritorio remoto.

### Configurar IIS para servir el front-end de Angular y la API de ASP.NET Core

ado que nuestra aplicación Angular + ASP.NET Core se compone de dos proyectos separados a los que se debe acceder a través del mismo puerto (HTTP en el puerto 80), vamos a configurar un solo sitio en IIS para atender el frente de Angular. finalice la aplicación desde la ruta base ( /) y cree una aplicación secundaria para ASP.NET Core API que maneje todas las solicitudes que comiencen con la ruta /api.

Siga estos pasos para configurar IIS para la aplicación de pila completa Angular + ASP.NET Core.

1. Abra IIS en el servidor.
2. Elimine el "Sitio web predeterminado" en Sitios y "DefaultAppPool" en Grupos de aplicaciones.
3. Haga clic derecho en la carpeta Sitios y seleccione "Agregar sitio web".
4. Ingrese el nombre del sitio (por ejemplo, mi aplicación).
5. Establezca la ruta física al directorio de la aplicación Angular (`C:\Projects\front-end`).
6. Deje el nombre de host vacío y haga clic en "Aceptar".
7. Haga clic derecho en el nuevo sitio y seleccione "Agregar aplicación".
8. Introduzca el alias "api" (sin comillas).
9. Establezca la ruta física al directorio api de ASP.NET Core (`C:\Projects\back-end`).
10. Haga clic en Aceptar".
11. En Grupos de aplicaciones, haga clic con el botón derecho en el grupo de aplicaciones para el nuevo sitio y seleccione "Configuración básica". Cambie la versión de .NET CLR a 'Sin código administrado', las aplicaciones .NET Core no requieren .NET CLR.
12. Cree un archivo llamado "web.config" dentro de la carpeta front-end de Angular (`C:\Projects\front-end`) y agregue la siguiente configuración:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.webServer>
        <staticContent>
            <remove fileExtension=".js" />
            <mimeMap fileExtension=".js" mimeType="application/javascript; charset=UTF-8" />
        </staticContent>
        <rewrite>
            <rules>
                <rule name="Angular" stopProcessing="true">
                    <match url=".*" />
                    <conditions logicalGrouping="MatchAll">
                        <add input="{REQUEST_URI}" pattern="^/api/.*" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="/" />
                </rule>
            </rules>
        </rewrite>
    </system.webServer>
</configuration>
```

La configuración `<staticContent>` establece la codificación de caracteres en "UTF-8" para los archivos javascript, lo que evita que los caracteres Unicode en su javascript se conviertan antes de enviarse al navegador, lo que puede causar errores (por ejemplo, errores de expresión regular no válidos).

La configuración `<rewrite>` crea una regla de reescritura que permite actualizar la aplicación Angular sin obtener errores 404.

### Pruebar la aplicación Angular + ASP.NET Core + SQL Server ejecutándose en Azure

ngrese la dirección IP pública de su Azure Windows Server en un navegador para acceder y probar su nueva aplicación de pila completa Angular + ASP.NET Core + Azure SQL Server.

La dirección IP pública se puede ubicar en la página de descripción general de la máquina virtual en el portal de Microsoft Azure.

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
