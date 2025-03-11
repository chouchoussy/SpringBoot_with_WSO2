# TẠO TRANG ĐĂNG NHẬP ỨNG DỤNG SPRINGBOOT VỚI WSO2 

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

