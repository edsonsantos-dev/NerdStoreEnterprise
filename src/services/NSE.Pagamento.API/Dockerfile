﻿FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/services/NSE.Pagamento.API/NSE.Pagamento.API.csproj", "src/services/NSE.Pagamento.API/"]
RUN dotnet restore "src/services/NSE.Pagamento.API/NSE.Pagamento.API.csproj"
COPY . .
WORKDIR "/src/src/services/NSE.Pagamento.API"
RUN dotnet build "NSE.Pagamento.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NSE.Pagamento.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NSE.Pagamento.API.dll"]
