
## String

### match

字符串实例对象的 `match()` 方法对字符串进行正则匹配，返回匹配结果。

```typescript
// lib.es5.d.ts
interface RegExpMatchArray extends Array<string> {
    index?: number;
    input?: string;
}

interface String {
    
    // lib.es5.d.ts
    /**
     * Matches a string with a regular expression, and returns an array containing the results of that search.
     * @param regexp A variable name or string literal containing the regular expression pattern and flags.
     */
    match(regexp: string | RegExp): RegExpMatchArray | null;

    // lib.es2015.symbol.wellknown.d.ts
    /**
     * Matches a string an object that supports being matched against, and returns an array containing the results of that search.
     * @param matcher An object that supports being matched against.
     */
    match(matcher: { [Symbol.match](string: string): RegExpMatchArray | null; }): RegExpMatchArray | null;

}
```

字符串的 `match()` 方法与正则对象的 `exec()` 方法非常类似：匹配成功返回一个数组，匹配失败返回 null。

如果正则表达式带有 `g` 修饰符，则该方法与正则对象的 `exec()` 方法行为不同，会一次性返回所有匹配成功的结果。

#### demo

```TypeScript
function getQuery(key) {
    var m = "",
        location = global.location;
    if (location) {
        m = location.search.match(new RegExp('(\\?|&)' + key + '=([^&]*)(#|&|$)'));
    }
    return !m ? "" : decodeURIComponent(m[2]);
}

function getCookie(key) {
    var r = new RegExp("(?:^|;+|\\s+)" + key + "=([^;]*)");
    var m = '';
    if (global.document) {
        m = global.document.cookie.match(r);
    }
    return (!m ? "" : m[1]) || null;
}
```

**getQuery** 获取当前 URL 中指定参数的值：`?key=value` 或 `&key=value`

```
RegExp('(\\?|&)' + key + '=([^&]*)(#|&|$)');
```

1. 第1个分组匹配界定起始位置：`?` 或 `&`；  
2. 接下来固定匹配 `key=`：`?key=` 或 `&key=`；  
3. 接下来匹配=号之后的 value：

- 第2个分组匹配纯值部分：若干个非 `&` 字符；  
- 第3个分组匹配界定结束位置：`#` 或 `&` 或 `$`；  

返回 = group[2]

**getCookie** 获取当前 cookie 中指定参数的cookie值。

```
RegExp("(?:^|;+|\\s+)" + key + "=([^;]*)");
```

non group = `(?:^|;+|\\s+)` = `?:^` or `;+` or `\\s+`，匹配界定 key 的起始位置

`?:` 表示 non-capturing group，`^` 表示什么意思呢？

- `;+`：1个或多个 `;`  
- `\\s+`：1个或多个 whitespace  

接下来固定匹配 `key=`  

group1 = `[^;]*`，匹配=号之后的 value，若干个 非 `;` 字符（遇到 `;` 结束）。

返回 = group[1]

### search

字符串对象的 `search()` 方法，返回 **第一个** 满足条件的匹配结果在整个字符串中的位置。  
如果没有任何匹配，则返回 -1。

```typescript

interface String {

    // lib.es5.d.ts
    /**
     * Finds the first substring match in a regular expression search.
     * @param regexp The regular expression pattern and applicable flags.
     */
    search(regexp: string | RegExp): number;

    // lib.es2015.symbol.wellknown.d.ts
    /**
     * Finds the first substring match in a regular expression search.
     * @param searcher An object which supports searching within a string.
     */
    search(searcher: { [Symbol.search](string: string): number; }): number;

}
```

### split

字符串对象的 `split()` 方法按照正则规则分割字符串，返回一个由分割后的各个部分组成的数组。

该方法接受两个参数，第一个参数是正则表达式，表示分隔规则，第二个参数是返回数组的最大成员数。

```typescript
interface String {

    // lib.es5.d.ts
    /**
      * Split a string into substrings using the specified separator and return them as an array.
      * @param separator A string that identifies character or characters to use in separating the string. If omitted, a single-element array containing the entire string is returned.
      * @param limit A value used to limit the number of elements returned in the array.
      */
    split(separator: string | RegExp, limit?: number): string[];

    // lib.es2015.symbol.wellknown.d.ts
    /**
     * Split a string into substrings using the specified separator and return them as an array.
     * @param splitter An object that can split a string.
     * @param limit A value used to limit the number of elements returned in the array.
     */
    split(splitter: { [Symbol.split](string: string, limit?: number): string[]; }, limit?: number): string[];
}
```

#### demo

```TypeScript
export function removeURLParameter(url, parameter) {
    // prefer to use l.search if you have a location/link object
    let urlparts = url.split('?');
    if (urlparts.length >= 2) {
        let prefix = encodeURIComponent(parameter) + '=';
        let pars = urlparts[1].split(/[&;]/g);

        // reverse iteration as may be destructive
        for (let i = pars.length; i-- > 0;) {
            // idiom for string.startsWith
            if (pars[i].lastIndexOf(prefix, 0) !== -1) {
                pars.splice(i, 1);
            }
        }

        url = urlparts[0] + (pars.length > 0 ? '?' + pars.join('&') : '');
        return url;
    } else {
        return url;
    }
}
```

