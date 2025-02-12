# Stage 1: Build the .NET app
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy the project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the entire project and build the application
COPY . ./
RUN dotnet publish -c Release -o /app/build

# Stage 2: Run the app with ASP.NET runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/build ./

# Expose the application port
EXPOSE 80
EXPOSE 443
EXPOSE 888

# Define the entry point for the application
ENTRYPOINT ["dotnet", "test-api.dll"]
