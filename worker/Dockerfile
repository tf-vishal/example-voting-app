#Two Stages Buiild and Run
#Copy files from/to?
#What's the EntryPoint?


#Stage 1 Build the application
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:9.0-bookworm-slim AS build

#Copy Project files and restore dependencies
WORKDIR /src
COPY Worker.csproj .
RUN dotnet restore 

#COPY source code and build
COPY . .
RUN dotnet publish Worker.csproj -c Release -o /app --self-contained false --no-restore

#Stage 3 Create runtime image
FROM mcr.microsoft.com/dotnet/sdk:9.0-bookworm-slim AS runtime
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]