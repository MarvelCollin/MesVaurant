FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MesVaurant.UI/MesVaurant.UI.csproj", "MesVaurant.UI/"]
COPY ["MesVaurant.Application/MesVaurant.Application.csproj", "MesVaurant.Application/"]
COPY ["MesVaurant.Domain/MesVaurant.Domain.csproj", "MesVaurant.Domain/"]
RUN dotnet restore "MesVaurant.UI/MesVaurant.UI.csproj"
COPY . .
WORKDIR "/src/MesVaurant.UI"
RUN dotnet build "MesVaurant.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MesVaurant.UI.csproj" -c Release -o /app/publish --no-restore

FROM nginx:alpine AS final
EXPOSE 80
COPY --from=publish /app/publish/wwwroot /usr/share/nginx/html
COPY ["MesVaurant.UI/nginx.conf", "/etc/nginx/conf.d/default.conf"]