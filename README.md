# Golang
## Lịch sử ra đời
- Ngôn ngữ Go ban đầu được thiết kế và phát triển bởi một nhóm kĩ sư Google bao gồm Robert Griesemer, Ken Thompson và Rob Pike vào năm 2007. 
- Sau đó Go lần đầu tiên được giới thiệu vào tháng 11 năm 2009 và phiên bản đầu tiên của nó được phát hành vào tháng 12 năm 2012.

## Điểm mạnh và yếu của Go so với các ngôn ngữ khác
- 

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
    - Variadic Function: Là hàm có thể truyền vào tùy ý số lượng các tham số sử dụng syntax `...`, tham số sử dụng `...` phải là tham số cuối.
        ```
        func sum(elems ...int) int {
            sum := 0
            for _, v := range elems {
                sum += v
            }
            return sum
        }
        ```
    - Cả tham số và giá trị trả về trao đổi dữ liệu với hàm theo cách truyền vào giá trị (pass by value).
    - Sử dụng câu lệnh `defer` để trì hoãn việc thực thi hàm cho tới khi hàm bao ngoài nó return.
        ```
        func main() {
            defer fmt.Println("world")
            fmt.Println("hello")
        }
        // kết quả: hello world
        ```
    - Mỗi lời gọi `defer` sẽ được push vào stack và được thực thi theo thứ tự LIFO (Last in first out). Ta thường sử dụng defer cho việc đóng hoặc giải phóng tài nguyên.

4. For loop
    - Trong Go, vòng `for` gồm 3 phần:
        - `Init statement`: Được thực thi trước khi bắt đầu vòng lặp đầu tiên.
        - `Condition expression`: Được đánh giá trước mỗi vòng lặp.
        - `Post statement`: Được thực thi vào cuối mỗi vòng lặp.
        ```
        sum := 0
        for i := 0; i < 10; i++ {
		    sum += i
	    }
        ```
    - `Init statement` và `Post statement` có thể được lược bỏ (while trong go)
        ```
        sum := 1
        for sum < 1000 {
		    sum += sum
	    }
        ```

5. Structs
    - `Struct` trong Go là một tập hợp các trường, các thuộc tính.
        ```
        type User struct {
	        Id       int    
	        Name     string 
	        Email    string 
	        Password string 
	        Phone    string 
	        Gender   string 
        }
        ```
    - Khởi tạo `struct`:
        ```
        u := User{
            Id:       1,
            Name:     "John Doe",
            Email:    "johndoe@gmail.com",
            Password: "123456",
            Phone:    "13800138000",
            Gender:   "male",
        }
        ```
6. Array
    - Là một dãy có độ dài cố định chứa các phần tử có cùng kiểu dữ liệu.
    - Cách khai báo một array
        ```
        ar := [6]int{1, 2, 3, 4, 5, 6}
        ```
    - Sử dụng vòng `for range` để duyệt qua tất cả các phần tử trong 1 `array`:
        ```
        for i, v := range ar {
		    fmt.Println(i, v)
	    }
        ```
        Trong đó biến đầu tiên (i) là index của phần tử trong array, còn biến thứ hai (v) là một bản copy giá trị của phần tử tại index đó.

