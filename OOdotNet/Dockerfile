FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["OOdotNet/OOdotNet.csproj", "OOdotNet/"]
RUN dotnet restore "OOdotNet/OOdotNet.csproj"
COPY . .
WORKDIR "/src/OOdotNet"
RUN dotnet build "OOdotNet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OOdotNet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OOdotNet.dll"]
