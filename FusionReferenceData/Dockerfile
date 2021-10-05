#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["FusionReferenceData/FusionReferenceData.csproj", "FusionReferenceData/"]
RUN dotnet restore "FusionReferenceData/FusionReferenceData.csproj"
COPY . .
WORKDIR "/src/FusionReferenceData"
RUN dotnet build "FusionReferenceData.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FusionReferenceData.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FusionReferenceData.dll"]
