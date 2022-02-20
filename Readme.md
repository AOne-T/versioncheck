Local build using `tasks.json` or manually calling
`dotnet publish /property:GenerateFullPaths=true /consoleloggerparameters:NoSummary --version-suffix 20220220-master-1 Service/Service.csproj`
Succeeds

While calling `docker build -t st --target build --build-arg VERSION=20220220-master-1 -f Service/Dockerfile .`
Fails