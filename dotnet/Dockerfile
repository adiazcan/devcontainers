FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["dotnet.csproj", "./"]
RUN dotnet restore "dotnet.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "dotnet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
RUN apt-get update 
RUN apt-get install -y --no-install-recommends apt-utils 
RUN apt-get install -y curl unzip procps
RUN curl -sSL https://aka.ms/getvsdbgsh | bash /dev/stdin -v latest -l /app/publish/vsdbg;
ENTRYPOINT ["dotnet", "dotnet.dll"]
