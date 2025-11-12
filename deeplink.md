# **Deep Link in Flutter**

---

## **Tổng quan**
Bất cứ ứng dụng nào trên Android và iOS khi được tải về thì chúng đều tự động tải những file cấu hình được lưu trên web và xác thực với ứng dụng hiện tại:

- **Android:**  
  👉 [https://api.easyposs.vn/.well-known/assetlinks.json](https://api.easyposs.vn/.well-known/assetlinks.json)

- **iOS:**  
  👉 [https://api.easyposs.vn/.well-known/apple-app-site-association](https://api.easyposs.vn/.well-known/apple-app-site-association)

---

## **Tài liệu tham khảo**
- [http://codewithandrea.com/articles/flutter-deep-links/#anatomy-of-a-deep-link](http://codewithandrea.com/articles/flutter-deep-links/#anatomy-of-a-deep-link)  
- [https://stackoverflow.com/a/42290810](https://stackoverflow.com/a/42290810)

---

## **Android**

### **1. Setup domain trong AndroidManifest**
*(Hình minh họa hoặc code mẫu AndroidManifest.xml tại đây)*  
￼  
￼

---

### **2. assetlinks.json**
￼  
- **package_name** phải trùng với `applicationId` ở `app/build.gradle`  
￼  

- **sha256:**  
  Có thể lấy từ trên store nếu app đã được đăng trên **CH Play**,  
  hoặc nếu app ở local thì chạy lệnh sau để lấy ra:
  ```bash
  keytool -list -v -keystore ~/.android/debug.keystore \
  -alias androiddebugkey -storepass android -keypass android
