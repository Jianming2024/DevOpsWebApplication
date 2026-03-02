# 1) Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# copy everything and publish
COPY . .
RUN dotnet restore DevOpsWebApplication/DevOpsWebApplication.csproj
RUN dotnet publish DevOpsWebApplication/DevOpsWebApplication.csproj -c Release -o /app/publish

# 2) Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

COPY --from=build /app/publish .
EXPOSE 8080
ENV ASPNETCORE_URLS=http://0.0.0.0:8080

ENTRYPOINT ["dotnet", "DevOpsWebApplication.dll"]