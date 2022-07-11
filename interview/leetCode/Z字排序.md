```js
var ZReserve=function(numRows,s){
    if(numRows==1) return s
    let arr=new Array(numRows).fill('')
    let row=0 //当前处在第几行
    for(let i=0,len=s.length,down=true;i<len;i++){
        arr[row]+=s[i]
        if(down)
            row++
        else 
            row--
        if(row==numRows-1)
            down=false
        else if(row==0)
           down=true   
    }
    return arr.join('')
}
```

