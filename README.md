## Clean Code PHP
**Biến**
- Sử dụng tên biến có nghĩa và có thể phát âm :
Không nên :
 ```
 $str_date = $moment->format('y-m-d');
 ```
 Nên :
```
$currentDate = $moment->format('y-m-d');
```
- Sử dụng cùng 1 từ cho cùng một loại biến : 
Không nên : 
```
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```
Nên : 
```
getUser();
```
- Sử dụng tên biến có thể tìm kiếm được
Không nên : 
```
$result = $serializer->serialize($data, 448);
// What the heck is 448 for?
```
Nên : 
```
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;
}

if ($user->access & User::ACCESS_UPDATE) {
    // do edit ...
}
```
- Sử dụng biến giải thích : 
Không nên : 
```
$info[1];
```
Nên : 
```
$info['name'];
```
- Tránh lồng quá nhiều và return sớm : 
Quá nhiều if else sẽ khiến code khó hiểu. Càng rõ ràng càng tốt.
Không nên : 
```
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            } else {
                return 1;
            }
        } else {
            return 0;
        }
    } else {
        return 'Not supported';
    }
}
```
Nên : 
```
function fibonacci(int $n): int
{
    if ($n === 0 || $n === 1) {
        return $n;
    }

    if ($n > 50) {
        throw new \Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```
- Tránh ánh xạ nhiều lần, làm cho người đọc phải dịch biến có nghĩa là gì :
Không nên :
```
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Wait, what is `$li` for again?
    dispatch($li);
}
```
Nên : 
```
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```
- Không nên thêm bối cảnh không cần thiết :Nếu tên lớp / đối tượng của bạn cho bạn biết điều gì đó, đừng lặp lại điều đó trong tên biến của bạn.
Không nên : 
```
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
```
Nên : 
```
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
```
- Sử dụng đối số mặc định vì phải kiểm tra bằng biểu thức điều kiện: 
Không nên : 
```
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
$breweryName : Có thể có giá trị là NULL
```
Nên : 
```
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```
- Phép so sánh : 
Không nên : 
```
$a = '42';
$b = 42;

if ($a != $b) {
   // The expression will always pass
}
Kết quả trả về False trên thực tế nó phải là true
```
Nên : 
```
$a = '42';
$b = 42;

if ($a !== $b) {
    // The expression is verified
}
Nó sẽ so sánh cả kiểu biến và giá trị.
```
- Function 
  - Đối số function (2 hoặc ít hơn).
  Không nên : 
  ```
  function createMenu(string $title, string $body, string $buttonText, bool $cancellable): void
  {
    // ...
  }
  ```
  Nên : 
   ```
   class MenuConfig
    {
        public $title;
        public $body;
        public $buttonText;
        public $cancellable = false;
    }

    $config = new MenuConfig();
    $config->title = 'Foo';
    $config->body = 'Bar';
    $config->buttonText = 'Baz';
    $config->cancellable = true;

    function createMenu(MenuConfig $config): void
    {
        // ...
    }
   ```
   - Một function nên thực hiên 1 công việc
   Không nên : 
    ```
    function emailClients(array $clients): void
    {
        foreach ($clients as $client) {
            $clientRecord = $db->find($client);
            if ($clientRecord->isActive()) {
                email($client);
            }
        }
    }
    ```
    Nên : 
    ```
    function emailClients(array $clients): void
    {
        $activeClients = activeClients($clients);
        array_walk($activeClients, 'email');
    }

    function activeClients(array $clients): array
    {
        return array_filter($clients, 'isClientActive');
    }

    function isClientActive(int $client): bool
    {
        $clientRecord = $db->find($client);

        return $clientRecord->isActive();
    }
    ```
    - Tên function nói lên chức năng của nó :
    Không nên :
    ```
    class Email
    {
        //...

        public function handle(): void
        {
            mail($this->to, $this->subject, $this->body);
        }
    }

    $message = new Email(...);
    // What is this? A handle for the message? Are we writing to a file now?
    $message->handle();
    ```
    Nên : 
    ```
    class Email 
    {
        //...

        public function send(): void
        {
            mail($this->to, $this->subject, $this->body);
        }
    }

    $message = new Email(...);
    // Clear and obvious
    $message->send();
    ```
    - Function nên là 1 mức của abstract : Tách các chức năng để tăng khả năng tái sử dụng và kiểm tra
    - Không sử dụng các cờ (true,false..)làm tham số function :
    Không nên :
    ```
    function createFile(string $name, bool $temp = false): void
    {
        if ($temp) {
            touch('./temp/'.$name);
        } else {
            touch($name);
        }
    }
    ```
    Nên : 
    ```
    function createFile(string $name): void
    {
        touch($name);
    }

    function createTempFile(string $name): void
    {
        touch('./temp/'.$name);
    }
    ```
    - Tránh tác dụng phụ :
    Không nên : 
    ```
    // Biến toàn cầu được tham chiếu bởi hàm sau.
    // Nếu chúng ta có một hàm khác sử dụng tên này, bây giờ nó sẽ là một mảng và nó có thể phá vỡ nó.
    $name = 'Ryan McDermott';

    function splitIntoFirstAndLastName(): void
    {
        global $name;

        $name = explode(' ', $name);
    }

    splitIntoFirstAndLastName();

    var_dump($name); // ['Ryan', 'McDermott'];
    ```
    Nên :
    ```
    function splitIntoFirstAndLastName(string $name): array
    {
        return explode(' ', $name);
    }

    $name = 'Ryan McDermott';
    $newName = splitIntoFirstAndLastName($name);

    var_dump($name); // 'Ryan McDermott';
    var_dump($newName); // ['Ryan', 'McDermott'];
    ```
    - Không ghi vào function toàn cục
    - Không sử dụng mẫu Singleton
    - Đóng gói các điều kiện : 
    Không nên :
    ```
    if ($article->state === 'published') {
    // ...
    }
    ```
    Nên :
    ```
    if ($article->isPublished()) {
    // ...
    }
    ```
    - Tránh điều kiện phủ định : 
    Không nên :
    ```
    if (!isDOMNodeNotPresent($node))
    {
        // ...
    }
    ```
    Nên : 
    ```
    if (isDOMNodePresent($node)) {
    // ...
    }
    ```
    - Xóa code không cần thiết
## Các chuẩn PSR-X trong PHP
- Chuẩn PSR -0 nói về Autoloading
  - Cung cấp quy tắc về việc viết các hàm autoload trong php, cách sử dụng namespace và kiến trúc thư mục, file để đảm bảo tính nhất quán giữa các project
- Chuẩn PSR-1 về Basic Coding
  - Tệp tin chỉ sử dụng các thẻ `<?php` và `<?=`
  - Tệp tin chỉ sử dụng UTF-8
  - Namespcae phải tuân theo PSR-0, PSR-4.
  - Hằng số phải khai báo bằng chữ in HOA có phân tách bằng dấu gạch chân
  - Tên class phải có dạng : NameClass
  - Tên phương thức: từ đầu viết thường và từ sau viết hoa

    
    
