#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["TestDebugger/TestDebugger.csproj", "TestDebugger/"]
RUN dotnet restore "TestDebugger/TestDebugger.csproj"
COPY . .
WORKDIR "/src/TestDebugger"
RUN dotnet build "TestDebugger.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestDebugger.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestDebugger.dll"]