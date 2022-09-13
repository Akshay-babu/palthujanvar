FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["palthujanvar.csproj", "."]
RUN dotnet restore "./palthujanvar.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "palthujanvar.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "palthujanvar.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "palthujanvar.dll"]