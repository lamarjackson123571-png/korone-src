FROM ://microsoft.com AS build-env
WORKDIR /app

# Copy everything and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy remaining source files and build production release
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM ://microsoft.com
WORKDIR /app
COPY --from=build-env /app/out .

ENV ASPNETCORE_URLS=http://+:3000
EXPOSE 3000

ENTRYPOINT ["dotnet", "Api.dll"]
