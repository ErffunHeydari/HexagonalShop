FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Hexagonal-Shop.Messaging/Hexagonal-Shop.Messaging.csproj", "Hexagonal-Shop.Messaging/"]
RUN dotnet restore "Hexagonal-Shop.Messaging/Hexagonal-Shop.Messaging.csproj"
COPY . .
WORKDIR "/src/Hexagonal-Shop.Messaging"
RUN dotnet build "Hexagonal-Shop.Messaging.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hexagonal-Shop.Messaging.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hexagonal-Shop.Messaging.dll"]
