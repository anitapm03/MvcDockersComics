﻿FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY *.csproj ./

RUN dotnet restore 
COPY . .
WORKDIR "/src/MvcDockersComics"

RUN dotnet build "/src/MvcDockersComics.csproj" -c Release -o /app/build
 

FROM build AS publish
RUN dotnet publish "/src/MvcDockersComics.csproj" -c Release -o /app/publish
 

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MvcDockersComics.dll"]