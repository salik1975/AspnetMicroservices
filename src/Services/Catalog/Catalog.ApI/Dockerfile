#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Services/Catalog/Catalog.ApI/Catalog.ApI.csproj", "Services/Catalog/Catalog.ApI/"]
RUN dotnet restore "Services/Catalog/Catalog.ApI/Catalog.ApI.csproj"
COPY . .
WORKDIR "/src/Services/Catalog/Catalog.ApI"
RUN dotnet build "Catalog.ApI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Catalog.ApI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Catalog.ApI.dll"]
