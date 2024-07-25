# Use the official .NET 8 SDK image as the build image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Set the working directory
WORKDIR /app

# Copy the project file and restore any dependencies (via `dotnet restore`)
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application files and build the application
COPY . ./
RUN dotnet publish -c Release -o out

# Use the official ASP.NET Core runtime image as the base image for the final image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

# Set the working directory
WORKDIR /app

# Copy the build output from the build image to the runtime image
COPY --from=build /app/out .


# Specify the entry point for the application
ENTRYPOINT ["dotnet", "miniteste.dll"]
