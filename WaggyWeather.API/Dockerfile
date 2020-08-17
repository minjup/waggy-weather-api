#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["WaggyWeather.API/WaggyWeather.API.csproj", "WaggyWeather.API/"]
RUN dotnet restore "WaggyWeather.API/WaggyWeather.API.csproj"
COPY . .
WORKDIR "/src/WaggyWeather.API"
RUN dotnet build "WaggyWeather.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WaggyWeather.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WaggyWeather.API.dll"]