FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WorkApi/WorkApi.csproj", "WorkApi/"]
RUN dotnet restore "WorkApi/WorkApi.csproj"
COPY . .
WORKDIR "/src/WorkApi"
RUN dotnet build "WorkApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WorkApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WorkApi.dll"]
