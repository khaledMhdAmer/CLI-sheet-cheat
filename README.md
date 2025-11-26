Absolutely! Using the CLI is actually faster and more consistent. Here's how to create your entire solution structure:

## Step 1: Create Solution and Projects

```bash
# Create a new solution
dotnet new sln -n YourProjectName

# Create the API project (already exists, but here's how you'd create it)
dotnet new webapi -n YourProjectName.API

# Create the DAL project (Class Library)
dotnet new classlib -n YourProjectName.DAL

# Create the CMS project (I'll show MVC, Razor Pages, and Blazor options)
# Option A: MVC
dotnet new mvc -n YourProjectName.CMS

# Option B: Razor Pages (simpler for CMS)
dotnet new webapp -n YourProjectName.CMS

# Option C: Blazor Server
dotnet new blazor -n YourProjectName.CMS
```

## Step 2: Add Projects to Solution

```bash
dotnet sln add YourProjectName.API/YourProjectName.API.csproj
dotnet sln add YourProjectName.DAL/YourProjectName.DAL.csproj
dotnet sln add YourProjectName.CMS/YourProjectName.CMS.csproj
```

## Step 3: Add Project References

```bash
# API references DAL
dotnet add YourProjectName.API/YourProjectName.API.csproj reference YourProjectName.DAL/YourProjectName.DAL.csproj

# CMS references DAL
dotnet add YourProjectName.CMS/YourProjectName.CMS.csproj reference YourProjectName.DAL/YourProjectName.DAL.csproj
```

## Step 4: Add NuGet Packages to DAL

```bash
cd YourProjectName.DAL

dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Tools
dotnet add package Microsoft.EntityFrameworkCore.Design

cd ..
```

## Complete Example Script

Here's a complete script you can run from your solution directory:

```bash
# Navigate to your projects folder
cd C:\YourProjectsFolder

# Create solution
dotnet new sln -n MyProject

# Create projects
dotnet new webapi -n MyProject.API
dotnet new classlib -n MyProject.DAL
dotnet new mvc -n MyProject.CMS

# Add to solution
dotnet sln add MyProject.API/MyProject.API.csproj
dotnet sln add MyProject.DAL/MyProject.DAL.csproj
dotnet sln add MyProject.CMS/MyProject.CMS.csproj

# Add project references
dotnet add MyProject.API/MyProject.API.csproj reference MyProject.DAL/MyProject.DAL.csproj
dotnet add MyProject.CMS/MyProject.CMS.csproj reference MyProject.DAL/MyProject.DAL.csproj

# Add EF Core packages to DAL
dotnet add MyProject.DAL/MyProject.DAL.csproj package Microsoft.EntityFrameworkCore
dotnet add MyProject.DAL/MyProject.DAL.csproj package Microsoft.EntityFrameworkCore.SqlServer
dotnet add MyProject.DAL/MyProject.DAL.csproj package Microsoft.EntityFrameworkCore.Tools
dotnet add MyProject.DAL/MyProject.DAL.csproj package Microsoft.EntityFrameworkCore.Design
```

## Step 5: Verify Structure

```bash
# See your solution structure
dotnet sln list

# Build everything to make sure it works
dotnet build
```

## Running Projects

```bash
# Run the API
dotnet run --project MyProject.API

# Run the CMS (in another terminal)
dotnet run --project MyProject.CMS
```

## Bonus: Common CLI Commands

```bash
# Restore packages
dotnet restore

# Clean build artifacts
dotnet clean

# List available project templates
dotnet new list

# Create migration (from solution root, after setting up DbContext)
dotnet ef migrations add InitialCreate --project MyProject.DAL --startup-project MyProject.API

# Update database
dotnet ef database update --project MyProject.DAL --startup-project MyProject.API
```

This CLI approach is especially useful because you can script it, version control it, and it works identically across different machines and operating systems. Would you like me to show you how to set up a basic DbContext and entity in the DAL project next?
