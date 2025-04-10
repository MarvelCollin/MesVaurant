FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MesVaurant.API/MesVaurant.API.csproj", "MesVaurant.API/"]
COPY ["MesVaurant.Application/MesVaurant.Application.csproj", "MesVaurant.Application/"]
COPY ["MesVaurant.Domain/MesVaurant.Domain.csproj", "MesVaurant.Domain/"]
COPY ["MesVaurant.Infrastructure/MesVaurant.Infrastructure.csproj", "MesVaurant.Infrastructure/"]
RUN dotnet restore "MesVaurant.API/MesVaurant.API.csproj"
COPY . .
WORKDIR "/src/MesVaurant.API"
RUN dotnet build "MesVaurant.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MesVaurant.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MesVaurant.API.dll"]