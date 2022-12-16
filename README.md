# Overhead-and-Shelf-Out

Select * from (select*, concat(STR_NBR,SKU_NUMBER) as unique_identifier_1

 from MET_BASE.SHELF_OUT_DATA) as S

 join ( select *, concat(store_number, sku_number) as unique_identifier_2
  from `analytics-met-thd.MET_STAGE.OVERHEAD_MULTIPLE_LOCATION` )  as O on

  O.unique_identifier_2 = S.unique_identifier_1;

  ### skus that are scanned out and that also have been seen overhead ###


with overhead as (
 
 select*, concat(STR_NBR,SKU_NUMBER) as unique_identifier_1

 from MET_BASE.SHELF_OUT_DATA), 
 
 shelf as ( select *, concat(store_number, sku_number) as unique_identifier_2
from `analytics-met-thd.MET_STAGE.OVERHEAD_MULTIPLE_LOCATION`)

select overhead.*

from overhead

join shelf on 

overhead.unique_identifier_1 = shelf.unique_identifier_2;
![image](https://user-images.githubusercontent.com/17092274/208141711-3c3611c8-625d-41ec-9339-e87d5df36d17.png)
