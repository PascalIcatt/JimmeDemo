# .NET 8.0 Web API Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["JimmeApp.WebApi/JimmeApp.WebApi.csproj", "JimmeApp.WebApi/"]
RUN dotnet restore "JimmeApp.WebApi/JimmeApp.WebApi.csproj"
COPY . .
WORKDIR "/src/JimmeApp.WebApi"
RUN dotnet build "JimmeApp.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "JimmeApp.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JimmeApp.WebApi.dll"]