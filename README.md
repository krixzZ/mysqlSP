# mysqlSP
Ejemplos Store Procedures MySQL

STORED PROGRAMS MYSQL
----------------------

1. Stored Procedures (desde app con acceso a BD)
2. Stored functions (desde SQL)
3. Triggers
4. Events (ejecución programada)


-- creando SP
-- dice que el delimitador sera //
DELIMETER // 
CREATE PROCEDURE prueba()
BEGIN
	SELECT 'esta es una prueba' AS mimensaje1,
		   'esta es una prueba' AS mimensaje2',
		   'esta es una prueba' AS mimensaje3';
END //
DELIMETER ;

-- SP2
DELIMETER // 
CREATE PROCEDURE prueba2()
BEGIN
	DECLARE nuevos int;

	SELECT COUNT(*)
	INTO nuevos
	FROM bdpndientes.pendientes
	INNER JOIN estatuspendiente ON estatuspendiente.id = pendientes.idEstatusPendiente
	WHERE estatuspendiente.estatus = 'NUEVO';

	SELECT nuevos AS prndientesnuevos,
		   'esta es una prueba' AS mimensaje2',
		   'esta es una prueba' AS mimensaje3';
END //
DELIMETER ;


-- llamando al SP
call prueba();


-- drop
drop procedure prueb;


-- SP más avanzado IF
DELIMITER //

CREATE PROCEDURE totalpendientes(in vatIdPersonaAsignado, out frase varhar(50), out persona varchar(50))
BEGIN

	declare totalpendientes int;

	select count(*)
	into totalpendientes
	from pendientes
	where idPersonasAsignado=varIdPersonaAsigado;

	select nombre
	into persona
	from personas
	where id=varPersonaAsignado;

	if totalpendientes=0 then
		set frase='NO TIENE PENDIENTES';
	elseif totalpendientes>=1 and totalpendientes<=3 then
		set frase=CONCAT('ESTA ALGO OCUPADO',totalpendientes,' PENDIENTES');
	elseif totalpendientes>=4 then
		set frase=CONCAT('TIENE MUCHO TRABAJO',totalpendientes,' PENDIENTES');
	end if;

END //
DELIMITER ;

-- llamar a SP
call totalpendientes (3,@frase,@persona);
select @frase,@persona;


-- SP más avanzado CASE/WHEN
DELIMITER //
CREATE PROCEDURE totalpendientesCASE(in vatIdPersonaAsignado, out frase varhar(50), out persona varchar(50))
BEGIN

	declare totalpendientes int;

	select count(*)
	into totalpendientes
	from pendientes
	where idPersonasAsignado=varIdPersonaAsigado;

	select nombre
	into persona
	from personas
	where id=varPersonaAsignado;

	case totalpendientes
		when totalpendients>=1 and totalpendientes<=3
			set frase=CONCAT('ESTA ALGO OCUPADO',totalpendientes,' PENDIENTES');
		when totalpendients>=4
			set frase=CONCAT('TIENE MUCHO TRABAJO',totalpendientes,' PENDIENTES');
		else
			set frase='NO TIENE PENDIENTES';
		end case;

END //
DELIMITER ;

-- llamar a SP
call totalpendientesCASE (3,@frase,@persona);
select @frase,@persona;















