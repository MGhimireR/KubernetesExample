FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app



FROM mcr.microsoft.com/dotnet/sdk:5.0-alpine AS build
WORKDIR /src
COPY ["KubernetesExample.csproj", "/src"]  #ADD


RUN dotnet restore "KubernetesExample.csproj"  # Restoring Dependencies
COPY . .

RUN dotnet build "KubernetesExample.csproj" -c Release -o /app/build   #Building Application

FROM build AS publish
RUN dotnet publish "KubernetesExample.csproj" -c Release -o /app/publish  #Publishing Application 


FROM base AS final
ENV ASPNETCORE_URLS http://*:5000


WORKDIR /app
COPY --from=publish /app/publish .
EXPOSE 5000
ENTRYPOINT ["dotnet", "KubernetesExample.dll"] #CMD