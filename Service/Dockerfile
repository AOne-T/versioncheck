FROM mcr.microsoft.com/dotnet/sdk:3.1 as base
WORKDIR /app-src
COPY Service/Service.csproj Service/Service.csproj
COPY Subproject/Subproject.csproj Subproject/Subproject.csproj
RUN dotnet restore Service/Service.csproj

FROM base as build
ARG VERSION=1
ARG CONFIGURATION=Debug
RUN dotnet publish Service/Service.csproj \
        -c ${CONFIGURATION} \
        /p:SolutionDir=$PWD \
        /bl:version_suffix.binlog \
        /consoleloggerparameters:ErrorsOnly \
        --version-suffix ${VERSION} \
        -r linux-x64 \
        --self-contained false \
        -o /app-publish || true \
        && cat /app-src/Subproject/obj/Debug/netstandard2.0/Subproject.AssemblyInfo.cs \
        && exit 0

FROM mcr.microsoft.com/dotnet/aspnetcore-runtime:3.1 as publish
WORKDIR /app
COPY --from=build /app-publish .