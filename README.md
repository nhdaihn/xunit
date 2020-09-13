##### Unit Test là gì?
Unit Test là một loại kiểm thử phần mềm trong đó các đơn vị hay thành phần riêng lẻ của phần mềm được kiểm thử. Kiểm thử đơn vị được thực hiện trong quá trình phát triển ứng dụng. Mục tiêu của Kiểm thử đơn vị là cô lập một phần code và xác minhtính chính xác của đơn vị đó.

##### xUnit là gì?
xUnit hay còn gọi là xUnit.net là một khung thử nghiệm đơn vị cho .NET. Nó là mã nguồn mở và hoàn toàn miễn phí để sử dụng. 
Những người tạo ra khung NUnit, James & Brad, cũng được ghi nhận vì đã viết khung thử nghiệm xUnit với mục đích duy nhất làxây dựng một khung thử nghiệm tốt hơn. Do đó, bạn sẽ tìm thấy rất nhiều điểm tương đồng giữa thử nghiệm NUnit và thử nghiệm xUnit. NUnit đóng vai trò là nền tảng cho rất nhiều tính năng mới được giới thiệu trong xUnit.(tham khảo xUnit.net)

##### Cài đạt xUnit trong Visual studio by nuget.
<img src="https://imgur.com/gallery/yGGs83X">
###### Install nuget **Xunit** vs **Xunit.runner.visualstudio**
<img src="https://imgur.com/gallery/OYRrlvh">

##### AAA testing là gì?
AAA là một pattern phổ biến để viết unit test cho một method.<br/>
###### Trong đó:
The [**Arrange** ] section of a unit test method initializes objects and sets the value of the data that is passed to the method under test.<br/>
The [**Act** ] section invokes the method under test with the arranged parameters.<br/>
The [**Assert** ] section verifies that the action of the method under test behaves as expected.<br/>

###### Ví dụ 
//Arrange test
testClass objtest = new testClass();
Boolean result;

//Act test
result = objtest.testFunction();

//Assert test
Assert.AreEqual(true, result);

##### Tại sao Class Asserts?
Trong xUnit class khá quan trọng cần quan tâm là Xunit.Assert. Class này cho phép so sánh các giá trị, chuỗi, tập hợp, ngoại lệ và sự kiện.<br/>

**All** : Kiểm tra xem tất cả item trong collection có thực hiện đúng action hay không.<br/>
```csharp
Assert.All(result, item => Assert.Contains("John", item.Name));
```

**Collection** : Kiểm tra xem từng phần tử trong collection có thực hiện đúng hành động tương ứng hay không(Số lượng kiểm tra phải bằng với số phần tử trong collection(phức tạp hơn Assert.All)).<br/>
```csharp
var list = new List<int> { 42, 2112 };
Assert.Collection(list,
                item => Assert.Equal(42, item),
                item => Assert.Equal(2112, item));
```
				
**Contains** : Kiểm tra chuổi này có tồn tại trong chuỗi kia.<br/>
**DoesNotContain** : Kiểm tra chuổi này không tồn tại trong chuỗi kia.<br/>
```csharp
Assert.Contains("This", "This is a text.");
Assert.DoesNotContain("abcd", "This is a text.");
```

**Empty** : Kiểm tra collection có rỗng<br/>
**NotEmpty** : Kiểm tra collection không rỗng<br/><br/>
```csharp
var observableList = new ObservableList<DateTime> { DateTime.Now, new DateTime(2001, 5, 4) };
observableList.Clear();
Assert.Empty(observableList.ToArray());
```

**StartsWith** : Kiểm tra chuỗi này có bắt đầu bằng chuỗi kia<br/>
**EndsWith** : Kiểm tra chuối này có kết thúc bằng chuỗi kia<br/>
```csharp
Assert.StartsWith("This is a text.", "This");
Assert.EndsWith("This is a text.", "text.");
```

**Equal** : Kiểm tra hai giá trị có băng nhau<br/>
**NotEqual** : Kiểm tra hai giá trị có khác nhau<br/>
```csharp
Assert.Equal("This", "This");
Assert.Equal("This", "This is a text.");
```

