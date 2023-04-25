# TBSMARKET
—----------------------11Obtener SUBTOTAL de productos vendidos basado en la tabla VENTA_DETALLE.
select
 vd.idven,
 pro.NOMPRO as NOMPRO,
 pro.PREPRO as PREPRO,
 vd.CANVENDET as CANVENDET,
 (pro.prepro * vd.canvendet) as SUBTOTAL
from 
 VENTA_DETALLE vd inner join  PRODUCTO pro on vd.CODPRO = pro.CODPROD;

—------------------------12Listar Identificador de la venta, vendedor y subtotal de ventas.
select
 vd.idven,
 ven.idvend,
 (pro.prepro * vd.canvendet) as SUBTOTAL
from 
 VENTA_DETALLE vd inner join  PRODUCTO pro on vd.CODPRO = pro.CODPROD
 inner join VENTA ven ON  ven.IDVEN = vd.IDVEN ;

—---------------------13Listar monto total de ventas por VENDEDOR
select
 pe.idper as ID,
 (pe.apeper ||','||' ' || pe.nomper) as VENDEDOR,
 SUM(pro.prepro * vd.canvendet) as SUBTOTAL
from 
 VENTA_DETALLE vd inner join  PRODUCTO pro on vd.CODPRO = pro.CODPROD
 inner join VENTA ven ON  ven.IDVEN = vd.IDVEN
 inner join PERSONA pe on pe.IDPER = ven.IDVEND
GROUP BY pe.idper,(pe.apeper ||','||' ' || pe.nomper);


—--------14Listar cantidad de productos por CATEGORIA.
select 
cat.nomcat as CATEGORIA,
count(pro.IDCATPRO) as CANTIDAD
from categoria cat inner join producto pro on pro.IDCATPRO = cat.IDCAT
GROUP BY cat.nomcat;

—----------------15Listar la inversión total con que se cuenta en productos por cada categoría.
SELECT 
CAT.NOMCAT AS CATEGORIA,
'S/. ' || SUM(PRO.PREPRO * PRO.STOCKPRO) AS SUBTOTAL
FROM PRODUCTO PRO INNER JOIN CATEGORIA CAT ON PRO.IDCATPRO=IDCAT GROUP BY CAT.NOMCAT;

Listar los CLIENTES que no han realizado compras.
select
 (UPPER(pe.apeper) ||','||' ' || pe.nomper) as Cliente,
 pe.celper as CELULAR,
 pe.emaper as EMAIL,
 ven.IDVEN AS IDVEN
from Persona pe left join VENTA ven on ven.IDCLI = pe.IDPER
WHERE pe.tipper= 'C' and ven.IDVEN is NULL;

