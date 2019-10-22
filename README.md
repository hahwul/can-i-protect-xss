# can-i-protect-xss
Everything about xss protection technology

## :100: Best practice
Get and handle only the values that developers can predict.

e.g 
```
/list?id=1
/list?id=2
/list?id=3
....

In this case, only numeric values are required for the id parameter. 
For these parameters, that you better not to not processing other than type(string, etc..) for avoid multiple vulnerability. 
It's better not to aim for unnecessary reflection and DOM write.
```

## :shield: Protection Technic
### 1. Escape the Special char
`&` => `&amp;`<br>
`"` => `&quot`<br>
`'` => `&#x27;`<br>
`<` => `&lt;`<br>
`>` => `&gt;`<br>
`/` => `&#x2F;`<br>

encoding pattern
- HTML: `&#x3c;`
- URL: `%3c`
- Unicode: `\u003c`
- CSS: `\3c` `\0003c`

### 2. If you needs tag?
filtering xss tags and event handler, dangerous attribute
- filtering xss tags(running with out eventhandler)
```
<script>
<iframe>
<meta>
<style> 
```
- filtering event handlers(any `on*` pattern)
any `on*` pattern regex
```
/on*/g
```

`on*` base event handlers. (There may be more, so please verify with the on* pattern)
```
- refer from code in XSpear
- https://github.com/hahwul/XSpear/blob/master/lib/XSpear.rb
- If you need an event handler list to develop, refer to the path below.
 + https://github.com/hahwul/can-i-protect-xss/blob/master/resource/event_handler.txt

        'onAbort',
        'onActivate',
        'onAfterPrint',
        'onAfterUpdate',
        'onBeforeActivate',
        'onBeforeCopy',
        'onBeforeCut',
        'onBeforeDeactivate',
        'onBeforeEditFocus',
        'onBeforePaste',
        'onBeforePrint',
        'onBeforeUnload',
        'onBeforeUpdate',
        'onBegin',
        'onBlur',
        'onBounce',
        'onCellChange',
        'onChange',
        'onClick',
        'onContextMenu',
        'onControlSelect',
        'onCopy',
        'onCut',
        'onDataAvailable',
        'onDataSetChanged',
        'onDataSetComplete',
        'onDblClick',
        'onDeactivate',
        'onDrag',
        'onDragEnd',
        'onDragLeave',
        'onDragEnter',
        'onDragOver',
        'onDragDrop',
        'onDragStart',
        'onDrop',
        'onEnd',
        'onError',
        'onErrorUpdate',
        'onFilterChange',
        'onFinish',
        'onFocus',
        'onFocusIn',
        'onFocusOut',
        'onHashChange',
        'onHelp',
        'onInput',
        'onKeyDown',
        'onKeyPress',
        'onKeyUp',
        'onLayoutComplete',
        'onLoad',
        'onloadstart',
        'onLoseCapture',
        'onMediaComplete',
        'onMediaError',
        'onMessage',
        'onMouseDown',
        'onMouseEnter',
        'onMouseLeave',
        'onMouseMove',
        'onMouseOut',
        'onMouseOver',
        'onMouseUp',
        'onMouseWheel',
        'onMove',
        'onMoveEnd',
        'onMoveStart',
        'onOffline',
        'onOnline',
        'onOutOfSync',
        'onPaste',
        'onPause',
        'onPopState',
        'onProgress',
        'onPropertyChange',
        'onReadyStateChange',
        'onRedo',
        'onRepeat',
        'onReset',
        'onResize',
        'onResizeEnd',
        'onResizeStart',
        'onResume',
        'onReverse',
        'onRowsEnter',
        'onRowExit',
        'onRowDelete',
        'onRowInserted',
        'onScroll',
        'onSeek',
        'onSelect',
        'onSelectionChange',
        'onSelectStart',
        'onStart',
        'onStop',
        'onStorage',
        'onSyncRestored',
        'onSubmit',
        'onTimeError',
        'onTrackChange',
        'onUndo',
        'onUnload',
        'onURLFlip',
        'ontouchstart',
        'ontouchend',
        'ontouchmove',
        'onafterscriptexecute',
        'onbeforescriptexecute',
        'onpointerover',
        'onpointerdown',
        'onpointerenter',
        'onpointerleave',
        'onpointermove',
        'onpointerout',
        'onpointerup',
        'onloadstart',
        'onloadend'
```

- filtering dangerous attribute
```
style=""
class=""
id=""
name=""
```

### Protection on LocalStorage
```
var content = localStorage.getItem('content') # wost..
var content = XSSProtect(localStorage.getItem('content')) # 
```

## :nut_and_bolt: Mitigation Technic
### CSP
```
Content-Security-Policy: default-src https://google.com
```
https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP

### X-XSS-Protection
```
X-XSS-Protection: 0
X-XSS-Protection: 1
X-XSS-Protection: 1; mode=block
X-XSS-Protection: 1; report=<reporting-uri>
```
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection

## :package: Opensource protection library
- ?

## :crossed_swords: Awesome test vector
- https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection
- https://portswigger.net/web-security/cross-site-scripting/cheat-sheet
- https://blog.rubiya.kr/index.php/2019/03/28/browsers-xss-filter-bypass-cheat-sheet/

## :shipit: Contributing method
Add issue or send pull request contents. I like collaboration.

## :scroll: Reference
https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html<br>
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection<br>
https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP<br>
