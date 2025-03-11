# TẠO TRANG ĐĂNG NHẬP ỨNG DỤNG SPRINGBOOT VỚI WSO2 
## GIỚI THIỆU 
- Sử dụng **OpenID Connect (OIDC)** làm giao thức xác thực để tích hợp giữa ứng dụng Spring Boot và WSO2 Identity Server
OpenID Connect là một lớp xác thực xây dựng trên OAuth 2.0, cung cấp khả năng xác thực người dùng và trao đổi thông tin nhận dạng (identity) một cách an toàn.
WSO2 Identity Server hỗ trợ OIDC như một giao thức mặc định, và nó thường được sử dụng khi bạn cần xác thực người dùng (authentication) cùng với quyền truy cập tài nguyên (authorization).

## Quy trình làm việc 
- Khi người dùng truy cập ``` http://localhost:8080/login ``` , Spring Boot sẽ chuyển hướng đến trang đăng nhập của ``` WSO2 ``` qua endpoint ``` authorization-uri ```.
- Sau khi người dùng đăng nhập, WSO2 trả về một ID Token (một loại JWT) cùng với Access Token, đây là đặc trưng của OIDC.
- Spring Boot sử dụng thông tin này để xác thực người dùng và hiển thị trang home.
  
## Cài đặt WSO2
#### Cài đặt WSO2 
- Cài đặt WSO2 tại trang ```https://wso2.com/ ```
- Chạy WSO2 Identity Server:
  ```
  cd ~/wso2is/wso2is-<version>/bin
  ./wso2server.sh
  ```
- Truy cập vào giao diện quản lý ```https://localhost:9443/carbon ``` với tài khoản mặc định:
  + Username: admin
  + Password: admin

  ![image](https://github.com/user-attachments/assets/37bca68d-30b7-4ae7-acb5-041279d13768)

#### Thêm ứng dụng vào WSO2 
- Tại mục Application, chọn ``` New Application ``` và thêm ứng dụng mới 
  ![image](https://github.com/user-attachments/assets/013a2f1d-88de-407b-b820-b2a0d2660336)
- Vào mục ``` Protocol ``` của ứng dụng vừa tạo để lưu ``` clientID ``` và ```client secret```
  ![image](https://github.com/user-attachments/assets/0c8cdbe8-c25e-4004-b053-32565c401848)
- Cấu hình thư mục application properties theo mã vừa lưu
  ```
  spring.security.oauth2.client.registration.wso2.client-id=S0sw95ESZYWz4y99aKei_EpetkAa
  spring.security.oauth2.client.registration.wso2.client-secret=F0RznwZ16yl85RT8QN0fbECyYfdON7BfZ6VFTx4O4pIa
  spring.security.oauth2.client.registration.wso2.scope=openid,email,profile
  spring.security.oauth2.client.registration.wso2.authorization-grant-type=authorization_code
  spring.security.oauth2.client.registration.wso2.redirect-uri=http://localhost:8080/login/oauth2/code/wso2
  spring.security.oauth2.client.provider.wso2.issuer-uri=https://localhost:9443/oauth2/token
  spring.security.oauth2.client.provider.wso2.authorization-uri=https://localhost:9443/oauth2/authorize
  spring.security.oauth2.client.provider.wso2.token-uri=https://localhost:9443/oauth2/token
  spring.security.oauth2.client.provider.wso2.user-info-uri=https://localhost:9443/oauth2/userinfo
  spring.security.oauth2.client.provider.wso2.jwk-set-uri=https://localhost:9443/oauth2/jwks
  spring.security.oauth2.client.provider.wso2.user-name-attribute=sub
  server.port=8080
```

