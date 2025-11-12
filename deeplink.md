<img width="959" height="336" alt="Pasted Graphic 1" src="https://github.com/user-attachments/assets/86808788-6a06-45e7-93c9-ba2952eabde4" /># **Deep Link in Flutter**

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
<img width="732" height="209" alt="sintent-filter androidautoVerify=true" src="https://github.com/user-attachments/assets/27889b15-16f4-461c-8065-0ed52f726889" />

<img width="539" height="85" alt="androidname=flutter_deeplinking_enabled" src="https://github.com/user-attachments/assets/ce56a27a-9096-48b7-b35a-839a8152da96" />

￼
---

### **2. assetlinks.json**
￼ <img width="959" height="336" alt="Pasted Graphic 1" src="https://github.com/user-attachments/assets/c9e09bc2-be54-40cf-8f14-dad5c0edac95" />

- **package_name** phải trùng với `applicationId` ở `app/build.gradle`  
<img width="440" height="381" alt="compileSdkVersion 36" src="https://github.com/user-attachments/assets/7604957f-5297-4c80-b4f1-d5aebf7c0c65" />

- **sha256:**  
  Có thể lấy từ trên store nếu app đã được đăng trên **CH Play**,
  <img width="1816" height="900" alt="App integrity" src="https://github.com/user-attachments/assets/72258854-c7d0-4778-9144-cfbabfe61eb8" />

  hoặc nếu app ở local thì chạy lệnh sau để lấy ra:
  ```bash
  keytool -list -v -keystore ~/.android/debug.keystore \
  -alias androiddebugkey -storepass android -keypass android

### **3. Kiểm tra liên kết hoạt động (Supported Links)**

- Nếu đã setup **thành công**, trong **phần Cài đặt của ứng dụng → App Info → Supported links**  
  sẽ hiển thị **domain** được cấu hình, và **người dùng không thể bật/tắt thủ công**.

- Nếu **liên kết vẫn có thể bật/tắt thủ công**, nghĩa là quá trình setup **có lỗi** ở một trong các bước sau:
  - File **`assetlinks.json`** trên server chưa đúng hoặc chưa public.
  - File **SHA256** không khớp với key signing của ứng dụng.
  - **`applicationId`** trong `build.gradle` không trùng với **`package_name`** trong file `assetlinks.json`.

- Một số tài liệu cho rằng khi build **debug**, phần **Active links** có thể cần **kích hoạt thủ công**:  
  👉 [https://docs.flutter.dev/cookbook/navigation/set-up-app-links](https://docs.flutter.dev/cookbook/navigation/set-up-app-links)

---

### **4. Kiểm tra hoạt động Deep Link**

## **Cách 1: Sử dụng lệnh ADB**
Chạy lệnh sau trong terminal để kiểm tra deep link có mở đúng app hay không:
```bash
adb shell am start -a android.intent.action.VIEW \
    -c android.intent.category.BROWSABLE \
    -d "https://api.easyposs.vn/payment?traceid=1234567" \
    vn.softdreams.easy_pos## **Cách 1: Mở trực tiếp trên trình duyệt
Dán URL lên thanh địa chỉ trình duyệt:

arduino
Sao chép mã
https://api.easyposs.vn/payment?traceid=1234567
Khi deep link được gọi từ một ứng dụng khác, bản chất là web sẽ mở liên kết này,
sau đó Android/iOS sẽ dựa vào file cấu hình trong thư mục .well-known để xác định có mở app hay không.

5. Cách hoạt động khi mở app qua Deep Link
Khi người dùng nhấn vào deep link, hệ thống sẽ kiểm tra domain trong file cấu hình .well-known.
Nếu domain hợp lệ và app được cài đặt, hệ thống sẽ mở app thay vì mở trong trình duyệt.

Ứng dụng sẽ khởi tạo lại từ đầu nếu đang ở trạng thái terminated,
hoặc chỉ gọi callback của deep link nếu app đang chạy nền hoặc đang mở.

Việc điều hướng đến màn hình nào phụ thuộc vào thư viện quản lý route bạn sử dụng.

6. Điều hướng trong Flutter (sử dụng GetX)
Với GetX, framework sẽ tự động parse URL để tìm routeName tương ứng.
Ví dụ:

arduino
Sao chép mã
https://api.easyposs.vn/payment?traceid=1234567
👉 GetX sẽ tìm màn hình có routeName = /payment?traceid=1234567.

Nếu không tìm thấy màn hình phù hợp, GetX sẽ fallback về route gốc /,
tức là app sẽ không điều hướng đến màn hình nào cả.

⚠️ Lưu ý:
Không nên đăng ký màn hình có routeName trùng với /,
vì nếu deep link không match với route nào, màn / sẽ bị gọi mặc định,
dẫn đến hành vi không đúng mong muốn
