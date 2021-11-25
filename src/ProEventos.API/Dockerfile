
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
#EXPOSE 80
#EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ProEventos.Api/ProEventos.API.csproj", "ProEventos.Api/"]
COPY ["ProEventos.Application/ProEventos.Application.csproj", "ProEventos.Application/"]
COPY ["ProEventos.Persistence/ProEventos.Persistence.csproj", "ProEventos.Persistence/"]
COPY ["ProEventos.Domain/ProEventos.Domain.csproj", "ProEventos.Domain/"]
RUN dotnet restore "ProEventos.Api/ProEventos.API.csproj"
COPY . .
WORKDIR "/src/ProEventos.Api"
RUN dotnet build "ProEventos.API.csproj" -c Release -o /app/build


FROM build AS publish
RUN dotnet publish "ProEventos.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ProEventos.API.dll"]