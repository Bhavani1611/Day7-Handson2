#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

##FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443

#FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
#WORKDIR /src
#COPY ["Day7-2ndHandson/Day7-2ndHandson.csproj", "Day7-2ndHandson/"]
#RUN dotnet restore "Day7-2ndHandson/Day7-2ndHandson.csproj"
#COPY . .
#WORKDIR "/src/Day7-2ndHandson"
#RUN dotnet build "Day7-2ndHandson.csproj" -c Release -o /app/build

#FROM build AS publish
#RUN dotnet publish "Day7-2ndHandson.csproj" -c Release -o /app/publish#

#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "Day7-2ndHandson.dll"] */

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env

WORKDIR /app

# Copy csproj and restore as distinct layers

COPY *.csproj ./

RUN dotnet restore

# Copy everything else and build

COPY . ./

RUN dotnet publish -c Release -o out

# Build runtime image

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2

WORKDIR /app

COPY --from=build-env /app/out .

ENTRYPOINT ["dotnet", "Day7-2ndHandson.dll"]