7. Slices
    - Slice là một kiểu cấu trúc dữ liệu động, có thể thay đổi kích thước, được xây dựng trên mảng (array).
    - Cấu trúc của slice:
        - `Pointer`: Con trỏ đến underlying array.
        - `Len`: Độ dài của slice.
        - `Capacity`: Sức chứa tối đa của slice.
    - Khi thay đổi giá trị của phần tử trong slice thì cũng sẽ làm thay đổi giá trị của phần tử trong underlying array.
    - Có thể sử dụng `for ... range` để duyệt qua các phần tử trong array.
    - Sử dụng hàm `len()` để xem độ dài và hàm `cap()` để xem sức chứa tối đa của slice.
    - Khai báo một slice 
        ```
        // Slice with len = 3 and cap = 3
	    a := []int{1, 2, 3}

	    // Slice with len = 3 and cap = 6
	    b := make([]int, 3, 6)

        // Make a slice from array
	    ar := []int{1, 2, 3}
	    c := ar[1:3]
        ```
    - Sử dụng hàm `append` để thêm phần tử vào cuối slice
        ```
        // Add elements to a slice
	    a := []int{1, 2, 3, 4, 5, 6}
	    a = append(a, 4)
        ```
    - Trong trường hợp slice ban đầu không đủ sức chứa khi thêm vào phần tử, hàm append sẽ hiện thực cấp phát lại vùng nhớ có kích thước:
        - Nếu kích thước cũ (cap) < 1024: cấp phát gấp đôi (x2) vùng nhớ cũ.
        - Nếu kích thước cũ >= 1024: cấp phát 1.25x vùng nhớ cũ.
    
        Sau đó, dữ liệu cũ sẽ được sao chép sang.

8. Map
    - `Map` là một kiểu dữ liệu dùng để lưu trữ các cặp `key - value`
        ```
        // Initialize a map
	    m := make(map[string]int)

	    // Add or update an element
	    m["1"] = 1
	    m["1"] = 2

	    // Delete an element
	    delete(m, "1")

	    // Check for key existence and retrieve value
	    v, ok := m["1"]
        ```
9. Method
    - Go không có class, tuy nhiên chúng ta có thể định nghĩa các phương thức (Method) cho type (kiểu).
    - Phương thức là một hàm với đối số (argument) đặc biệt gọi là receiver.
    - Chỉ có thể thêm phương thức cho các kiểu được định nghĩa trong cùng một package.
        ```
        type Rectangle struct {
	        width  int
	        height int
        }

        // Value receiver method
        func (r Rectangle) area() int {
	        return r.width * r.height
        }

        // Pointer receiver method
        func (r *Rectangle) setWidth(width int) {
            r.width = width
        }
        ```
    - Với value receiver, method sẽ thực hiện trên một bản copy của dữ liệu gốc.
    - Để thay đổi giá trị của dữ liệu gốc, ta cần sử dụng pointer receiver.

10. Interface
    - Interface là một tập hợp các phương thức (methods). Interface cho phép chúng ta định nghĩa hành vi của các đối tượng mà không cần quan tâm đến implementation cụ thể của chúng.
    - Cú pháp để định nghĩa một interface trong Go
        ```
        type Shape interface {
            area() float64
            perimeter() float64
        }
        ```
    - Trong Go, interface được implement một cách ngầm định. Điều này có nghĩa là một kiểu dữ liệu tự động thỏa mãn một interface nếu nó implement tất cả các phương thức mà interface đó yêu cầu.
        ```
        type Shape interface {
	        area() float64
	        perimeter() float64
        }

        type Rectangle struct {
	        width, height float64
        }

        func (r Rectangle) area() float64 {
	        return r.width * r.height
        }

        func (r Rectangle) perimeter() float64 {
	        return 2*r.width + 2*r.height
        }

        func PrintArea(shape Shape) {
	        fmt.Println(shape.area())
        }

        func main() {
	        r := Rectangle{width: 10, height: 5}
	        PrintArea(r)
        }
        ```
    - Interface mà không định nghĩa bất kỳ một method nào được gọi là `empty interface`, `interface{}`. `Empty interface` có thể chứa giá trị của bất kỳ kiểu nào và thường được dùng để xử lý các giá trị mà không biết kiểu của nó là gì.
    - `Type assertion` trong Go là một cơ chế cho phép truy cập giá trị của một kiểu (type) cụ thể bên trong interface.
        ```
        func IsRectangle(shape Shape) {
	        //Type assertion
	        rec, ok := shape.(Rectangle)
	        if ok {
		        fmt.Printf("This is an rectangle with width = %f and height = %f\n", rec.width, rec.height)
	        } else {
		        fmt.Println("This is not a rectangle")
	        }
        }
        ```
    - Chúng ta có thể dùng `Type Switch` để thực hiện liên tiếp nhiều `type assertion`
        ```
        func checkType(i interface{}) {
	        switch _ := i.(type) {
	        case int:
		        fmt.Println("int")
	        case float64:
		        fmt.Println("float64")
	        case string:
		        fmt.Println("string")
	        default:
		        fmt.Println("unknown type")
            }
	    }
        ```
    - Không nên dùng cả value receiver và pointer receiver trên cùng một kiểu (type) trong Go.
    - Trong Go, nếu một kiểu `T` implement một interface với value receiver (`T`) thì cả `T` và `*T` đều implement interface này. Ngược lại, nếu kiểu `T` implement một interface với pointer receiver thì chỉ có `*T` implement interface. Vậy nên việc sử dụng cả hai loại receiver có thể gây nhầm lẫn về việc kiểu nào thực sự thực thi interface.

