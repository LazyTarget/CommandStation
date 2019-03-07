FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["CommandStation.Web/CommandStation.Web.csproj", "CommandStation.Web/"]
RUN dotnet restore "CommandStation.Web/CommandStation.Web.csproj"
COPY . .
WORKDIR "/src/CommandStation.Web"
RUN dotnet build "CommandStation.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CommandStation.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CommandStation.Web.dll"]