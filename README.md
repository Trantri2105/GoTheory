# Golang
## Lịch sử ra đời
- Ngôn ngữ Go ban đầu được thiết kế và phát triển bởi một nhóm kĩ sư Google bao gồm Robert Griesemer, Ken Thompson và Rob Pike vào năm 2007. 
- Sau đó Go lần đầu tiên được giới thiệu vào tháng 11 năm 2009 và phiên bản đầu tiên của nó được phát hành vào tháng 12 năm 2012.

## Điểm mạnh và yếu của Go so với các ngôn ngữ khác

## Go được dùng để lập trình các ứng dụng như thế nào

## Chi tiết về Go
1. Package
    - Mọi chương trình trong Go đều được tạo nên bởi các package. Mỗi file đều thuộc một package.
    - Theo quy chuẩn, tên của package sẽ trùng với tên thư mục chứa package đó.
    - Để sử dụng các chức năng từ một package khác, chúng ta cần phải import path của package đó vào file của mình, cú pháp:
        ```
        // Import 1 package
        import "package"

        // Import nhiều package
        import (
            "package_1"
            "package_2"
        )
        ```
    - Hàm, biến và các kiểu dữ liệu trong Go sẽ có thể sử dụng trong các package khác nếu (exported) nếu viết hoa chữ cái đầu.
    - Các biến và hàm không được export sẽ chỉ có thể sử dụng bên trong package của nó.
    - Package `main` được sử dụng để chứa hàm `main()` dùng để thực thi chương trình.

2. Go modules
    - Go Modules là hệ thống quản lý các dependencies của go.
    - Module là tập hợp của các package trong go với file `go.mod` ở thư mục gốc.
    - File `go.mod` sẽ chứa path của module, các dependencies cần thiết để module đó chạy thành công.
        ```
        module SchoolManagement

        go 1.22

        require (
	        github.com/gin-gonic/gin v1.10.0
	        github.com/go-kit/kit v0.13.0
	        github.com/go-playground/validator/v10 v10.23.0
	        github.com/golang-jwt/jwt v3.2.2+incompatible
	        github.com/jmoiron/sqlx v1.4.0
	        github.com/joho/godotenv v1.5.1
	        github.com/lib/pq v1.10.9
	        github.com/redis/go-redis/v9 v9.7.0
	        golang.org/x/crypto v0.29.0
        )

        require (
	        github.com/bytedance/sonic v1.12.5 // indirect
	        github.com/bytedance/sonic/loader v0.2.1 // indirect
	        github.com/cespare/xxhash/v2 v2.2.0 // indirect
	        github.com/cloudwego/base64x v0.1.4 // indirect
            ....
	        golang.org/x/sys v0.27.0 // indirect
	        golang.org/x/text v0.20.0 // indirect
	        google.golang.org/protobuf v1.35.2 // indirect
	        gopkg.in/yaml.v3 v3.0.1 // indirect
        )
        ```
    - Khởi tạo một module trong go sử dụng câu lệnh
        ```
        go mod init module_name
        ```
    - Khi câu lệch chạy thành công, file `go.mod` sẽ tự động được tạo tại gốc của thư mục và sẽ quản lý toàn bộ dependencies của module, bao gồm cả các thư mục con.
    - Sử dụng câu lệnh `go get package_name` để thêm dependency.
    - Sử dụng câu lệnh `go mod tidy` để thêm các dependency còn thiếu trong modules và xóa các dependency không dùng đến.
3. Functions
   - Functions trong Go có thể có nhiều tham số và trả về nhiều dữ liệu:
      ```
     func swap(x, y string) (string, string) {
         return y, x
     }
     ```
   - Dữ liệu trả về có thể được đặt tên, câu lệnh `return` sẽ trả về giá trị của các biến này
      ```
     func split(sum int) (x, y int) {
         x = sum * 4 / 9
         y = sum - x
         return
     }
     ```   
   - Variadic Function: Là hàm có thể truyền vào tùy ý số lượng các tham số sử dụng syntax ..., tham số sử dụng ... phải là tham số cuối.
      ```
     func sum(elems ...int) int {
         sum := 0
         for _, v := range elems {
            sum += v
         }
         return sum
     }
     ```
   
