FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY samples/samples.csproj samples/
RUN dotnet restore samples/samples.csproj
COPY . .
WORKDIR /src/samples
RUN dotnet build samples.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish samples.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "samples.dll"]
