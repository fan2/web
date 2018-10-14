
## String

### match

```typescript
// lib.es5.d.ts
interface RegExpMatchArray extends Array<string> {
    index?: number;
    input?: string;
}

// lib.es2015.symbol.wellknown.d.ts
interface String {

    /**
     * Matches a string an object that supports being matched against, and returns an array containing the results of that search.
     * @param matcher An object that supports being matched against.
     */
    match(matcher: { [Symbol.match](string: string): RegExpMatchArray | null; }): RegExpMatchArray | null;

}
```

### replace

```typescript
// lib.es2015.symbol.wellknown.d.ts
interface String {

    /**
     * Replaces text in a string, using an object that supports replacement within a string.
     * @param searchValue A object can search for and replace matches within a string.
     * @param replaceValue A string containing the text to replace for every successful match of searchValue in this string.
     */
    replace(searchValue: { [Symbol.replace](string: string, replaceValue: string): string; }, replaceValue: string): string;

}
```

## RegExp

### test

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

### exec

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