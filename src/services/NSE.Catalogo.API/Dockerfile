﻿FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/services/NSE.Catalogo.API/NSE.Catalogo.API.csproj", "src/services/NSE.Catalogo.API/"]
RUN dotnet restore "src/services/NSE.Catalogo.API/NSE.Catalogo.API.csproj"
COPY . .
WORKDIR "/src/src/services/NSE.Catalogo.API"
RUN dotnet build "NSE.Catalogo.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NSE.Catalogo.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NSE.Catalogo.API.dll"]
