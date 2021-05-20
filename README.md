# code-snippets
anotaciones propias de trozos de código y funciones utiles en general

## ordenamiento de precios de sitio web lider.cl
### valido para seccion mundo lider 
```
var jq = document.createElement('script');
jq.src = "https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js";
document.getElementsByTagName('head')[0].appendChild(jq);
var table = []
$('.product-info').each(function(ix,el){
    var p = {
        producto:$(el).find('.product-description').text(),
        precioactual:parseFloat($(el).find('.walmart-sales-price')[0].innerText.split('\n')[0].replace('$','').replace(/\./g,'')),
        descuento:parseFloat($(el).find('.walmart-discount-percentage-card').text().replace('%','').replace(/\./g,'')),
        precioprevio:parseFloat($(el).find('.walmart-reference-price').text().replace('$','').replace(/\./g,'')),
    }
    p.precioprevio=(isNaN(p.precioprevio)?0:p.precioprevio)
    p.descuento=(isNaN(p.descuento)?0:p.descuento)
    table.push(p)
})
console.table(table)
```

## Calculo de boleta de honorarios
```
function boleta(monto,retencion=11.5){
    return {
        valorRecibido:monto.toLocaleString('de-DE'),
        valorBoleta:Math.ceil(monto*100/(100-retencion)).toLocaleString('de-DE'),
        impuesto:retencion+'%',
        retencion:Math.ceil(monto*100/(100-retencion)-monto).toLocaleString('de-DE')
    }
}
```
