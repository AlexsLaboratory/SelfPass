FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SelfPass.Auth/SelfPass.Auth.csproj", "SelfPass.Auth/"]
RUN dotnet restore "SelfPass.Auth/SelfPass.Auth.csproj"
COPY . .
WORKDIR "/src/SelfPass.Auth"
RUN dotnet build "SelfPass.Auth.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SelfPass.Auth.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SelfPass.Auth.dll"]
