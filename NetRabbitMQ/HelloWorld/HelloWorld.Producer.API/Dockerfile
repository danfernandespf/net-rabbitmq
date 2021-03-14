#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["HelloWorld/HelloWorld.Producer.API/HelloWorld.Producer.API.csproj", "HelloWorld/HelloWorld.Producer.API/"]
RUN dotnet restore "HelloWorld/HelloWorld.Producer.API/HelloWorld.Producer.API.csproj"
COPY . .
WORKDIR "/src/HelloWorld/HelloWorld.Producer.API"
RUN dotnet build "HelloWorld.Producer.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloWorld.Producer.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloWorld.Producer.API.dll"]