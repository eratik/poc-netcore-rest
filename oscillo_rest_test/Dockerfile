#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["oscillo_rest_test/oscillo_rest_test.csproj", "oscillo_rest_test/"]
RUN dotnet restore "oscillo_rest_test/oscillo_rest_test.csproj"
COPY . .
WORKDIR "/src/oscillo_rest_test"
RUN dotnet build "oscillo_rest_test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "oscillo_rest_test.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "oscillo_rest_test.dll"]
