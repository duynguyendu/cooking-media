FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["CookingMedia.Api/CookingMedia.Api.csproj", "CookingMedia.Api/"]
RUN dotnet restore "CookingMedia.Api/CookingMedia.Api.csproj"
COPY . .
WORKDIR "/src/CookingMedia.Api"
RUN dotnet build "CookingMedia.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CookingMedia.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CookingMedia.Api.dll"]
