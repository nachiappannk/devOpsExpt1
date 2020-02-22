FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["SampleApplication/SampleApplication.csproj", "SampleApplication/"]
RUN dotnet restore "SampleApplication/SampleApplication.csproj"
COPY . .
WORKDIR "/src/SampleApplication"
RUN dotnet build "SampleApplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SampleApplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SampleApplication.dll"]