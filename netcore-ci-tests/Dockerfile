FROM microsoft/dotnet
WORKDIR /app

COPY netcore-ci-tests.csproj .
RUN dotnet restore

COPY . .
RUN dotnet test