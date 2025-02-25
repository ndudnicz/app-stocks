# docker build --no-cache -t api . && docker run -p 5000:5000 api

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /
RUN git clone https://github.com/ndudnicz/api-stocks.git App
WORKDIR /App
RUN dotnet restore
RUN dotnet publish -o out
COPY ./*.json ./out/

FROM mcr.microsoft.com/dotnet/aspnet:9.0
WORKDIR /App
COPY --from=build /App/out .
EXPOSE 5000
ENV ASPNETCORE_URLS=http://+:5000
ENTRYPOINT ["dotnet", "dotnet-api.dll"]