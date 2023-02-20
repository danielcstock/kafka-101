FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["csharp-kafka-101/csharp-kafka-101.csproj", "csharp-kafka-101/"]
RUN dotnet restore "csharp-kafka-101/csharp-kafka-101.csproj"
COPY . .
WORKDIR "/src/csharp-kafka-101"
RUN dotnet build "csharp-kafka-101.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "csharp-kafka-101.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "csharp-kafka-101.dll"]
