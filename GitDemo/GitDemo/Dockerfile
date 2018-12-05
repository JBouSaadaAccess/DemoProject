FROM microsoft/dotnet:2.1-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY GitDemo/GitDemo.csproj GitDemo/
RUN dotnet restore GitDemo/GitDemo.csproj
COPY . .
WORKDIR /src/GitDemo
RUN dotnet build GitDemo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish GitDemo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GitDemo.dll"]
