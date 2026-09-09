# Bump Intent.Packager reference to 3.6.1 for modules touched in d7a06ca783

## Context
The previous commit (`d7a06ca783` — "Updated all the modules with Default Severity and Classifications") touched 31 module directories under `Modules/`. Each module's `.csproj` carries a `PackageReference Include="Intent.Packager"` entry. The user wants that reference bumped to version `3.6.1` for every module affected by that commit — and nothing else (no module version bumps, no other dependency changes, no other files touched).

## Scope: modules to update
Determined via `git show --stat --name-only d7a06ca783` and confirmed each has an `Intent.Packager` `PackageReference` in its `.csproj`. Current versions found (mostly `3.6.0`, a few `3.5.0`):

- Intent.Modules.Application.AutoMapper (3.6.0)
- Intent.Modules.Application.Contracts (3.6.0)
- Intent.Modules.Application.DependencyInjection (3.6.0)
- Intent.Modules.Application.DependencyInjection.MediatR (3.6.0)
- Intent.Modules.Application.Dtos (3.6.0)
- Intent.Modules.Application.Dtos.AutoMapper (3.6.0)
- Intent.Modules.Application.Dtos.Mapperly (3.6.0)
- Intent.Modules.Application.Dtos.Pagination (3.6.0)
- Intent.Modules.Application.FluentValidation.Dtos (3.6.0)
- Intent.Modules.Application.Identity (3.5.0)
- Intent.Modules.Application.MediatR (3.6.0)
- Intent.Modules.Application.MediatR.Behaviours (3.6.0)
- Intent.Modules.Application.MediatR.FluentValidation (3.6.0)
- Intent.Modules.Application.ServiceImplementations (3.6.0)
- Intent.Modules.Application.Wolverine (3.6.0)
- Intent.Modules.Application.Wolverine.FluentValidation (3.6.0)
- Intent.Modules.AspNetCore (3.6.0)
- Intent.Modules.AspNetCore.Controllers (3.6.0)
- Intent.Modules.AspNetCore.HealthChecks (3.6.0)
- Intent.Modules.AspNetCore.IntegrationTesting (3.6.0)
- Intent.Modules.AspNetCore.Logging.Serilog (3.6.0)
- Intent.Modules.AspNetCore.Swashbuckle (3.6.0)
- Intent.Modules.AspNetCore.Swashbuckle.Security (3.6.0)
- Intent.Modules.AspNetCore.Versioning (3.5.0)
- Intent.Modules.Entities (3.6.0)
- Intent.Modules.Entities.Repositories.Api (3.5.0)
- Intent.Modules.EntityFrameworkCore (3.5.0)
- Intent.Modules.EntityFrameworkCore.DiffAudit (3.6.0)
- Intent.Modules.EntityFrameworkCore.Repositories (3.6.0)
- Intent.Modules.Hangfire (3.6.0)
- Intent.Modules.Infrastructure.DependencyInjection (3.6.0)
- Intent.Modules.ValueObjects (3.6.0)

## Change
For each module's `Modules/<ModuleName>/<ModuleName>.csproj`, edit only the line:
```
<PackageReference Include="Intent.Packager" Version="3.6.0">   (or "3.5.0")
```
to:
```
<PackageReference Include="Intent.Packager" Version="3.6.1">
```
Use a targeted string replacement per file (matching on the exact `Intent.Packager` line, since indentation varies slightly between files — e.g. Wolverine and EntityFrameworkCore.Repositories use 8-space indent instead of 4). Do not touch any other `PackageReference`, the module's own `<Version>`, `imodspec`, `pkg.config`, `modules.config`, or `release-notes.md` files.

## Explicitly out of scope
- No module version bumps (module's own version in `.imodspec` / `pkg.config` / `modules.config` stays as-is).
- No changes to any other NuGet package references.
- No changes to `release-notes.md` or other module metadata files.

## Verification
- Re-run the same `grep -n "Intent.Packager"` sweep across all 31 `.csproj` files and confirm every one now reads `Version="3.6.1"`.
- `git diff --stat` should show exactly 31 files changed, each a single-line diff (the `Intent.Packager` version attribute only).
