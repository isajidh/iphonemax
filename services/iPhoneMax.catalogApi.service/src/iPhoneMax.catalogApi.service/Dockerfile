FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 5001

ENV ASPNETCORE_URLS=http://+:5001

# Creates a non-root user with an explicit UID and adds permission to access the /app folder
# For more info, please refer to https://aka.ms/vscode-docker-dotnet-configure-containers
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
USER appuser

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["services/iPhoneMax.catalogApi.service/src/iPhoneMax.catalogApi.service/Ecom.Catalog.Service.csproj", "services/iPhoneMax.catalogApi.service/src/iPhoneMax.catalogApi.service/"]
RUN dotnet restore "services/iPhoneMax.catalogApi.service/src/iPhoneMax.catalogApi.service/Ecom.Catalog.Service.csproj"
COPY . .
WORKDIR "/src/services/iPhoneMax.catalogApi.service/src/iPhoneMax.catalogApi.service"
RUN dotnet build "Ecom.Catalog.Service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Ecom.Catalog.Service.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Ecom.Catalog.Service.dll"]
