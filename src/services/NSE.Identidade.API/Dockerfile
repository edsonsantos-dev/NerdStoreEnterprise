﻿FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/services/NSE.Identidade.API/NSE.Identidade.API.csproj", "src/services/NSE.Identidade.API/"]
RUN dotnet restore "src/services/NSE.Identidade.API/NSE.Identidade.API.csproj"
COPY . .
WORKDIR "/src/src/services/NSE.Identidade.API"
RUN dotnet build "NSE.Identidade.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NSE.Identidade.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NSE.Identidade.API.dll"]
