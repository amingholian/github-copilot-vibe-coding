# PostHubAPI

The **PostHubAPI** is a blog API that provides complete CRUD (Create, Read, Update, Delete) functionalities for Posts and Comments, along with user registration capabilities.

## Technologies Used

### Language & Runtime

| Technology | Version |
|---|---|
| **C#** | 12 (via .NET 8) |
| **.NET SDK** | 8.0 |

### API / Web

| Package | Version | Purpose |
|---|---|---|
| **ASP.NET Core** | 8.0 | Web API framework |
| **ASP.NET Core Identity** | 8.0.1 | User and role management |
| `Microsoft.AspNetCore.Authentication.JwtBearer` | 8.0.0 | JWT authentication middleware |

### Data Access

| Package | Version | Purpose |
|---|---|---|
| **Entity Framework Core** | 8.0.1 | ORM / data access |
| `Microsoft.EntityFrameworkCore.Sqlite` | 8.0.1 | Production database provider |
| `Microsoft.EntityFrameworkCore.InMemory` | 8.0.1 | Development / test database provider |

### Application

| Package | Version | Purpose |
|---|---|---|
| **AutoMapper** (`AutoMapper.Extensions.Microsoft.DependencyInjection`) | 12.0.1 | DTO to model mapping |
| **BCrypt.Net** | 0.1.0 | Password hashing |

### API Documentation

| Package | Version | Purpose |
|---|---|---|
| **Swashbuckle.AspNetCore** (Swagger / OpenAPI) | 6.5.0 | API docs and interactive UI |

### Testing

| Package | Version | Purpose |
|---|---|---|
| **xUnit** | 2.9.3 | Test framework |
| `xunit.runner.visualstudio` | 3.1.4 | VS Test Explorer integration |
| `Microsoft.NET.Test.Sdk` | 17.14.1 | .NET test runner |
| `Microsoft.AspNetCore.Mvc.Testing` | 8.0.1 | Integration test web app factory |

### Tooling

| Tool | Purpose |
|---|---|
| **LibMan** | Client-side library manager |
| **User Secrets** | Local development secret storage (JWT key) |

## Project Instruction Files

- [.github/instructions/aspnet-core-web-api.instructions.md](.github/instructions/aspnet-core-web-api.instructions.md): API startup, controller, validation, and response conventions for this repository.
- [.github/instructions/entity-framework-core.instructions.md](.github/instructions/entity-framework-core.instructions.md): EF Core provider, query, mutation, and persistence guidance for the project data layer.
- [.github/instructions/automapper.instructions.md](.github/instructions/automapper.instructions.md): DTO mapping rules for profiles, service-layer mapping, and update flows.
- [.github/instructions/xunit-api-testing.instructions.md](.github/instructions/xunit-api-testing.instructions.md): Test conventions for integration-style API tests and controller behavior checks.
- [.github/instructions/jwt-bearer-authentication.instructions.md](.github/instructions/jwt-bearer-authentication.instructions.md): JWT configuration, secret handling, and authorization guidance.
- [.github/instructions/swagger-openapi.instructions.md](.github/instructions/swagger-openapi.instructions.md): Swagger/OpenAPI contract and documentation guidance for API endpoints.

## Features

- **CRUD for Posts**: Create, read, update, and delete blog posts.
- **CRUD for Comments**: Manage comments associated with each post.
- **User Registration**: Enable user registration and management to interact with the blog.

## How to Use

1. **Clone the Repository**:

```

git clone https://github.com/your-username/PostHubAPI.git

```

2. **Environment Setup**:

- Ensure you have Visual Studio or another .NET compatible IDE installed.
- Confirm that Entity Framework and AutoMapper are configured in the environment.

3. **Execution**:

- Open the project in your IDE.
- Run the application.

4. **Using the API**:

- Utilize the provided routes and endpoints to interact with the API functionalities.

## Authentication Configuration

- In `Development`, JWT `RequireHttpsMetadata` is disabled to support local non-HTTPS metadata scenarios.
- In non-development environments, JWT `RequireHttpsMetadata` is enabled by default.
- Configure `JWT:Secret` outside source control before starting the API.

### Local Secret Setup

1. Initialize user secrets for the project:

```powershell
dotnet user-secrets init --project .\PostHubAPI.csproj
```

2. Store a development JWT signing secret locally:

```powershell
dotnet user-secrets set "JWT:Secret" "replace-with-a-long-random-secret" --project .\PostHubAPI.csproj
```

3. As an alternative, set the `JWT__Secret` environment variable instead of using user secrets.

### Secret Rotation

1. Generate a new signing secret.
2. Update the user secret or `JWT__Secret` environment variable.
3. Restart the API so new tokens are issued with the rotated secret.
