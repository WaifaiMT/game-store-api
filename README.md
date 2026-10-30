# GameStore API

A REST API for a video game catalog, built with **ASP.NET Core 9 minimal APIs** and **Entity Framework Core**.

> I built this while following an ASP.NET Core minimal APIs course, as a hands-on way to learn the .NET web stack. It's a learning project; my production work is in TypeScript/Node.js and ASP.NET Core (see my [GitHub profile](https://github.com/WaifaiMT)). Planned improvements are listed below.

## Features

- CRUD endpoints for games, plus a read-only genres endpoint
- Request validation (invalid input returns `400` with details)
- DTOs and mapping extensions to keep entities out of the API contract
- EF Core with SQLite, migrations, and seeded genre data. The database is created and migrated automatically on startup.

## Tech stack

ASP.NET Core 9 · C# · Entity Framework Core 9 · SQLite · MinimalApis.Extensions (validation)

## Endpoints

| Method | Route | Description | Responses |
|---|---|---|---|
| `GET` | `/games` | List all games with their genre | `200` |
| `GET` | `/games/{id}` | Get one game | `200`, `404` |
| `POST` | `/games` | Create a game | `201`, `400` |
| `PUT` | `/games/{id}` | Update a game | `204`, `400`, `404` |
| `DELETE` | `/games/{id}` | Delete a game | `204`, `404` |
| `GET` | `/genres` | List genres | `200` |

Example request body for `POST /games`:

```json
{
  "name": "Street Fighter II",
  "genreId": 1,
  "price": 19.99,
  "releaseDate": "1992-07-15"
}
```

Ready-made requests are in [`games.http`](src/GameStore.Api/games.http) and [`genres.http`](src/GameStore.Api/genres.http). They run directly in VS Code (REST Client) or Visual Studio.

## Running locally

Requires the [.NET 9 SDK](https://dotnet.microsoft.com/download).

```bash
git clone https://github.com/WaifaiMT/game-store-api.git
cd game-store-api
dotnet run --project src/GameStore.Api
```

The API listens on `http://localhost:5247`. A local `GameStore.db` SQLite file is created on first run.

## Project structure

```
src/GameStore.Api/
├── Data/         # DbContext, migrations, startup migration helper
├── Dtos/         # Request/response contracts
├── EndPoints/    # Minimal API route groups (games, genres)
├── Entities/     # EF Core entities
├── Mapping/      # Entity <-> DTO mapping extensions
└── Program.cs
```

## Roadmap

- [ ] Upgrade to .NET 10 (LTS)
- [ ] PostgreSQL + Docker Compose
- [ ] JWT authentication with roles (admin-only writes)
- [ ] Pagination, filtering, and search on `GET /games`
- [ ] OpenAPI docs with Scalar UI
- [ ] Integration tests (xUnit + WebApplicationFactory + Testcontainers)
- [ ] GitHub Actions CI and a hosted demo

## License

MIT
