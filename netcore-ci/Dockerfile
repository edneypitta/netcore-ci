FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY netcore-ci/netcore-ci.csproj netcore-ci/
RUN dotnet restore netcore-ci/netcore-ci.csproj

COPY . .
WORKDIR /src/netcore-ci
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .

ENTRYPOINT ["dotnet"]
CMD [ "netcore-ci.dll" ]
