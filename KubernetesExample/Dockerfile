FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["KubernetesExample/KubernetesExample.csproj", "KubernetesExample/"]

RUN dotnet restore "KubernetesExample/KubernetesExample.csproj"
COPY . .
WORKDIR "/src/KubernetesExample"
RUN dotnet build "KubernetesExample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KubernetesExample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KubernetesExample.dll"]