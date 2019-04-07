FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-stretch AS build
WORKDIR /src
COPY ["zubedotcom/zubedotcom.csproj", "zubedotcom/"]
RUN dotnet restore "zubedotcom/zubedotcom.csproj"
COPY . .
WORKDIR "/src/zubedotcom"
RUN dotnet build "zubedotcom.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "zubedotcom.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "zubedotcom.dll"]