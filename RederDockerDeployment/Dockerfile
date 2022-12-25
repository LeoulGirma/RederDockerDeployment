FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["RederDockerDeployment.csproj", "./"]
RUN dotnet restore "./RederDockerDeployment.csproj"
COPY . .
RUN dotnet build "RederDockerDeployment.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "RederDockerDeployment.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RederDockerDeployment.dll"]

#RUN ["apt-get", "update"]
#RUN ["apt-get", "install", "-y", "openssh-server"]
#RUN ["apt-get", "install", "-y", "nano"]
#RUN echo 'root:lollol0' | chpasswd
#RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
#RUN ["/etc/init.d/ssh", "start"]

#EXPOSE 22