**True** : Kiểm tra có trả về True<br/>
**False** : Kiểm tra có trả về False<br/>
```csharp
Assert.True("".GetType() == typeof(string));
Assert.False(1.GetType() == typeof(int));
```

**InRange** : Kiểm tra giá trị có trong khoảng giá trị<br/>
**NotInRange** : Kiểm tra giá trị có nằm ngoài khoảng giá trị<br/>
```csharp
var actual = 1;
Assert.InRange(actual, int.MinValue, int.MaxValue)
```

**IsAssignableFrom** :<br/>

**IsType** : Kiểm tra xem giá trị có phải kiểu đã cho<br/>
**IsNotType** : Kiểm tra xem giá trị không phải kiểu đã cho<br/>
```csharp
Assert.IsType<string>("passes");
Assert.IsNotType<string>(1);
```

**Matches**: Kiểm tra string match a regular expression<br/>
**DoesNotMatch**: Kiểm tra string not match a regular expression<br/>
```csharp
var regEx = @"\A[A-Z0-9+_.-]+@[A-Z0-9.-]+\Z";
Assert.DoesNotMatch(regEx, "this is a text");
Assert.Matches(regEx, "this is a text");
```

**Null**: Kiểm tra object có null<br/>
**NotNull** : Kiểm tra object khác null<br/>
```csharp
string str1 = null;
string str2 = "hello";              
Assert.Null(str1);
Assert.Nullstr2 
```

**Same**: Kiểm tra hai object có cùng instance<br/>
**NotSame** : Kiểm tra hai object không cùng instance<br/>
```csharp
Customer john = new Customer { Id = 1, Name = "John" };
Customer john2 = john;
Assert.Same(john, john2);
```

**StrictEqual**:<br/>
**NotStrictEqual**:<br/>

**Subset**: Kiểm tra một tập hợplà subset của một tập hợp khác.<br/>
**ProperSubset** : Kiểm tra một tập hợplà proper subset của một tập hợp khác.<br/>
```csharp
var set1 = new HashSet<int> { 1, 2, 3, 4, 5, 6 };
var set2 = new HashSet<int> { 3, 4 };
var notProperSubset = new HashSet<int> { 1, 2, 3, 4, 5, 6 };
Assert.Subset(set1, set2);
Assert.ProperSubset(set1, set2);
// fails, https://mathinsight.org/definition/proper_subset
Assert.ProperSubset(set1, notProperSubset);
```

**PropertyChanged**: Kiểm tra property hoặc collection có được thay đổi<br/>
```csharp
// arrange
var target = new ObservableStack<string>();
target.Push("1");
// act
Assert.PropertyChanged(target, "Count", () => target.Clear());
```csharp

PropertyChangedAsync: Kiểm tra property hoặc collection có được thay đổi bất đồng bộ

**Raises**: Kiểm tra một event có được gọi <br/>
**RaisesAny**:<br/>
**RaisesAnyAsync**:<br/>

**Single**: Kiểm tra collection chỉ có duy nhất một phần tử<br/>
```csharp
var listWithSingle = new List<int> { 1 };
Assert.Single(listWithSingle);
```

**Throws**: Kiểm tra ngoại lệ được ném ra<br/>
```csharp
Assert.Throws<Exception>(() => service.GetData());
```

**ThrowsAnyAsync**:<br/>
**RecordException**:<br/>
**RecordExceptionAsync**:<br/>

##### Quy tắc đặt tên cho medthod test

Có nhiều quy tắc đặt tên cho method unit test <br/>
*  Ở đây đang tham khảo* (https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html)<br/>
```csharp
[MethodName_StateUnderTest_ExpectedBehavior]<br/>
```
**MethodName**: Tên method<br/>
**StateUnderTest**: Trạng thái kiểm tra<br/>
**ExpectedBehavior**: Kết quả mong muốn<br/>

Ví dụ muốn test method Add với đầu vào là hai số nguyên dương bất kỳ và kết quả mong muôn là > 100<br/>

```csharp
[Fact]
public void Add_AnyNumberic_BiggerThan100()
{
	//
}
```
