ARG VARIANT="5.0-focal"
FROM mcr.microsoft.com/dotnet/sdk:${VARIANT} AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:${VARIANT}
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "sample.dll"]