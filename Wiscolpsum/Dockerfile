FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Wiscolpsum/Wiscolpsum.csproj", "Wiscolpsum/"]
RUN dotnet restore "Wiscolpsum/Wiscolpsum.csproj"
COPY . .
WORKDIR "/src/Wiscolpsum"
RUN dotnet build "Wiscolpsum.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Wiscolpsum.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Wiscolpsum.dll"]