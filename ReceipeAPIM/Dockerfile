FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 59006
EXPOSE 44317

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ReceipeAPIM/ReceipeAPIM.csproj ReceipeAPIM/
RUN dotnet restore ReceipeAPIM/ReceipeAPIM.csproj
COPY . .
WORKDIR /src/ReceipeAPIM
RUN dotnet build ReceipeAPIM.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ReceipeAPIM.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ReceipeAPIM.dll"]
