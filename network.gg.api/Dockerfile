# build stage
FROM mcr.microsoft.com/dotnet/sdk:6.0-focal AS build
WORKDIR /src
COPY . .

RUN dotnet restore "./network.gg.api.csproj" --disable-parallel
RUN dotnet publish "./network.gg.api.csproj" -c release -o /app --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:6.0-focal
RUN apt-get update
RUN apt-get install -y iputils-ping iproute2 inetutils-traceroute
WORKDIR /app
COPY --from=build /app .

ENTRYPOINT ["dotnet", "network.gg.api.dll"]
