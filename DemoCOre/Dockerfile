FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DemoCOre/DemoCOre.csproj", "DemoCOre/"]
RUN dotnet restore "DemoCOre/DemoCOre.csproj"
COPY . .
WORKDIR "/src/DemoCOre"
RUN dotnet build "DemoCOre.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DemoCOre.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DemoCOre.dll"]