# .NET 8.0 CronJob Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["JimmeApp.CronJob/JimmeApp.CronJob.csproj", "JimmeApp.CronJob/"]
RUN dotnet restore "JimmeApp.CronJob/JimmeApp.CronJob.csproj"
COPY . .
WORKDIR "/src/JimmeApp.CronJob"
RUN dotnet publish "JimmeApp.CronJob.csproj" -c Release -o /app/publish

FROM build AS publish

FROM mcr.microsoft.com/dotnet/runtime:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JimmeApp.CronJob.dll"]