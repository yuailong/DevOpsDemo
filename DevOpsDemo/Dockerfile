FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DevOpsDemo/DevOpsDemo.csproj", "DevOpsDemo/"]
RUN dotnet restore "DevOpsDemo/DevOpsDemo.csproj"
COPY . .
WORKDIR "/src/DevOpsDemo"
RUN dotnet build "DevOpsDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DevOpsDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DevOpsDemo.dll"]