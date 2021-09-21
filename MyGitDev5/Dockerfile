#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["MyGitDev5/MyGitDev5.csproj", "MyGitDev5/"]
RUN dotnet restore "MyGitDev5/MyGitDev5.csproj"
COPY . .
WORKDIR "/src/MyGitDev5"
RUN dotnet build "MyGitDev5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyGitDev5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyGitDev5.dll"]