FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY MilkMatch/MilkMatch.csproj MilkMatch/
RUN dotnet restore "MilkMatch/MilkMatch.csproj"
COPY . .
WORKDIR "/src/MilkMatch"
RUN dotnet build "MilkMatch.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MilkMatch.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MilkMatch.dll"]
