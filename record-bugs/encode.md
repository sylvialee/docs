## js与PHP编码之异同

# js编码
* escape / 
* encodeURI / decodeURI
* encodeURIComponent / decodeURIComponent


# PHP编码
* encodeurl / decodeurl
* rowencodeurl / rowdecodeurl


# 两者保持一直需要js做转码
<pre>
    function fixedEncodeURIComponent (str) {
    return encodeURIComponent(str).replace(/[!'()*]/g, function(c) {
        return '%' + c.charCodeAt(0).toString(16).toUpperCase();
    });
    }

</pre>