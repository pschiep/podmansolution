#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebAPI2/WebAPI2.csproj", "WebAPI2/"]
RUN dotnet restore "WebAPI2/WebAPI2.csproj"
COPY . .
WORKDIR "/src/WebAPI2"
RUN dotnet build "WebAPI2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAPI2.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAPI2.dll"]