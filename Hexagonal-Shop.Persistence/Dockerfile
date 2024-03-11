FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Hexagonal-Shop.Persistence/Hexagonal-Shop.Persistence.csproj", "Hexagonal-Shop.Persistence/"]
RUN dotnet restore "Hexagonal-Shop.Persistence/Hexagonal-Shop.Persistence.csproj"
COPY . .
WORKDIR "/src/Hexagonal-Shop.Persistence"
RUN dotnet build "Hexagonal-Shop.Persistence.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hexagonal-Shop.Persistence.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hexagonal-Shop.Persistence.dll"]
