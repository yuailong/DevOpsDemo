FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY . .
RUN dotnet restore "DevOpsDemo/DevOpsDemo.csproj"
WORKDIR "/src/DevOpsDemo"
RUN dotnet build "DevOpsDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DevOpsDemo.csproj" -c Release -o /app

FROM microsoft/dotnet:2.1-aspnetcore-runtime AS final
WORKDIR /app
EXPOSE 80
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DevOpsDemo.dll"]