### replace

字符串对象的 `replace()` 方法可以替换匹配的值。它接受两个参数，第一个是正则表达式，表示搜索模式，第二个是替换的内容。

正则表达式如果不加 `g` 修饰符，就替换第一个匹配成功的值，否则替换所有匹配成功的值。

```typescript
interface String {

    // lib.es5.d.ts
    /**
      * Replaces text in a string, using a regular expression or search string.
      * @param searchValue A string to search for.
      * @param replacer A function that returns the replacement text.
      */
    replace(searchValue: string | RegExp, replacer: (substring: string, ...args: any[]) => string): string;


    // lib.es2015.symbol.wellknown.d.ts
    /**
     * Replaces text in a string, using an object that supports replacement within a string.
     * @param searchValue A object can search for and replace matches within a string.
     * @param replaceValue A string containing the text to replace for every successful match of searchValue in this string.
     */
    replace(searchValue: { [Symbol.replace](string: string, replaceValue: string): string; }, replaceValue: string): string;

}
```

以下代码片段用于消除字符串首尾的空格：

```javascript
var str = '  #id div.class  ';

str.replace(/^\s+|\s+$/g, '')
// "#id div.class"
```

`replace()` 方法的第二个参数可以使用美元符号 `$`，用来指代所替换的内容。

