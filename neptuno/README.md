## Código xml de entrada

```xml
<?xml version="1.0" encoding="UTF-8"?>
<neptuno>
  <articulos>
  <RefArticulo>10</RefArticulo>
  <ReferenciaProveedor>100</ReferenciaProveedor>
  <RefCliente>1</RefCliente>
  <NombreArticulo>Jugo de Manzana</NombreArticulo>
  <NombreCategoria>Bebidas</NombreCategoria>
  <PrecioUnidad>30</PrecioUnidad>
  <UnidadesExistencia>40</UnidadesExistencia>
</articulos>
<clientes>
  <RefCliente>1</RefCliente>
  <NombreCliente>Juan</NombreCliente>
  <DireccionCliente>Taco</DireccionCliente>
  <CiudadCliente>París</CiudadCliente>
  <CodPostalCliente>38206</CodPostalCliente>
  <PaisCliente>Francia</PaisCliente>
  <TelefornoCliente>6666666</TelefornoCliente>
</clientes>
<proveedores>
  <ReferenciaProveedor>100</ReferenciaProveedor>
  <NombreProveedor>David</NombreProveedor>
  <PaisProveedor>Francia</PaisProveedor>
</proveedores>
</neptuno>
```

## Consulta 1
```xml
<html>
<head>Primera Consulta</head>
  <body>
    <table>
      <tr border="3">
        <td>Referencia del Artículo</td>
        <td>Referencia del Proveedor</td>
        <td>Nombre del Artículo</td>
      </tr>
      {
        for $articulo in doc("neptuno.xml") //articulos
        return
        <tr>
          <td>{data($articulo/RefArticulo)}</td>
          <td>{data($articulo/ReferenciaProveedor)}</td>
          <td>{data($articulo/NombreArticulo)}</td>
        </tr>
      }
  </table>
  </body>
</html>
```
```html
<html>
  <head>Primera Consulta</head>
  <body>
    <table>
      <tr>
        <td>Referencia del Artículo</td>
        <td>Referencia del Proveedor</td>
        <td>Nombre del Artículo</td>
      </tr>
      <tr>
        <td>10</td>
        <td>100</td>
        <td>Jugo de Manzana</td>
      </tr>
    </table>
  </body>
</html>
```
## Consulta 2
```html
<html>
<head>Segunda Consulta</head>
  <body>
    <table>
      <tr>
        <td>Referencia Cliente</td>
        <td>NOmbre Cliente</td>
        <td>Referencia Artículo</td>
      </tr>
      {
        for $articulo in doc("neptuno.xml") //articulos
        for $cliente in doc("neptuno.xml") //clientes
        where $articulo/NombreCategoria="Bebidas" 
          and $articulo/RefCliente=$cliente/RefCliente
        return
        <tr>
          <td>{data($cliente/RefCliente)}</td>
          <td>{data($cliente/NombreCLiente)}</td>
          <td>{data($articulo/RefArticulo)}</td>
        </tr>
      }
  </table>
  </body>
</html>
```
### Salida de consulta 2
```html
<html>
  <head>Segunda Consulta</head>
  <body>
    <table>
      <tr>
        <td>Referencia Cliente</td>
        <td>NOmbre Cliente</td>
        <td>Referencia Artículo</td>
      </tr>
      <tr>
        <td>1</td>
        <td/>
        <td>10</td>
      </tr>
    </table>
  </body>
</html>
```
## Consulta 3
```xml
<html>
<head>Segunda COnsulta</head>
  <body>
    <table>
      <tr>
        <td>Referencia Artículo</td>
        <td>Nombre del Artículo</td>
        <td>Nombre de Proveedor</td>
        <td>País de Proveedor</td>
      </tr>
      {
        for $articulo in doc("neptuno.xml") //articulos
        for $proveedor in doc("neptuno.xml") //proveedores
        where $articulo/NombreCategoria="Bebidas" 
        and
        $articulo/ReferenciaProveedor=$proveedor/ReferenciaProveedor
        return
        <tr>
          <td>{data($articulo/RefArticulo)}</td>
          <td>{data($articulo/NombreArticulo)}></td>
          <td>{data($proveedor/NombreProvedoor)}</td>
          <td>{data($proveedor/PaisProveedor)}</td>
        </tr>
      }
  </table>
  </body>
</html>
```
### Salida Consulta 3
```html
<html>
  <head>Segunda COnsulta</head>
  <body>
    <table>
      <tr>
        <td>Referencia Artículo</td>
        <td>Nombre del Artículo</td>
        <td>Nombre de Proveedor</td>
        <td>País de Proveedor</td>
      </tr>
      <tr>
        <td>10</td>
        <td>Jugo de Manzana&gt;</td>
        <td/>
        <td>Francia</td>
      </tr>
    </table>
  </body>
</html>
```

## Consulta 4
```xml
<html>
<head>Segunda COnsulta</head>
  <body>
    <table>
      <tr>
        <td>Nombre del Cliente</td>
        <td>Nombre del Artículo</td>
        <td>Nombre de Proveedor</td>
      </tr>
      {
        for $articulo in doc("neptuno.xml") //articulos
        for $cliente in doc("neptuno.xml") //clientes
        for $proveedor in doc("neptuno.xml") //proveedores
        where $articulo/NombreCategoria="Bebidas" 
          and $articulo/RefCliente=$cliente/RefCliente
          and
         $articulo/ReferenciaProveedor=$proveedor/ReferenciaProveedor
        return
        <tr>
          <td>{data($cliente/NombreCliente)}</td>
          <td>{data($articulo/NombreArticulo)}></td>
          <td>{data($proveedor/NombreProvedoor)}</td>
        </tr>
      }
  </table>
  </body>
</html>
```
```html
<html>
  <head>Segunda COnsulta</head>
  <body>
    <table>
      <tr>
        <td>Nombre del Cliente</td>
        <td>Nombre del Artículo</td>
        <td>Nombre de Proveedor</td>
      </tr>
      <tr>
        <td>Juan</td>
        <td>Jugo de Manzana&gt;</td>
        <td/>
      </tr>
    </table>
  </body>
</html>
```
