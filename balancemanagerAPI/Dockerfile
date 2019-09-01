FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY balancemanagerAPI/balancemanagerAPI.csproj balancemanagerAPI/
RUN dotnet restore "balancemanagerAPI/balancemanagerAPI.csproj"
COPY . .
WORKDIR "/src/balancemanagerAPI"
RUN dotnet build "balancemanagerAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "balancemanagerAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "balancemanagerAPI.dll"]
