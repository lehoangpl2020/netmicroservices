#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Servicers/Ordering/Ordering.API/Ordering.API.csproj", "Servicers/Ordering/Ordering.API/"]
COPY ["Servicers/Ordering/Ordering.Application/Ordering.Application.csproj", "Servicers/Ordering/Ordering.Application/"]
COPY ["Servicers/Ordering/Ordering.Domain/Ordering.Domain.csproj", "Servicers/Ordering/Ordering.Domain/"]
COPY ["BuildingBlocks/EventBus.Messages/EventBus.Messages.csproj", "BuildingBlocks/EventBus.Messages/"]
COPY ["Servicers/Ordering/Ordering.Infrastructure/Ordering.Infrastructure.csproj", "Servicers/Ordering/Ordering.Infrastructure/"]
RUN dotnet restore "Servicers/Ordering/Ordering.API/Ordering.API.csproj"
COPY . .
WORKDIR "/src/Servicers/Ordering/Ordering.API"
RUN dotnet build "Ordering.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Ordering.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Ordering.API.dll"]