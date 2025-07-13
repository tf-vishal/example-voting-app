#Two Stages Buiild and Run
#Copy files from/to?
#What's the EntryPoint?


#Stage 1 Build the application
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:9.0-bookworm-slim AS build
ARG TARGETPLATFORM
ARG TARGETARCH
ARG BUILDPLATFORM

RUN echo "Building for platform: $TARGETPLATFORM, architecture: $TARGETARCH, build platform: $BUILDPLATFORM"


#Copy Project files and restore dependencies
WORKDIR /src
COPY Worker.csproj .
RUN dotnet restore -a ${TARGETARCH} 

#COPY source code and build
COPY . .
RUN dotnet publish Worker.csproj -c Release -o /app -a $TARGETARCH --self-contained false --no-restore

#Stage 2 Create runtime image
FROM mcr.microsoft.com/dotnet/runtime:9.0 AS runtime
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]