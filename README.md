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
    - Xử lý đồng thời (concurrency):
        - Xử lý đồng thời là khả năng phân chia và điều phối nhiều tác vụ khác nhau trong cùng một khoảng thời gian và tại một thời điểm chỉ có thể xử lý một tác vụ.
        - Tất cả các chương trình đang chạy trong máy tính chúng ta chạy đều do hệ điều hành quản lý, với mỗi chương trình đang chạy như vậy được gọi là một process (tiến trình) và được cấp một process id (PID) để hệ điều hành dễ dàng quản lí.
        - Các tác vụ của tiến trình sẽ được CPU core (nhân CPU) của máy tính xử lý và tại một thời điểm một nhân CPU chỉ có thể xử lý một tác vụ.
        - Nhân CPU sẽ không đợi xử lý xong một tác vụ rồi mới xử lý tiếp tác vụ khác, mà nhân CPU sẽ chia các tác vụ lớn thành các tác vụ nhỏ hơn và sắp xếp xen kẽ lẫn nhau. 
        - Nhân CPU xẽ tận dụng thời gian rảnh của tác vụ này để đi làm tác vụ khác, một lúc thì làm tác vụ nhỏ này, một lúc khác thì làm tác vụ nhỏ khác.
        - Như vậy chúng ta sẽ cảm thấy máy tính xử lý nhiều việc cùng lúc tại cùng thời điểm. Nhưng bản chất bên dưới nhân CPU thì nó chỉ có thể thực thi một tác vụ nhỏ trong tác vụ lớn tại thời điểm đó.
    - Xử lý song song (parallelism):
        - Xử lý song song là khả năng xử lý nhiều tác vụ khác nhau trong cùng một thời điểm, các tác vụ này hoàn toàn độc lập với nhau. 
        - Xử lý song song chỉ có thể thực hiện trên máy tính có số nhân lớn hơn 1.
        - Thay vì một nhân CPU chúng ta chỉ có thể xử lý một tác vụ nhỏ tại một thời điểm thì khi số nhân CPU có nhiều hơn chúng ta có thể xử lý các tác vụ song song với nhau cùng lúc trên các nhân CPU.
        - Trên mỗi nhân của CPU vẫn xảy ra quá trình xử lý đồng thời miễn là tại một thời điểm không có xảy ra việc xử lý cùng một tác vụ trên hai nhân CPU khác nhau.
    - Thread:
        - Thread là một luồng trong một tiến trình đang chạy.
        - Các thread trong process sẽ được cấp phát riêng một vùng nhớ stack để lưu các biến riêng của thread đó. 
        - Ngoài ra các thread chia sẻ chung vùng nhớ heap của process.
        - Số lượng thread chạy song song trong cùng một thời điểm sẽ bằng với số lượng nhân CPU mà máy tính chúng ta có. Vì vậy khi chúng ta lập trình mà tạo quá nhiều thread thì cũng không có giúp cho chương trình chúng ta chạy nhanh hơn, mà còn gây ra lỗi và làm chậm chương trình.
    - Goroutine
        - Goroutines là một đơn vị concurrency của ngôn ngữ Go, Go sử dụng goroutine để xử lý đồng thời nhiều tác vụ.
        - Việc khởi tạo goroutines sẽ ít tốn chi phí hơn khởi tạo thread so với các ngôn ngữ khác.
        - Goroutine và thread không giống nhau.
        - Đầu tiên, system thread sẽ có một kích thước vùng nhớ stack cố định (thông thường vào khoảng 2MB). Vùng nhớ stack chủ yếu được dùng để lưu trữ những tham số, biến cục bộ và địa chỉ trả về khi chúng ta gọi hàm.
        - Kích thước cố định của stack sẽ dẫn đến hai vấn đề:
            - Stack overflow với những chương trình gọi hàm đệ quy sâu.
            - Lãng phí vùng nhớ đối với chương trình đơn giản.
        - Goroutine giải quyết vấn đề này bằng cách cấp phát linh hoạt vùng nhớ stack:
            - Một Goroutines sẽ được bắt đầu bằng một vùng nhớ nhỏ (khoảng 2KB hoặc 4KB).
            - Khi không gian stack hiện tại là không đủ Goroutines sẽ tự động tăng không gian stack (kích thước tối đa của stack có thể được đạt tới 1GB).
            - Bởi vì chi phí của việc khởi tạo là nhỏ, chúng ta có thể dễ dàng giải phóng hàng ngàn goroutines.
        - Trong các ngôn ngữ lập trình khác thì các thread được quản lý bởi hệ điều hành.
        - Trong Golang sử dụng Go runtime có riêng cơ chế định thời cho Goroutines, nó dùng một số kỹ thuật để ghép M Goroutines trên N thread của hệ điều hành.
        - Cơ chế định thời Goroutines tương tự với cơ chế định thời của hệ điều hành nhưng chỉ ở mức chương trình.
        - Bắt đầu một goroutine mới bằng cách thêm từ khóa `go` vào trước một hàm.
            ```go
            func main() {
	            go fmt.Println("World")
	            fmt.Println("Hello")
	            time.Sleep(1 * time.Second)
            }
            ```
        - Hàm `main()` trong Go sẽ được chạy trong `main goroutine`, khi `main goroutine` chạy xong, chương trình sẽ kết thúc, các `goroutine` khác dù chưa chạy xong sẽ đều phải dừng lại.
    - Channel
        - Channel là các kênh giao tiếp trung gian giữa các Goroutines trong Golang.
        - Channel giúp các goroutines có thể gởi và nhận được dữ liệu cho nhau một cách an toàn thông qua cơ chế lock-free.
        - Channel là kênh giao tiếp 2 chiều. Nghĩa là Channel có thể dùng cho cả gởi và nhận dữ liệu.
        - Các hoạt động gửi và nhận dữ liệu trên channel sẽ bị chặn (block) cho đến khi cả hai bên đều sẵn sàng:
            - Khi một goroutine gửi dữ liệu vào một channel (ch <- value), nó sẽ chờ (bị block) cho đến khi có một goroutine khác sẵn sàng nhận dữ liệu từ channel đó.
            - Tương tự, khi một goroutine muốn nhận dữ liệu từ một channel (value := <-ch), nó sẽ chờ cho đến khi có dữ liệu được gửi vào channel.
            - Nhờ cơ chế này, các goroutine có thể tự đồng bộ hóa với nhau một cách tự nhiên thông qua việc trao đổi dữ liệu, mà không cần sử dụng các cơ chế đồng bộ hóa phức tạp khác.
            ```go
            func sendValue(c chan<- int, value int) {
	            //Send value to channel
	            c <- value
            }
            func receiveValue(c <-chan int) {
	            //Receive value from channel
	            fmt.Println(<-c)
            }
            func main() {
	            //Initialize a channel
	            c := make(chan int)
	            go sendValue(c, 10)
	            go receiveValue(c)
	            time.Sleep(1 * time.Second)
            }
            ```
        - Để đóng một Channel chúng ta sẽ dùng hàm close(). Khi một Channel bị close thì có nghĩa là không còn dữ liệu nào sẽ đi qua nó nữa. Nếu ta gửi dữ liệu vào 1 channel đã được đóng thì sẽ dẫn đến panic.
            ```go
            func sendValue(c chan<- int, value int) {
	            //Send value to channel
	            c <- value
	            close(c)
            }
            func receiveValue(c <-chan int) {
	            //Receive value and check if channel ís closed
	            value, ok := <-c
	            if ok {
		            fmt.Println("Received value:", value)
	            } else {
		            fmt.Println("Channel is closed")
	            }
            }
            func main() {
	            //Initialize a channel
	            c := make(chan int)
	            go sendValue(c, 10)
	            go receiveValue(c)
	            go receiveValue(c)
	            time.Sleep(1 * time.Second)
            }
            ```
        - Ta có thể sử dụng `for range` để nhận tất cả dữ liệu từ một channel cho đến khi channel đó đóng.
            ```go
            func sendValue(c chan<- int, value ...int) {
	            //Send value to channel
	            for _, v := range value {
		            c <- v
	            }
	            close(c)
            }
            func receiveValue(c <-chan int) {
	            for v := range c {
		            fmt.Println(v)
	            }
            }
            func main() {
	            //Initialize a channel
	            c := make(chan int)
	            go sendValue(c, 3, 5, 7)
	            go receiveValue(c)
	            time.Sleep(1 * time.Second)
            }
            ```
        - Câu lệnh `Select` giúp một goroutine có thể làm việc, đợi và phản ứng với nhiều channel.
            ```go
            func sendValue(c chan<- int, value int) {
	            c <- value
	            close(c)
            }
            func main() {
	            c1 := make(chan int)
	            c2 := make(chan int)
	            go sendValue(c1, 3)
	            go sendValue(c2, 2)
	            select {
	            case v1 := <-c1:
		            fmt.Printf("First received from c1: %v\n", v1)
		            fmt.Printf("Then received from c2: %v\n", <-c2)

	            case v2 := <-c2:
		            fmt.Printf("First received from c2: %v\n", v2)
		            fmt.Printf("Then received from c1: %v\n", <-c1)
	            }
            }
            ```
    - Buffered channel
        - Buffered Channel là một channel trong Golang có khả năng lưu trữ được dữ liệu bên trong nó.
        - Sử dụng hàm len() để xem số lượng giá trị hiện đang có trong channel.
        - Sử dụng hàm cap() dể xem sức chứa tối đa của một channel.
        - Buffered Channel sẽ không block goroutine nếu sức chứa vẫn còn, mà không cần phải có một goroutine khác lấy dữ liệu từ channel.
        - Buffered Channel sẽ block goroutine hiện tại nếu vượt sức chứa.
        - Lấy dữ liệu từ empty buffered channel sẽ block goroutine.
            ```go
            func sendValue(c chan<- int, value ...int) {
	            //Send value to channel
	            for _, v := range value {
		            c <- v
	            }
	            close(c)
            }
            func receiveValue(c <-chan int) {
	            for v := range c {
		            fmt.Println(v)
	            }
            }
            func main() {
	            //Initialize a channel with capacity = 3
	            c := make(chan int, 3)
	            go sendValue(c, 3, 5, 7)
	            go receiveValue(c)
	            time.Sleep(1 * time.Second)
            }
            ```
    - Mutex
        - Mutex là một cơ chế đồng bộ hóa được sử dụng để đảm bảo rằng chỉ có một goroutine có thể truy cập vào một tài nguyên chia sẻ tại một thời điểm.
        - Go cung cấp hai loại mutex
            - Mutex: Khóa tiêu chuẩn, chỉ cho phép một goroutine truy cập vào tài nguyên chia sẻ tại một thời điểm.
            ```go
            var total struct {
	            sync.Mutex
	            value int
            }

            func add(value int) {
	            total.Lock()
	            total.value += value
	            fmt.Printf("add: %d, total value: %d \n", value, total.value)
	            total.Unlock()
            }

            func main() {
	            fmt.Printf("Initial total value: %d\n", total.value)
	            go add(10)
	            go add(-20)
	            go add(30)
	            time.Sleep(1 * time.Second)
            }
            ```
            - RWMutex (Read-Write Mutex): Phân biệt giữa các thao tác đọc và ghi. Nhiều goroutine có thể đồng thời đọc dữ liệu, nhưng chỉ một goroutine có thể ghi dữ liệu tại một thời điểm.
    - WaitGroup
        - WaitGroup là một cấu trúc đồng bộ hóa trong gói sync của Go, được sử dụng để đợi một nhóm goroutine hoàn thành công việc của chúng trước khi tiếp tục thực thi.
        - WaitGroup hoạt động như một bộ đếm:
            - Khi thêm goroutine vào nhóm đợi, ta tăng bộ đếm lên (sử dụng phương thức Add())
            - Khi một goroutine hoàn thành công việc, nó giảm bộ đếm xuống (sử dụng phương thức Done())
            - Goroutine chính có thể đợi cho đến khi bộ đếm về 0 (sử dụng phương thức Wait())
            ```go
            func main() {
	            var wg sync.WaitGroup

	            wg.Add(3)

	            go func() {
		            defer wg.Done()
		            fmt.Println("Goroutine 1 is running...")
		            time.Sleep(1 * time.Second)
		            fmt.Println("Goroutine 1 completed")
	            }()

	            go func() {
		            defer wg.Done()
		            fmt.Println("Goroutine 2 is running...")
		            time.Sleep(2 * time.Second)
		            fmt.Println("Goroutine 2 completed!")
	            }()

	            go func() {
		            defer wg.Done()
		            fmt.Println("Goroutine 3 is running...")
		            time.Sleep(3 * time.Second)
		            fmt.Println("Goroutine 3 completed!")
	            }()

	            fmt.Println("Waiting for all goroutines to complete...")
	            wg.Wait()
	            fmt.Println("All goroutines completed")
            }
            ```



    

    



    
