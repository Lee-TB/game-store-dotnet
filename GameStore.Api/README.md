# Game Store API

## Starting SQL Server
Running SQL Server as a Docker container
```powershell
$sa_password = "[SA PASSWORD HERE]"
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=$sa_password" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d --rm --name mssql mcr.microsoft.com/mssql/server:2022-latest
```

## Setting the connection string to the scret manager
https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-8.0&tabs=windows#set-multiple-secrets

To use user secrets, run the following command in the project directory
```powershell
dotnet user-secrets init
```
Set a secret
```powershell
$sa_password = "[SA PASSWORD HERE]"

dotnet user-secrets set  "ConnectionStrings:GameStoreContext" "Server=localhost; Database=GameStore; User Id=sa; Password=$sa_password; TrustServerCertificate=True;"
```

## Swagger
Add Swashbuckle.AspNetCore 6.5.0 package.
```powershell
dotnet add package Swashbuckle.AspNetCore --version 6.5.0
```
Add the following code.
```c#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
// another code

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}
// another code
```