FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ConsoleAppSelfHostWebApi/ConsoleAppSelfHostWebApi.csproj", "ConsoleAppSelfHostWebApi/"]
RUN dotnet restore "ConsoleAppSelfHostWebApi/ConsoleAppSelfHostWebApi.csproj"
COPY . .
WORKDIR "/src/ConsoleAppSelfHostWebApi"
RUN dotnet build "ConsoleAppSelfHostWebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleAppSelfHostWebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleAppSelfHostWebApi.dll"]
