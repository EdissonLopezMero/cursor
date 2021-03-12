# cursor
cursor que muestra los clientes deudores
declare @cedula_cliente char(10),@nombres char(30),
		@nombre_mes char(5),@descripcion_l char(5),
		@total_l char(5)

declare deudores cursor
	for select cedula_clientepk,nombres,nombre_mes,descripcion_l,total_l 
	from ConsumodeElectrico 
	inner join meses on id_mes=id_mespk 
	inner join clientes on cedula_cliente=cedula_clientepk
where descripcion_l='deuda'
open deudores
fetch deudores into @cedula_cliente ,@nombres ,@nombre_mes ,
					@descripcion_l ,@total_l 
while (@@FETCH_STATUS=0)
		begin
		print  @cedula_cliente +space(5)+@nombres+space(3)+@nombre_mes +''+
		@descripcion_l +space(3)+@total_l
		fetch deudores into @cedula_cliente ,@nombres ,@nombre_mes ,@descripcion_l ,
							@total_l 
		end 
		close deudores
		deallocate deudores
