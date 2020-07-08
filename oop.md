#### Lập trình hướng đối tượng là gì?

 Lập trình hướng đối tượng là một kỹ thuật lập trình  mà ở đó lập trình viên sẽ nắm bắt và phân tích các thực thế, sự việc của đời sống ánh xạ vào chương trình    phần mềm của mình. Các đối tượng sẽ được mô tả bằng class trong lập trình, class sẽ bao gồm các thuộc tính(attribute) và các phương thức(method) của đối tượng. Từ class chúng ta sẽ tạo ra các thể hiện của class đó gọi là các object và các object này sẽ tương tác với nhau thông qua các message trong chương trình của chúng ta.

#### Các tính chất của lập trình hướng đối tượng

**Tính kế thừa**

  **Kế thừa** cho phép một class có thể  kế thừa các attribute và method từ một class khác đồng thời có thêm các attribute và method của riêng chúng, ví dụ: 1 class **Animal** có các thuộc tính như sau: *tên*, *tuổi*, *màu sắc* và các hành vi: *ăn*, *uống* và nếu một class **Person** kế thừa class Animal này thì có nghĩa rằng Person sẽ hiển nhiên có các thuộc tính tên*, *tuổi*, *màu sắc* và các hành vi: *ăn*, *uống* , ngoài ra có thể  có thêm thuộc tính khác như *nghề nghiệp* chẳng hạn. Với tính chất này thì code của chúng ta sẽ trở nên reuseable(tái sử dụng) phải không?

**Tính trừu tượng**

  **Trừu tượng**  có nghĩa là bỏ qua các chi tiết, chỉ tập trung vào các thuộc tính và hành vi quan trọng, ví dụ: Nếu làm một bài toán liên quan đến quản lý nhân   viên trong công ty thì chúng ta sẽ chỉ trung vào vào các đặc điểm: *tên*, *tuổi*, *kinh nghiệm*, *kĩ năng* và bỏ qua những chi tiết khác như màu da, màu tóc.

**Tính đa hình**

 Dù là cùng một hành động nhưng mỗi đối tượng lại có một cách thực hiện khác nhau đó chính là **Đa hình** ví dụ: cùng là một hành động ăn nhưng với động vật thì thế cho thức ăn vào miệng rồi ăn nhưng còn đối với con người thì phải chế biến thức ăn thức ăn trước rồi mới đưa vào miệng.

**Tính đóng gói**

  Là tính chất cho phép một class ẩn dấu các thuộc tính và phương thức khỏi sự truy cập từ bên ngoài class đó.
  
#### Message trong lập trình hướng đối tượng
  Trong lập trình hướng đối tượng thì các object sẽ tương tác với nhau thông qua các message.
  Ví dụ chúng ta có các class như sau:
  ```
  class Animal
   attr_accessor :name
    
   def initialize(name)
     @name = name
     @age = age
     @color = color
   end
  end

  class Test
   def animal_name
     dog = Animal.new('Dog', 1, 'black')
     dog_name = dog.name
     dog_name
   end
  end

  class OtherClass
   def other_method
    test = Test.new
    test.animal_name
   end
  end
  ```
Hãy chú ý đến dòng `dog_name = dog.name` ở câu lệnh này `name` là message được gửi đi còn `dog` là receiver còn sender sẽ là một một object của class Test được tạo ra ở OtherClass, đây là cách mà cách mà các object tương tác với nhau trong chương trình của chúng ta. 

#### Ưu điểm lập trình hướng đối tượng

- Dễ thay đổi code
- Tính bảo mật cao và khả năng tái sử dụng
- Tiết kiệm đáng kể tài nguyên hệ thống