FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MesVaurant.UI.csproj", "./"]
RUN dotnet restore "MesVaurant.UI.csproj"
COPY . .
RUN dotnet build "MesVaurant.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MesVaurant.UI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MesVaurant.UI.dll"]