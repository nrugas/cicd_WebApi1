FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["cicd_WebApi1/cicd_WebApi1.csproj", "cicd_WebApi1/"]
RUN dotnet restore "cicd_WebApi1/cicd_WebApi1.csproj"
COPY . .
WORKDIR "/src/cicd_WebApi1"
RUN dotnet build "cicd_WebApi1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "cicd_WebApi1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "cicd_WebApi1.dll"]