FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["hic.parkingservice/hic.parkingservice.csproj", "hic.parkingservice/"]
RUN dotnet restore "hic.parkingservice/hic.parkingservice.csproj"
COPY . .
WORKDIR "/src/hic.parkingservice"
RUN dotnet build "hic.parkingservice.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "hic.parkingservice.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "hic.parkingservice.dll"]