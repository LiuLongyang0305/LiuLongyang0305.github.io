# 1. 正则表达式——Regular Expression

- [1. 正则表达式——Regular Expression](#1-正则表达式regular-expression)
  - [1.1. NSRegularExpression](#11-nsregularexpression)
    - [1.1.1. 用到的常量](#111-用到的常量)
    - [1.1.2. 方法](#112-方法)
    - [1.1.3. 替换方法](#113-替换方法)
    - [1.1.4. 正则表达式的测试程序](#114-正则表达式的测试程序)
  - [1.2. 正则表达式](#12-正则表达式)
    - [1.2.1. 两种模糊匹配](#121-两种模糊匹配)
    - [1.2.2. 字符组](#122-字符组)
    - [1.2.3. 量词](#123-量词)
    - [1.2.4. 多选分支](#124-多选分支)
    - [1.2.5. 正则表达式中的括号](#125-正则表达式中的括号)
      - [1.2.5.1. 分组和分支功能](#1251-分组和分支功能)
      - [1.2.5.2. 引用分组用以提取数据](#1252-引用分组用以提取数据)
      - [1.2.5.3. 分组引用](#1253-分组引用)
      - [1.2.5.4. 分组嵌套](#1254-分组嵌套)
      - [1.2.5.5. 不捕获子组](#1255-不捕获子组)
    - [1.2.6. 四种常见的匹配模式](#126-四种常见的匹配模式)
    - [1.2.7. 断言](#127-断言)
      - [1.2.7.1. 单词边界](#1271-单词边界)
      - [1.2.7.2. 环视(Look Around)](#1272-环视look-around)

## 1.1. NSRegularExpression

### 1.1.1. 用到的常量

```swift{.line-numbers}
    public struct Options : OptionSet {

        public init(rawValue: UInt)

        
        public static var caseInsensitive: NSRegularExpression.Options { get } // 不区分大小写

        public static var allowCommentsAndWhitespace: NSRegularExpression.Options { get }//忽略空格和#

        public static var ignoreMetacharacters: NSRegularExpression.Options { get }//整体化

        public static var dotMatchesLineSeparators: NSRegularExpression.Options { get }//匹配任何字符，包括分隔符

        public static var anchorsMatchLines: NSRegularExpression.Options { get }// 允许^和$在匹配的结束行

        public static var useUnixLineSeparators: NSRegularExpression.Options { get }

        public static var useUnicodeWordBoundaries: NSRegularExpression.Options { get }
    }

     public struct MatchingOptions : OptionSet {

        public init(rawValue: UInt)

        
        public static var reportProgress: NSRegularExpression.MatchingOptions { get } /* Call the block periodically during long-running match operations. */

        public static var reportCompletion: NSRegularExpression.MatchingOptions { get } /* Call the block once after the completion of any matching. */

        public static var anchored: NSRegularExpression.MatchingOptions { get } /* Limit matches to those at the start of the search range. */

        public static var withTransparentBounds: NSRegularExpression.MatchingOptions { get } /* Allow matching to look beyond the bounds of the search range. */

        public static var withoutAnchoringBounds: NSRegularExpression.MatchingOptions { get } /* Prevent ^ and $ from automatically matching the beginning and end of the search range. */
    }

    public struct MatchingFlags : OptionSet {

        public init(rawValue: UInt)

        
        public static var progress: NSRegularExpression.MatchingFlags { get } /* Set when the block is called to report progress during a long-running match operation. */

        public static var completed: NSRegularExpression.MatchingFlags { get } /* Set when the block is called after completion of any matching. */

        public static var hitEnd: NSRegularExpression.MatchingFlags { get } /* Set when the current match operation reached the end of the search range. */

        public static var requiredEnd: NSRegularExpression.MatchingFlags { get } /* Set when the current match depended on the location of the end of the search range. */

        public static var internalError: NSRegularExpression.MatchingFlags { get } /* Set when matching failed due to an internal error. */
    }
}

```

### 1.1.2. 方法

```swift{.line-numbers}
extension NSRegularExpression {

    
    /* The fundamental matching method on NSRegularExpression is a block iterator.  There are several additional convenience methods, for returning all matches at once, the number of matches, the first match, or the range of the first match.  Each match is specified by an instance of NSTextCheckingResult (of type NSTextCheckingTypeRegularExpression) in which the overall match range is given by the range property (equivalent to rangeAtIndex:0) and any capture group ranges are given by rangeAtIndex: for indexes from 1 to numberOfCaptureGroups.  {NSNotFound, 0} is used if a particular capture group does not participate in the match.
    */
    
    open func enumerateMatches(in string: String, options: NSRegularExpression.MatchingOptions = [], range: NSRange, using block: (NSTextCheckingResult?, NSRegularExpression.MatchingFlags, UnsafeMutablePointer<ObjCBool>) -> Void)

    
    open func matches(in string: String, options: NSRegularExpression.MatchingOptions = [], range: NSRange) -> [NSTextCheckingResult]

    open func numberOfMatches(in string: String, options: NSRegularExpression.MatchingOptions = [], range: NSRange) -> Int

    open func firstMatch(in string: String, options: NSRegularExpression.MatchingOptions = [], range: NSRange) -> NSTextCheckingResult?

    open func rangeOfFirstMatch(in string: String, options: NSRegularExpression.MatchingOptions = [], range: NSRange) -> NSRange
}
```

### 1.1.3. 替换方法

```swift{.line-numbers}
extension NSRegularExpression {

    
    /* NSRegularExpression also provides find-and-replace methods for both immutable and mutable strings.  The replacement is treated as a template, with $0 being replaced by the contents of the matched range, $1 by the contents of the first capture group, and so on.  Additional digits beyond the maximum required to represent the number of capture groups will be treated as ordinary characters, as will a $ not followed by digits.  Backslash will escape both $ and itself.
    */
    open func stringByReplacingMatches(in string: String, options: NSRegularExpression.MatchingOptions = [], range: NSRange, withTemplate templ: String) -> String

    open func replaceMatches(in string: NSMutableString, options: NSRegularExpression.MatchingOptions = [], range: NSRange, withTemplate templ: String) -> Int

    
    /* For clients implementing their own replace functionality, this is a method to perform the template substitution for a single result, given the string from which the result was matched, an offset to be added to the location of the result in the string (for example, in case modifications to the string moved the result since it was matched), and a replacement template.
    */
    open func replacementString(for result: NSTextCheckingResult, in string: String, offset: Int, template templ: String) -> String

    
    /* This class method will produce a string by adding backslash escapes as necessary to the given string, to escape any characters that would otherwise be treated as template metacharacters. 
    */
    open class func escapedTemplate(for string: String) -> String
}
```

### 1.1.4. 正则表达式的测试程序

```swift{.line-numbers}
func testRegularExpression (regex:String,validateString:String) -> [String]{
    do {
        let regex: NSRegularExpression = try NSRegularExpression(pattern: regex, options: [])
        let matches = regex.matches(in: validateString, options: [], range: NSMakeRange(0, validateString.count))
        return matches.map {(validateString as NSString).substring(with: $0.range)}
    } catch {
        print("Error when create regex!")
        return []
    }
}
```

## 1.2. 正则表达式

### 1.2.1. 两种模糊匹配

- 横向：匹配长度不固定，形式`{m,n}`，表示至少重复`m`次，至多重复`n`次。例如`ab{2,5}c`可以匹配：`abbc`、`abbbc`、`abbbbc`、`abbbbbc`。
- 纵向：具体到某一个字符，可能不止一种情况，形式`[chars]`。例如`a[123]b`可以匹配`a1b`、`a2b`、`a3b`。

### 1.2.2. 字符组

- 表示范围。
  - `[1-9]`可以匹配任何数字。
  - `[a-z]`可以匹配任何小写字母。
  - `[A-Z]`可以匹配任何大写字母。
- 排除字符组。用`^`符号，比如`[^abc]`可以匹配`abc`之外的任何字符。
- 常见字符组。
  - `\d` <=====> `[0-9]`
  - `\D` <=====> `[^0-9]`
  - `\w` <=====> `[0-9a-zA-Z]`
  - `\W` <=====> `[^0-9a-zA-Z]`
  - `\s` <=====> `[\t\v\n\r\f]`
  - `\S` <=====> `[^\t\v\n\r\f]`
  - `.` <=====> `[^\n\r\u2028\u2029]`
  - `\`:如果要匹配以下字符必须使用转义符号：`*?+[(){}^$|\/>`

### 1.2.3. 量词

量词也叫重复。知道`{m,n}`的含义之后，需要熟记一下简写形式：

- `{m,}`表示至少重复`m`次。
- `{m}`等价于`{m,m}`表示重复`m`次。
- `?`等价于`{0,1}`表示出现或者不出现。
- `+`等价于`{1,}`，表示至少出现一次。
- `*`等价于`{0,}`，表示出现任意次。
- 贪婪匹配：尽可能多的匹配。实现方式：量词后面加上`+`，比如`{m,n}+`、`?+`、`++`。
- 惰性匹配：尽可能少的匹配。实现方式：量词后面加上`?`，比如`{m,n}?`、`??`、`+?`。

### 1.2.4. 多选分支

多选分支支持多个子模式任选其一。实现方式`p1|p2|p3`，其中*p1、p2、p3*是子模式。

```swift{.line-numbers}
let code = "abxc   adzc   aeyc"
print(testRegularExpression(regex: "a(bx|ey)c", validateString: code))
//Print ["abxc", "aeyc"]

//需要自己体会区别
let code = "goodboy   badboy"
print(testRegularExpression(regex: "good|goodboy", validateString: code))
//Print ["good"]
print(testRegularExpression(regex: "goodboy|good", validateString: code))
//Print ["goodboy"]
print(testRegularExpression(regex: "badboy|goodboy", validateString: code))
//Print ["goodboy", "badboy"]

```

### 1.2.5. 正则表达式中的括号

#### 1.2.5.1. 分组和分支功能

- `(ab)+`
- `(p1|p2)`

#### 1.2.5.2. 引用分组用以提取数据

```swift{.line-numbers}
func testRegularExpressionCaptureGroups (regex:String,validateString:String) -> [[String]]{
    do {
        let regex: NSRegularExpression = try NSRegularExpression(pattern: regex, options: [])
        let matches = regex.matches(in: validateString, options: [], range: NSMakeRange(0, validateString.count))
        var data = [[String]]()
        for match in matches {
            var currentMatch = [String]()
            for idx in 0..<match.numberOfRanges {
                currentMatch.append((validateString as NSString).substring(with: match.range(at: idx)))
            }
            data.append(currentMatch)
        }
        return data
    } catch {
        print("Error when create regex!")
        return []
    }
}
let regex = "(\\d{4})-(\\d{2})-(\\d{2})"
var string1 = "2017-06-12";
print(testRegularExpressionCaptureGroups(regex: regex, validateString: string1))
// Print [["2017-06-12", "2017", "06", "12"]]
```

#### 1.2.5.3. 分组引用

以日期为例，匹配三种格式的日期：`2021-05-27`、`2021/05/27`、`2021.05.27`，首先想到的正则可能是`"\\d{4}(-|\\/|\\.)\\d{2}\\1\\d{2}"`但是这种写法也能匹配到形如`2021-05/27`形式的日期即分隔符不相同的日期。

解决方案是分组引用，大部分情况下用`\number`来引用已经存在的分组，比如：

```swift{.line-numbers}
let regex = "\\d{4}(-|\\/|\\.)\\d{2}\\1\\d{2}"
var date1 = "2021-05-27";
var date2 = "2021/05/27";
var date3 = "2021.05.27";
var dateWithWrongFormat = "2021-05/27";

print(testRegularExpressionCaptureGroups(regex: regex, validateString: date1)) //Print: [["2021-05-27", "-"]]
print(testRegularExpressionCaptureGroups(regex: regex, validateString: date2))//print: [["2021/05/27", "/"]]
print(testRegularExpressionCaptureGroups(regex: regex, validateString: date3))//Print: [["2021.05.27", "."]]
print(testRegularExpressionCaptureGroups(regex: regex, validateString: dateWithWrongFormat))
//Print: No matches in "2021-05/27" []
```

> 很多语言支持命名分组，语法为`(?P<GROUP_NAME>RegularExpression)`。由官方文档可知，*Swift*似乎暂> 不支持`<>`运算符,也就无从支持命名分组了。不过`NSTextCheckingResult`类中提供了函数
> `open func range(withName name: String) -> NSRange`,似乎又可存有期待。

#### 1.2.5.4. 分组嵌套

当分组出现嵌套时，如何区分分组编号？很简单：从左至右数左括号是第几个，就是第几个子组。

```swift{.line-numbers}
let regex = "((\\d{4})-(\\d{2})-(\\d{2}))   ((\\d{2}):(\\d{2}):(\\d{2}))"
let code = "2021-05-27   09:13:18"
print(testRegularExpressionCaptureGroups(regex: regex, validateString: code))
//Print: [["2021-05-27   09:13:18", "2021-05-27", "2021", "05", "27", "09:13:18", "09", "13", "18"]]
```

#### 1.2.5.5. 不捕获子组

某些情况下，只是把括号里的内容看成一个整体，后续不再使用，即不必要保存子组，不保存子组可以提高正则的性能，也可以理解为**只分组不分配响应的编号**。语法为`(?:RgularExpression)`。

### 1.2.6. 四种常见的匹配模式

- 不区分大小写
  
  ```swift{.line-numbers}
    let regex = "(?i)cat"
    let code = "cat CAT Cat cAt caT"
    print(testRegularExpression(regex: regex, validateString: code))
    //Print: ["cat", "CAT", "Cat", "cAt", "caT"]
  ```

- 点号通配符模式
- 多行匹配模式:`(?m)RegularExpression`
- 注释模式:`(?#COMMMENT)`

### 1.2.7. 断言

#### 1.2.7.1. 单词边界

```swift{.line-numbers}
func replaceWhenRegularExpressionMatch(_ regex: String, _ validateString: String, with template: String) -> String{
    do {
        let regex: NSRegularExpression = try NSRegularExpression(pattern: regex, options: [])
        let temp = regex.stringByReplacingMatches( in: validateString , options: [], range: NSMakeRange(0, validateString.count),withTemplate: template)
        return temp
    } catch {
        return "Error when create regex!"
    }
}
let regex = "tom"
var code = "tom asked me if I would go fishing with him tomorrow."
print(replaceWhenRegularExpressionMatch(regex, code, with: "Jerry"))
//Print: Jerry asked me if I would go fishing with him Jerryorrow.
```

很明显，这样子替换是有问题的，把*tomorrow*中的*tom*也替换了，解决方案是使用单词边界。

```swift{.line-numbers}
let regex = "\\btom\\b"
var code = "tom asked me if I would go fishing with him tomorrow."
print(replaceWhenRegularExpressionMatch(regex, code, with: "Jerry"))
//Print: Jerry asked me if I would go fishing with him tomorrow.
```

#### 1.2.7.2. 环视(Look Around)

环视就是要求在匹配的前面或后面要求满足/不满足某些规则，有时也叫**零宽断言**。

| 正则     | 名称                               | 含义        | 示例                                         |
| :------- | :--------------------------------- | :---------- | :------------------------------------------- |
| `(?<=Y)` | 肯定逆序环视(Positive look behind) | 左边是*Y*   | `(?<=\d)`左边是数字的*th*,可以匹配*9th*      |
| `(?<!Y)` | 否定逆序环视(negative look behind) | 左边不是*Y* | `(?<=\d)`左边不是数字的*th*,可以匹配*health* |
| `(?=Y)`  | 肯定逆序环视(Positive look ahead)  | 右边是*Y*   | `six(?=\d)`右边是数字的*six*,可以匹配*six6*  |
| `(?!Y)`  | 肯定逆序环视(negative look ahead)  | 右边不是*Y* | `hi(?!\d)`右边不是数字的*hi*,可以匹配*high*  |

记忆口诀：左尖括号代表看左边，没尖括号代表看右边，感叹号表示非。

> **环视中也有括号，但是不保存为子组。**
