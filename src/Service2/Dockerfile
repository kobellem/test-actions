#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-focal AS base

ENV ASPNETCORE_URLS="http://0.0.0.0:5000"
EXPOSE 5000

RUN adduser --system --disabled-password user

WORKDIR /app
USER user

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-focal AS publish
WORKDIR /src
COPY ./src /src
RUN dotnet publish Service2/Service2.csproj -c Release -r linux-x64 -o /publish

FROM base AS final

COPY --from=publish /publish /app

ENTRYPOINT ["dotnet", "Service2.dll"]
