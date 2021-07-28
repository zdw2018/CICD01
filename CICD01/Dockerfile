#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CICD01/CICD01.csproj", "CICD01/"]
RUN dotnet restore "CICD01/CICD01.csproj"
COPY . .
WORKDIR "/src/CICD01"
RUN dotnet build "CICD01.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CICD01.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CICD01.dll"]