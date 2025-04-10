# Gunakan image runtime .NET untuk menjalankan aplikasi
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Gunakan image SDK .NET untuk membangun aplikasi
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["MesVaurant/MesVaurant.csproj", "MesVaurant/"]
RUN dotnet restore "MesVaurant/MesVaurant.csproj"
COPY . .
WORKDIR "/src/MesVaurant"
RUN dotnet build "MesVaurant.csproj" -c $BUILD_CONFIGURATION -o /app/build

# Tahap publish aplikasi
FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "MesVaurant.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

# Tahap final: Gunakan image runtime .NET untuk menjalankan aplikasi yang sudah dipublikasikan
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MesVaurant.dll"]
