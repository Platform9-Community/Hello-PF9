﻿FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 8080
ENV ASPNETCORE_URLS="http://+:8080"

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY [".", "Hello-PF9/"]
RUN dotnet restore "Hello-PF9/Hello-PF9.csproj"
COPY . .
WORKDIR "/src/Hello-PF9"
RUN dotnet build "Hello-PF9.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hello-PF9.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hello-PF9.dll"]
