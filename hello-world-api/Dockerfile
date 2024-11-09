# Use the official .NET SDK 5.0 image to build the app
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app

# Copy the project files and restore any dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application code and build the app
COPY . ./
RUN dotnet publish -c Release -o /app/out

# Use the runtime image for .NET 5.0 to run the app
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app/out .

# Expose port 80 and run the application
EXPOSE 80
ENTRYPOINT ["dotnet", "hello-world-api.dll"]
