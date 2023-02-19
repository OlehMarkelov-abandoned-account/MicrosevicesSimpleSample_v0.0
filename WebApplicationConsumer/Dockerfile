#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 5001

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WebApplicationConsumer/WebApplicationConsumer.csproj", "WebApplicationConsumer/"]
RUN dotnet restore "WebApplicationConsumer/WebApplicationConsumer.csproj"
COPY . .
WORKDIR "/src/WebApplicationConsumer"
RUN dotnet build "WebApplicationConsumer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplicationConsumer.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplicationConsumer.dll"]