# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy toàn bộ vào /src
COPY . .

# Di chuyển vào thư mục chứa file .csproj để restore và build
# Lưu ý: Vì Dockerfile nằm trong thư mục webAPI, nên đường dẫn lúc này là ./webAPI
RUN dotnet restore "./webAPI/webAPI.csproj"
RUN dotnet publish "./webAPI/webAPI.csproj" -c Release -o /app/out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/out .

# Render thường yêu cầu port 10000 hoặc tự gán, cấu hình này của bạn đã ổn
ENV ASPNETCORE_URLS=http://+:10000
EXPOSE 10000

ENTRYPOINT ["dotnet", "webAPI.dll"]
