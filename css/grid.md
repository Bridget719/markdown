依然是推荐链接：http://cssgridgarden.com/
![alt](https://uploadfiles.nowcoder.com/images/20220316/167993455_1647382326701/D2B5CA33BD970F64A6301FA75AE2EB22)

主要属性有:
- grid-template-rows,grid-template-coumns(简写grid-template)<br><br>
单位有%、px、em,还有fr（倍）（将除前三个单位分配剩下的部分按比例分配），还可以使用repeat,如repeat(5,20%)<br>
- item项：
grid-column-start、grid-column-end(简写grid-column)<br><br>
 (grid-column-end值可为负数，可以比start小，还可以使用span指定个数，如grid-column-end:span 2)<br>
- grid-row同理，grid-row-start,grid-column-start,grid-row-end,grid-column-end的简写为grid-area
 
- 简写时,值用‘/’分隔