11. Error handling
    - Trong Go, cơ chế xử lí lỗi sẽ dựa vào giá trị lỗi trả về của hàm.
    - Kiểu `error` là một `interface`
      ```
      type error interface {
          Error() string
      }
      ```
    - Hàm (function) có thể trả về một error, code gọi đến hàm này sẽ phải handle error này bằng cách xem nó có giá trị `nil` hay không.
      ```go
      i, err := strconv.Atoi("4")
      if err != nil {
          fmt.Printf("couldn't convert number: %v\n", err)
      }
      fmt.Println("Converted integer:", i)
      ```
    - Có thể tạo một `error` mới với static string bằng cách sử dụng `errors.New()` và có thể sử dụng `errors.Is()` để check error loại này.
    ```go
    // package foo

    var ErrCouldNotOpen = errors.New("could not open")

    func Open() error {
        return ErrCouldNotOpen
    }

    // package bar

    if err := foo.Open(); err != nil {
        if errors.Is(err, foo.ErrCouldNotOpen) {
        // handle the error
        } else {
            panic("unknown error")
        }
    }
    ```
    - Có thể tạo một custom error bằng cách implement Error interface và sử dụng `errors.As()` để xác định kiểu của `error`.
    ```go
    // package foo

    type NotFoundError struct {
        File string
    }

    func (e *NotFoundError) Error() string {
        return fmt.Sprintf("file %q not found", e.File)
    }

    func Open(file string) error {
        return &NotFoundError{File: file}
    }


    // package bar

    if err := foo.Open("testfile.txt"); err != nil {
        var notFound *NotFoundError
        if errors.As(err, &notFound) {
        // handle the error
        } else {
            panic("unknown error")
        }
    }
    ```

12. Naming Convention
    - Package
        - Tên package nên ngắn gọn, thường là một từ, viết bằng chữ thường không có gạch dưới hoặc chữ hoa xen kẽ.
        - Tên package nên mô tả chính xác chức năng hoặc mục đích của nó.
        - Tránh sử dụng các tên package phổ biến để tránh xung đột khi import.
        - Ví dụ: time, http, strings.
    - Biến, struct và hàm
        - Sử dụng camelCase cho tên biến và hàm không export.
        ```go
        var someVariable string
        func doSomething() {}
        ```
        - Sử dụng PascalCase cho tên biến và hàm được export.
        ```go
        var SomeVariable string
        func DoSomething() {}
        ```
        - Tên nên ngắn gọn nhưng có ý nghĩa, đủ để mô tả chức năng hoặc dữ liệu mà chúng nắm giữ.
      - Interface
        - Sử dụng PascalCase với hậu tố "-er" cho interface mô tả hành vi: Reader, Writer, Formatter

13. Multithreading
    - Xử lý đồng thời (concurrency)
    

    



    
