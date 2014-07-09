# The official raywenderlich.com Objective-C style guide.

This style guide outlines the coding conventions for raywenderlich.com.

## Introduction

Nguyên nhân chúng tôi tạo ra bản quy tắc code này là để giữ code trong các cuốn sách, bài hướng dẫn và các bộ starter kit được đẹp mắt và thống nhất ngay cả khi có nhiều tác giả khác nhau cùng viết một cuốn sách

Bản hướng dẫn này khác nhiều so với các những bản hướng dẫn Objective C khác vì nó tập trung chính vào khả năng đọc trên các bản in và trên web. Nhiều lựa chọn dựa trên việc hướng không gian làm việc của mắt, rõ ràng, dễ viết.

## Credits

The creation of this style guide was a collaborative effort from various raywenderlich.com team members under the direction of Nicholas Waynik.  The team includes: [Soheil Moayedi Azarpour](https://github.com/moayes), [Ricardo Rendon Cepeda](https://github.com/ricardo-rendoncepeda), [Tony Dahbura](https://github.com/tdahbura), [Colin Eberhardt](https://github.com/ColinEberhardt), [Matt Galloway](https://github.com/mattjgalloway), [Greg Heo](https://github.com/gregheo), [Matthijs Hollemans](https://github.com/hollance), [Christopher LaPollo](https://github.com/elephantronic), [Saul Mora](https://github.com/casademora), [Andy Pereira](https://github.com/macandyp), [Mic Pringle](https://github.com/micpringle), [Pietro Rea](https://github.com/pietrorea), [Cesare Rocchi](https://github.com/funkyboy), [Marin Todorov](https://github.com/icanzilb), [Nicholas Waynik](https://github.com/ndubbs), and [Ray Wenderlich](https://github.com/raywenderlich)

We would like to thank the creators of the [New York Times](https://github.com/NYTimes/objective-c-style-guide) and [Robots & Pencils'](https://github.com/RobotsAndPencils/objective-c-style-guide) Objective-C Style Guides.  These two style guides provided a solid starting point for this guide to be created and based upon.

## Background

Có nhiều tài liệu từ Apple không được đề cập đến trong quy tắc code này mà có thể được đề cập bởi một trong những tài liệu dưới đây:

* [The Objective-C Programming Language](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
* [Cocoa Fundamentals Guide](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
* [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* [iOS App Programming Guide](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)

## Table of Contents

* [Language](#language)
* [Code Organization](#code-organization)
* [Spacing](#spacing)
* [Comments](#comments)
* [Naming](#naming)
  * [Underscores](#underscores)
* [Methods](#methods)
* [Variables](#variables)
* [Property Attributes](#property-attributes)
* [Dot-Notation Syntax](#dot-notation-syntax)
* [Literals](#literals)
* [Constants](#constants)
* [Enumerated Types](#enumerated-types)
* [Case Statements](#case-statements)
* [Private Properties](#private-properties)
* [Booleans](#booleans)
* [Conditionals](#conditionals)
  * [Ternary Operator](#ternary-operator)
* [Init Methods](#init-methods)
* [Class Constructor Methods](#class-constructor-methods)
* [CGRect Functions](#cgrect-functions)
* [Golden Path](#golden-path)
* [Error handling](#error-handling)
* [Singletons](#singletons)
* [Line Breaks](#line-breaks)
* [Smiley Face](#smiley-face)
* [Xcode Project](#xcode-project)


## Language

Nên sử dụng US English.

**Preferred:**
```objc
UIColor *myColor = [UIColor whiteColor];
```

**Not Preferred:**
```objc
UIColor *myColour = [UIColor whiteColor];
```


## Code Organization

Sử dụng `#pragma mark -` để phân nhóm phương thức theo nhóm chức năng và thực thi protocol/delegate theo phương thức chung này.

```objc
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

## Spacing

* Indent (thụt lề) sử dụng 2 khoảng trắng. Không bao giờ indent với các tab. Hãy nhớ thiết lập lựa chọn này trong Xcode.
* Phương thức braces (ngoặc nhọn) và braces khác (if/else/switch/while...): luôn luôn mở trên một dòng cùng các câu lệnh nhưng đóng trên một dòng mới.

**Preferred:**
```objc
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}
```

**Not Preferred:**
```objc
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}
```

* Nên có chính xác một dòng trống giữa các phương thức để tạo sự dễ nhìn và code trông sẽ có tổ chức hơn.
* Việc sử dụng @synthesize tổng hợp sẽ giúp tiết kiệm dòng code @synthesize và @dynamic nên được khai báo trên các dòng mới trong implementation.
* Colon-align (Căn lề dấu hai chấm) phương thức gọi nên được tránh. Có những trường hợp một phương thức có thể có từ 3 hoặc nhiều hơn colon (dấu hai chấm) và các colon-align sẽ làm cho code dễ đọc hơn. Tuy nhiên không nên căn lề colon trong các phương thức có chứa block bởi vì indent của Xcode sẽ làm nó không đọc được.

**Preferred:**

```objc
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```

**Not Preferred:**

```objc
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

## Comments

Khi cần, các comment nên được dùng để giải thích **tại sao** một phần cụ thể trong code làm một việc gì đó. Bất kỳ comment nào được sử dụng phải giữ được sự cập nhập hoặc đã được xóa

Nên tránh các comment block, code nên được tự tài liệu hóa, chỉ khi thực sự cần thiết thì sử dụng vài dòng để giải thích. *Ngoại lệ: Điều này không áp dụng cho những comment sử dụng để tạo tài liệu. 

## Naming

Quy tắc đặt tên của Apple nên được tuân thủ ở bất kỳ nơi nào có thể, đặc biệt là những thứ liên quan đến [các quy tắc quản lý bộ nhớ]
(https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html) ([NARC](http://stackoverflow.com/a/2865194/340508)).

Dài, phương pháp mô tả và đặt tên cho các biến là rất tốt
Long, descriptive method and variable names are good.

**Preferred:**

```objc
UIButton *settingsButton;
```

**Not Preferred:**

```objc
UIButton *setBut;
```
Một bộ ba tiền tố nên luôn được sử dụng cho các tên biến và hằng số, tuy nhiên có thể được bỏ qua cho các đối tên tượng Core Data. 
A three letter prefix should always be used for class names and constants, however may be omitted for Core Data entity names. For any official raywenderlich.com books, starter kits, or tutorials, the prefix 'RWT' should be used.

Hằng số nên được camel-case với tất cả các từ viết hoa và bắt đầu bằng tiền tố là tên các lớp liên quan cho rõ ràng 

**Preferred:**

```objc
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
```

**Not Preferred:**

```objc
static NSTimeInterval const fadetime = 1.7;
```

Các thuộc tính  nên được camel-case với các từ đi đầu là chữ cái thường. Sử dụng auto-synthesis cho các thuộc tính hơn là tự tổng hợp bằng câu lệnh @synthesize trừ khi bạn có lý do chính đáng

**Preferred:**

```objc
@property (strong, nonatomic) NSString *descriptiveVariableName;
```

**Not Preferred:**

```objc
id varnm;
```

### Underscores

Khi sử dụng các thuộc tính, các biến nên luôn được truy cập và thay đổi sử dụng `self.`. Điều này có nghĩa là tất các thuộc tính sẽ được phân biệt trực quan, như là tất cả chúng sẽ bắt đầu với `self.`.

Một ngoại lệ: bên trong các khởi tạo, các thể hiện biến hỗ trợ (ví dụ: _variableName) nên được sử dụng trực tiếp để tránh bất kỳ ảnh hưởng phụ của các getter/setter

Các biến nội bộ không nên chứa gạch dưới

## Methods

Trong cấu trúc phương thức, nên có một khoảng trắng sau các phương thức kiểu (ký tự -/+). Nên có một khoảng trắng giữa các phân đoạn của phương thức. (phù hợp với phong cách của Apple). Luôn luôn thêm một từ khóa và được mô tả với các từ trước tham số.

Việc sử dụng từ "and" được dành riêng. Nó không nên được dùng cho nhiều tham số như minh họa trong `initWithWidth:height:` ví dụ dưới đây

**Preferred:**
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**Not Preferred:**

```objc
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```

## Variables

Biến nên được đặt tên để mô tả về mục đích sử dụng của nó rõ nhất có thế. Các tên biến có một ký tự nên được tránh ngoại trừ trong vòng lặp `for()`

Dấu chỉ con trỏ thuộc về các biến, ví dụ: `NSString *text` không nên `NSString* text` hoặc `NSString * text`, ngoại trừ trong trường hợp các hằng số.

[Các thuộc tính private](#private-properties) nên được sử dụng ở vị trí của các thể hiện của biến bất cứ khi nào có thể. Mặc dù việc sử dụng các thể hiện biến là một cách làm hợp lệ, việc đồng ý sử dụng các thuộc tính trong code của bàn là phù hợp hơn.

Truy cập trực tiếp các biến instance là điều mà các thuộc tính 'back' nên tránh ngoại trừ trong các phương thức khởi tạo (`init`, `initWithCoder:`,...). phương thức `dealloc` và bên trong các phương thức setter và getter tùy chỉnh. Để biết thêm về việc sử dụng các Phương Thức Truy Cập trong các Phương Thức Khởi Tạo và dealloc, xem [ở đây]
(https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6).

**Preferred:**

```objc
@interface RWTTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

**Not Preferred:**

```objc
@interface RWTTutorial : NSObject {
  NSString *tutorialName;
}
```


## Property Attributes

Các đặc tính của thuộc tính nên được liệt kê rõ ràng, và sẽ giúp các lập trình viên mới khi đọc code. Thứ tự của các thuộc tính nên được lưu trữ sau atomicity, điều này là phù hợp với việc sinh code tự động khi kết nối các thành phần giao diện từ Interface Builder.

**Preferred:**

```objc
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *tutorialName;
```

**Not Preferred:**

```objc
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

Các thuộc tính với bản sao có thể thay đổi được (như NSString) nên sử dụng `copy` thay vì `strong`.
Tại sao? Thêm chí nếu bạn khai báo một thuộc tính như `NSString` ai đó có thể truyền một instance của một `NSMutableString` và sau đó thay đổi nó mà bạn không cần phải chú ý về việc này.

**Preferred:**

```objc
@property (copy, nonatomic) NSString *tutorialName;
```

**Not Preferred:**

```objc
@property (strong, nonatomic) NSString *tutorialName;
```

## Dot-Notation Syntax

Cú phám chấm `.` hoàn toàn là một wrapper thuận tiện xung quanh các lời gọi phương thức truy cập. Khi bạn sử dụng cú pháp chấm, thuộc tính vẫn được truy nhập hoặc thay đổi sử dụng các phương thức getter và setter/ Đọc thêm [ở đây](https://developer.apple.com/library/ios/documentation/cocoa/conceptual/ProgrammingWithObjectiveC/EncapsulatingData/EncapsulatingData.html)

Ký tự chấm nên **luôn luôn** được sử dụng cho việc truy nhập và thay đổi các thuộc tính, nó làm code ngắn gọn hơn. Ký tự ngoặc vuông `[]` được ưa dùng trong tất cả các trường hợp khác.

**Preferred:**
```objc
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Not Preferred:**
```objc
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## Literals

`NSString`, `NSDictionary`, `NSArray`, và `NSNumber` nên được sử dụng bất cứ khi nào tạo các instance bất biến của các đối tượng. Hãy chú trong vào việc giá trị `nil` không thể được truyền vào `NSArray` và `NSDictionary`, nếu không sẽ gây ra lỗi crash.

**Preferred:**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**Not Preferred:**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

## Constants

Các hằng số được ưa dùng hơn các chuỗi ký tự or số trên một dòng, như thế chúng cho phép dễ dàng sao chép các biến thường dùng và có thể nhanh chóng được thay đổi mà không cần phải tìm kiếm và thay thế. Các hàng số nên được khai báo kiểu hằng số `static` và không nên sử dụng các `#define` trừ khi nó được sử dụng như một macro.

**Preferred:**

```objc
static NSString * const RWTAboutViewControllerCompanyName = @"RayWenderlich.com";

static CGFloat const RWTImageThumbnailHeight = 50.0;
```

**Not Preferred:**

```objc
#define CompanyName @"RayWenderlich.com"

#define thumbnailHeight 2
```

## Enumerated Types

Khi sử dụng các `enum`, nó được khuyến khích sử dụng các kiểu kỹ thuật underlying cố định mới bởi vì nó có kiểu kiểm tra mạnh hơn và hoàn thành code. Các SDK bây giờ thêm một macro để tạo điều kiện và khuyến khích việc sử dụng các kiểu underlying cố định: `NS_ENUM()`

**For Example:**

```objc
typedef NS_ENUM(NSInteger, RWTLeftMenuTopItemType) {
  RWTLeftMenuTopItemMain,
  RWTLeftMenuTopItemShows,
  RWTLeftMenuTopItemSchedule
};
```

You can also make explicit value assignments (showing older k-style constant definition):

```objc
typedef NS_ENUM(NSInteger, RWTGlobalConstants) {
  RWTPinSizeMin = 1,
  RWTPinSizeMax = 5,
  RWTPinCountMin = 100,
  RWTPinCountMax = 500,
};
```

Older k-style constant definitions should be **avoided** unless writing CoreFoundation C code (unlikely).

**Not Preferred:**

```objc
enum GlobalConstants {
  kMaxPinSize = 5,
  kMaxPinCount = 500,
};
```


## Case Statements

Dấu ngoặc nhọn không được yêu cầu cho các câu lệnh state, trừ khi bắt buộc phải tuân theo bởi các trình biên dịch.
Khi một case chưa nhiều hơn một dòng, các dấu ngoặc nhọn nên được thêm vào

```objc
switch (condition) {
  case 1:
    // ...
    break;
  case 2: {
    // ...
    // Multi-line example using braces
    break;
  }
  case 3:
    // ...
    break;
  default: 
    // ...
    break;
}

```

Có nhiều lần khi cùng code có thể được sử dụng cho nhiều case, và một fall-through nên được dùng. Một fall-through là việc loại bỏ các câu lệnh 'break' cho một case từ đó cho phép các luồng thực thi để đi qua các giá trị case tiếp theo. Một fall-through nên được comment cho việc code rõ ràng

```objc
switch (condition) {
  case 1:
    // ** fall-through! **
  case 2:
    // code executed for values 1 and 2
    break;
  default: 
    // ...
    break;
}

```

Khi sử ụng một kiểu enum cho một swithc, 'default' là không cần thiết. Ví dụ

```objc
RWTLeftMenuTopItemType menuType = RWTLeftMenuTopItemMain;

switch (menuType) {
  case RWTLeftMenuTopItemMain:
    // ...
    break;
  case RWTLeftMenuTopItemShows:
    // ...
    break;
  case RWTLeftMenuTopItemSchedule:
    // ...
    break;
}
```


## Private Properties

Các thuộc tính riêng nên được khai báo trong các mở rộng lớp (anonymous categories) ở trong file .m của lớp. Không nên đặt tên categories (như là `RWPrivate` hay `private`) nếu không dùng để mở rộng lớp khác. Nếu muốn chia sẻ anonymous category khi chạy unit test thì dùng file `+Private.h`. 

**For Example:**

```objc
@interface RWTDetailViewController ()

@property (strong, nonatomic) GADBannerView *googleAdView;
@property (strong, nonatomic) ADBannerView *iAdView;
@property (strong, nonatomic) UIWebView *adXWebView;

@end
```

## Booleans

Dùng `YES` và `NO` thay cho `true` và `false`. Giá trị `nil` dẫn đến `NO` vì thế không cần so sánh chúng trong các mệnh đề điều kiện. Cũng không nên so sánh biến trực tiếp với `YES` vì `YES` được định nghĩ là `1`.

**Nên:**

```objc
if (someObject) {}
if (![anotherObject boolValue]) {}
```

**Không nên:**

```objc
if (someObject == nil) {}
if ([anotherObject boolValue] == NO) {}
if (isAwesome == YES) {} // Never do this.
if (isAwesome == true) {} // Never do this.
```

Không nên sử dụng tiền tố “is” trong tên của thuộc tính kiểu `BOOL` vì nó trùng với tên hàm truy cập biến.

```objc
@property (assign, getter=isEditable) BOOL editable;
```
Tham khảo [Cocoa Naming Guidelines](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE).

## Conditionals

Trong thân hàm điều kiện nên bao bởi ngoặc nhọn vì nếu không làm như thế , lỗi thường xảy ra khi ta thêm dòng lệnh thứ hai. Ngoài ra các làm trên cũng giúp đảm bảo thống nhất code và dễ nhìn.

**Nên:**
```objc
if (!error) {
  return success;
}
```

**Không nên:**
```objc
if (!error)
  return success;
```

or

```objc
if (!error) return success;
```

### Ternary Operator

Toán tam phân `?:` chỉ nên dùng khi giúp tăng độ rõ ràng và giảm code thừa. Điều kiện đơn giản thì nên dùng tam phân, phức tạp thì nên dùng if . Hay nhất là dùng khi gán giá trị cho biến với điều kiện xác định.

Với các biến không phải boolean khi cần so sánh thì nên bao bởi ngoặc đơn giúp dễ đọc. Nếu biến chỉ cần so sánh với giá trị `BOOL` thì không cần ngoặc đơn. 

**Nên:**
```objc
NSInteger value = 5;
result = (value != 0) ? x : y;

BOOL isHorizontal = YES;
result = isHorizontal ? x : y;
```

**Không nên:**
```objc
result = a > b ? x = c > d ? c : d : y;
```

## Init Methods

Phương thức khởi tạo nên theo chuẩn của Apple. Trả về kiểu `instancetype` thay vì `id`.

```objc
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}
```

See [Class Constructor Methods](#class-constructor-methods) for link to article on instancetype.

## Class Constructor Methods

Các hàm tạo lớp nên trả về kiểu `instancetype` thay vì `id` để đảm bảo trình biên dịch trả về đúng kiểu.

```objc
@interface Airplane
+ (instancetype)airplaneWithType:(RWTAirplaneType)type;
@end
```

More information on instancetype can be found on [NSHipster.com](http://nshipster.com/instancetype/).

## CGRect Functions

Khi truy cập các giá trị `x`, `y` , `width`, `height` của một `CGRect`, nên sử dụng các hàm của `CGGeometry` thay vì lấy giá trị trực tiếp. 

**Nên:**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```

**Không nên:**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```

## Golden Path

Phần code làm việc với các điều kiện nên tuân thủ theo Golden Path 

**Nên:**

```objc
- (void)someMethod {
  if (![someOther boolValue]) {
	return;
  }

  //Do something important
}
```

**Không nên:**

```objc
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```

## Error handling

Khi phương thức trả về một tham số error bởi tham chiếu thì nên rẽ nhánh dựa trên kết quả trả về, không dựa trên biến error.

**Nên:**
```objc
NSError *error;
if (![self trySomethingWithError:&error]) {
  // Handle Error
}
```

**Không nên:**
```objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
  // Handle Error
}
```

## Singletons

Đối tượng singleton nên sử dụng thread-safe khi khởi tạo 

```objc
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```
This will prevent [possible and sometimes prolific crashes](http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html).


## Line Breaks

Việc xuống dòng cần được thực hiện sao cho dễ đọc trên bản in hay xem online. 

For example:
```objc
self.productsRequest = [[SKProductsRequest alloc] initWithProductIdentifiers:productIdentifiers];
```
Trường hợp dòng code dài thì nên xuống dòng.

```objc
self.productsRequest = [[SKProductsRequest alloc] 
  initWithProductIdentifiers:productIdentifiers];
```


## Smiley Face

Smiley faces are a very prominent style feature of the raywenderlich.com site!  It is very important to have the correct smile signifying the immense amount of happiness and excitement for the coding topic.  The end square bracket is used because it represents the largest smile able to be captured using ascii art.  A half-hearted smile is represented if an end parenthesis is used, and thus not preferred.

**Nên:**
```objc
:]
```

**Không nên:**
```objc
:)
```  


## Xcode project

Các file vật lý nên được sync với các file trong Xcode project mà không cần giải thích. Mỗi Xcode groups được tạo ra nên ánh xạ bởi thư mục trong hệ thống file. Code nên được nhóm lại không chỉ theo kiểu mà còn theo theo các tính năng lớn.

Nếu có thể thì nên coi cảnh báo khai build như là lỗi.

# Other Objective-C Style Guides

Nếu chưa thấy hài lòng, bạn có thể tham khảo thêm các quy tắc code dưới đây:

* [Robots & Pencils](https://github.com/RobotsAndPencils/objective-c-style-guide)
* [New York Times](https://github.com/NYTimes/objective-c-style-guide)
* [Google](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
* [GitHub](https://github.com/github/objective-c-conventions)
* [Adium](https://trac.adium.im/wiki/CodingStyle)
* [Sam Soffes](https://gist.github.com/soffes/812796)
* [CocoaDevCentral](http://cocoadevcentral.com/articles/000082.php)
* [Luke Redpath](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)
* [Marcus Zarra](http://www.cimgf.com/zds-code-style-guide/)
