FROM microsoft/dotnet:2.1-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Test/Test.csproj Test/
RUN dotnet restore Test/Test.csproj
COPY . .
WORKDIR /src/Test
RUN dotnet build Test.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Test.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Test.dll"]