- $&：匹配的子字符串。  
- $`：匹配结果前面的文本。  
- $'：匹配结果后面的文本。  
- $n：匹配成功的第n组内容，n是从1开始的自然数。  
- \$\$：指代美元符号 `$`。  

#### demo

```TypeScript
const REGEX_URL_CHAR = new RegExp('(' + /[-:@a-zA-Z0-9_.,~%+/\\?=&#!;()[\]$]/.source + ')');
const REGEX_URL_PROTO = /\b(?:(?:https?|s?ftp|ftps|file|nfs):\/\/|mailto:|tel:|www\.)/;
const REGEX_URL = new RegExp(REGEX_URL_PROTO.source + REGEX_URL_CHAR.source + '+', 'ig');

export function detectURL(str = '') {
    return str.replace(REGEX_URL, (url) => {
        const href = url.indexOf(':') > -1 ? url : `//${url}`;
        return `<a href="javascript:void(0);" data-href=${href}>${url}</a>`;
    });
}
```

## RegExp

`RegExp.prototype.lastIndex`：返回一个整数，表示`下一次开始搜索的位置`。该属性可读写，但是只在进行连续搜索时有意义。

### test

正则实例对象的 `test()` 方法返回一个布尔值，测试给定的参数字符串是否匹配当前模式。

```typescript
// lib.es5.d.ts
interface RegExp {

    /**
      * Returns a Boolean value that indicates whether or not a pattern exists in a searched string.
      * @param string String on which to perform the search.
      */
    test(string: string): boolean;

}
```

#### demo

```
let isIOS = /(iphone|ipad|ipod)/i.test(window.navigator.userAgent);
let isiPhoneX = /iphone x/gi.test(window.navigator.userAgent);
const isQBSideBar = /(PCQQBrowser)/i.test(window.navigator.userAgent) && /(qbsidebar)/i.test(window.navigator.userAgent);
```

### exec

正则实例对象的 `exec()` 方法，返回参数字符串匹配当前模式的结果。

如果发现匹配，就返回一个数组，成员是匹配成功的子字符串，否则返回 **null**。

如果正则表达式中定义了组，就可以在 **RegExp** 对象上用 `exec()` 方法提取出子串来。

`exec()` 方法在匹配成功后，会返回一个 **Array**，第一个元素是正则表达式匹配到的整个字符串，后面的字符串表示匹配成功的子串。  
`exec()` 方法在匹配失败时返回 **null**。

```typescript
// lib.es5.d.ts
interface RegExpExecArray extends Array<string> {
    index: number;
    input: string;
}

interface RegExp {

    /**
      * Executes a search on a string using a regular expression pattern, and returns an array containing the results of that search.
      * @param string The String object or string literal on which to perform the search.
      */
    exec(string: string): RegExpExecArray | null;

}
```

exec 方法的返回数组还包含以下两个属性：

- `input`：整个原字符串。  
- `index`：整个模式匹配成功的开始位置（从0开始计数）。  

正则表达式加上 `g` 修饰符，则可以多次调用 `exec()` 方法，下一次搜索的位置从上一次匹配成功结束的位置开始。

```shell
Ξ ~ → node
> let s = 'JavaScript, VBScript, JScript and ECMAScript';
undefined
> let re = /[a-zA-Z]+Script/g
undefined
> re.exec(s);
[ 'JavaScript',
  index: 0,
  input: 'JavaScript, VBScript, JScript and ECMAScript',
  groups: undefined ]
> re.lastIndex
10
> re.exec(s)
[ 'VBScript',
  index: 12,
  input: 'JavaScript, VBScript, JScript and ECMAScript',
  groups: undefined ]
> re.lastIndex
20
> re.exec(s)
[ 'JScript',
  index: 22,
  input: 'JavaScript, VBScript, JScript and ECMAScript',
  groups: undefined ]
> re.lastIndex
29
> re.exec(s)
[ 'ECMAScript',
  index: 34,
  input: 'JavaScript, VBScript, JScript and ECMAScript',
  groups: undefined ]
> re.lastIndex
44
> re.exec(s)
null
```

利用 `g` 修饰符允许多次匹配的特点，可以用一个循环完成全部匹配。

```shell
~ » node
> .editor
// Entering editor mode (^D to finish, ^C to cancel)
let s = 'JavaScript, VBScript, JScript and ECMAScript';
let re = /[a-zA-Z]+Script/g;

while(true) {
    let match = re.exec(s);
    if (!match) break;
    console.log('#' + match.index + ':' + match[0]);
}

#0:JavaScript
#12:VBScript
#22:JScript
#34:ECMAScript
undefined
>
```

在上面代码中，只要 `exec` 方法不返回 null，就会一直循环下去，每次输出匹配的位置和匹配的文本。

#### demo

```TypeScript
let filename = 'word2019.xlsx'; // 'excel2019.xlsx';
let filetype = null;
let filetypes = { doc: 'doc', xls: 'sheet' };
let refileext = /\.([^\.]{3})[^\.]*$/.exec((filename + "").toLowerCase());
let fileext = refileext[1];
if (fileext) {
    filetype = filetypes[fileext]
}
```

`\.([^\.]{3})[^\.]*$`:

1. 以 `.` 开头；  
2. `([^\.]{3})`：三个非 `.` 字符；  
3. 紧接着以0或多个非 `.` 字符结尾。  

**测试**：.doc、.docx 后缀类型的文件名返回 doc；.xls、xlsx 后缀类型的文件名返回 sheet。

## demo

以下综合示例基于微信小程序的 UserAgent 提取 iOS/Android 版本号。

```shell
MBP-FAN at ~ ❯ node
> .editor
// Entering editor mode (^D to finish, ^C to cancel)
let iMPUA='Mozilla/5.0 (iPhone; CPU iPhone OS 11_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15F79 MicroMessenger/6.7.0 NetType/WIFI Language/zh_CN';
let aMPUA='Mozilla/5.0 (Linux; Android 7.1.1; OS105 Build/NGI77B; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/53.0.2785.143 Crosswalk/24.53.595.0 XWEB/155 MMWEBSDK/19 Mobile Safari/537.36 MicroMessenger/6.6.6.1300(0x26060638) NetType/WIFI Language/zh_CN MicroMessenger/6.6.6.1300(0x26060638) NetType/WIFI Language/zh_CN miniProgram';

// RegExp.test()
let it = /os (\d+((\.|_)\d+)*)/i.test(iMPUA);
let irs = 'os (\\d+((\\.|_)\\d+)*)';
let ire = new RegExp(irs);

// String.match()
let im1 = iMPUA.toLowerCase().match(ire);
// RegExp.exec()
let im2 = ire.exec(iMPUA.toLowerCase());
let im3 = RegExp(/os (\d+((\.|_)\d+)*)/i).exec(iMPUA.toLowerCase());
let iv = im3[1].replace(/_/g, '.');

// RegExp.test()
let at = /android[/ ](\d+((\.|_)\d+)*)/i.test(aMPUA);
let ars = 'android[/ ](\\d+((\\.|_)\\d+)*)';
let are = new RegExp(ars);

// String.match()
let am1 = aMPUA.toLowerCase().match(are);
// RegExp.exec()
let am2 = are.exec(aMPUA.toLowerCase());
let am3 = RegExp(/android[\/ ](\d+((\.|_)\d+)*)/).exec(aMPUA.toLowerCase());
let av = am3[1].replace(/_/g, '.');

undefined

> it
true
> ire
/os (\d+((\.|_)\d+)*)/
> im1 // im2 // im3
[ 'os 11_4',
  '11_4',
  '_4',
  '_',
  index: 32,
  input: 'mozilla/5.0 (iphone; cpu iphone os 11_4 like mac os x) applewebkit/605.1.15 (khtml, like gecko) mobile/15f79 micromessenger/6.7.0 nettype/wifi language/zh_cn',
  groups: undefined ]
> iv
'11.4'
> 
> at
true
> are
/android[\/ ](\d+((\.|_)\d+)*)/
> am2 // am1 // am3
[ 'android 7.1.1',
  '7.1.1',
  '.1',
  '.',
  index: 20,
  input: 'mozilla/5.0 (linux; android 7.1.1; os105 build/ngi77b; wv) applewebkit/537.36 (khtml, like gecko) version/4.0 chrome/53.0.2785.143 crosswalk/24.53.595.0 xweb/155 mmwebsdk/19 mobile safari/537.36 micromessenger/6.6.6.1300(0x26060638) nettype/wifi language/zh_cn micromessenger/6.6.6.1300(0x26060638) nettype/wifi language/zh_cn miniprogram',
  groups: undefined ]
> av
'7.1.1'
```