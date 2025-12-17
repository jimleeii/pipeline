# Build stage
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

# Restore
COPY ["csharp.csproj", "/src/"]
RUN dotnet restore "/src/csharp.csproj"

# Build + publish
COPY . /src
RUN dotnet publish "/src/csharp.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Runtime stage (console app)
FROM mcr.microsoft.com/dotnet/runtime:10.0 AS final
WORKDIR /app

# Create non-root user
RUN groupadd --system --gid 1001 appgroup && \
    useradd --system --uid 1001 --gid appgroup --shell /bin/false appuser

# Copy published app   
COPY --from=build /app/publish .

# Switch to non-root user
USER appuser

ENTRYPOINT ["dotnet", "csharp.dll"]
