# Get Base Image (Full .NET Core SDK)
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY EksGithubActions/*.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY EksGithubActions ./
RUN dotnet publish -c Release -o out -r alpine-x64

# Generate runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine
WORKDIR /app
COPY --from=build-env /app/out .