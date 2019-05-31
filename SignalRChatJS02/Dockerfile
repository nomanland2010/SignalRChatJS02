FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SignalRChat/SignalRChatJS02.csproj", "SignalRChat/"]
RUN dotnet restore "SignalRChat/SignalRChatJS02.csproj"
COPY . .
WORKDIR "/src/SignalRChat"
RUN dotnet build "SignalRChatJS02.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SignalRChatJS02.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SignalRChatJS02.dll"]