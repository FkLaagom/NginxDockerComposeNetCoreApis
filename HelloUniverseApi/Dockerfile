# Get base SDK Image from Microsoft
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

# Copy csproj and restore as any dependecies (via NUGET)
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build release
COPY . ./
RUN dotnet publish -c Release -o out

# Generate runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
#EXPOSE 80
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "HelloUniverseApi.dll"] 