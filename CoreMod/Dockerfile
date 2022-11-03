FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CoreMod/CoreMod.csproj", "CoreMod/"]
RUN dotnet restore "CoreMod/CoreMod.csproj"
COPY . .
WORKDIR "/src/CoreMod"
RUN dotnet build "CoreMod.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CoreMod.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CoreMod.dll"]
